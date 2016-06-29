---
layout: post
title: "Bullet Proof Data Science in Scala"
description: "How to use Scala/Spark in such a way that user or machine errors lead to minimal harm?"
headline: 
date: 2016-06-25 14:31:44 +0200
categories:
- Data Science
- Scala
- Missing Values
- Spark
tags: []
imagefeature: 
mathjax: 
chart: 
comments: true
featured: true
---


In this post, we go over some typical aspects and challenges that occur in typical data science projects in order to extract some requirements for data analysis in the broad sense of the word. We then illustrate how we tackle these requirements in typical data science projects using Scala.

# Introduction

## Joining and Annotations

The reality is that often times several data sources need to be aggregated. Aggregation can be in two ways/directions:

1. _Vertical_: New data, similar to what we already have, and
2. _Horizontal_: Additional information about data we already obtained.

## Parsing Libraries

Last week I was parsing a tab-separated file with information about genomic variants (aka a [VCF file](https://github.com/tmoerman/vcf-comp)). The parsing was done using a [custom library](https://github.com/tmoerman/adam-fx) created by a colleague of mine. I had uses the library before, but now suddenly it did not work anymore. All I got was a [confusing error about some exception](https://plus.google.com/u/0/photos/albums/pgjn4t8o2070opjbq27bm8tg97jig4pu5?pid=6293736964412074498&oid=108837720006806497269):

![](https://lh4.googleusercontent.com/-Hsj5FX-c8Q0/V1fYbGmG6gI/AAAAAAAAI3s/i-vrYvoslC0IPUxgRzJWHy9Ib8WlJ3nhgCL0B/w1065-h383-no/2016-06-08.png)

And then, the fun starts. How to find out where things go wrong and how to make sure you don't have to rewrite (part of) the parser? It turned out additional fields can be added to a VCF format file, which the parser does not take into account.

## Missing Values

A similar issue occurs when dealing with missing values, or missing columns in the data. It's very easy to end up with exceptions in the Scala/Java world or equivalent in other languages.

The challenge of missing data becomes even more concrete when additional data is aggregated. Suppose we have additional annotations about a subset of the data. There needs to be a way to cover situations like this.

## Solving the Challenge in Scala

In other words, you don't have control over the input in most cases. In what follows, we describe an approach to data analysis in [Scala](http://www.scala-lang.org/) that takes into account the above challenges. The approach is heavily based on principles of [Functional Programming](https://en.wikipedia.org/wiki/Functional_programming) while capturing the data model in an object model.


# Bullet Proof Data Science

## Missing Values

On important aspect of the above challenges is missing values. Say you're a service organization that keeps records of potential customers. Furthermore, say you want to analyze people's hobbies. You would like to allow for a distinction between 3 situations:

1. There is no information about the customer's hobbies
2. The customer does not have any hobbies
3. The customer has 1 or more hobbies

Say you encode the hobbies as a `List` of `String` (free form), then (2) corresponds to an empty list and (3) corresponds to a list of _n_ hobbies. But what does (1) correspond to? In R, one usually gets `NA`. In Java, one would often sees the occurrence of `null`, but using `null` is not a [good](http://blog.scalac.io/2015/05/31/dealing-with-npe.html) [habit](http://alvinalexander.com/scala/scala-null-values-option-uninitialized-variables).

Instead, we use the `Option` type. It encapsulates whatever other data structure you want. The above 3 situations then correspond to:

1. `None` for no hobbies known about this person
2. `Some(List())` for this person does not have hobbies
3. `Some(List(hobby1, hobby2, ...))` for the hobbies for this person

For the FP (Functional Programming) people among us, the option is a Monad. But let's not go there yet in order not to scare off the others...


## Start with the End in Mind

In our experience, it makes sense to define a good model for the data after aggregation and processing and capture this in an object model. This model need to be the one that can be used as input for a machine learning library as such, but it should capture the logic of the application domain.

And Scala's `case` classes come in very handy. We will not cover the specifics or benefits of case classes here, but remember this: always put `case` in front of your class definition. Oh, and while you're at it, add `val` before every class parameter as well. 

For instance, and to be in line with the discussion above, we could define a `Name` class definition as follows:

```scala
case class Name(val firstName:Option[String], val lastName:Option[String])
```

One can add safe getters and setters if necessary:

```scala
case class Name(val firstName:Option[String], 
                val lastName:Option[String]) {
	def getSafeFirstName = firstName.getOrElse("First name not known")
	def getSafeLastName  = lastName.getOrElse("Last name not known")
}
```

Please note that the safe getters return a `String`, even if the value is not available.


## Safe transformation

Once we encapsulated the data in an `Option`, we can safely process this data as well. There are multiple way to do this, but all come down to the same principle: 

1. Only process _values_ that should be processed, so don't process missing entries, and
2. Make sure the processing itself is _safe_ by catching exceptions where necessary.

Coming back to our example: In practice one seldom gets a dataset with first name and last name clearly split. We could store input as well, and define a companion object in order for people to easily use the API:

```scala
case class Name(val unparsed:Option[String], 
                val firstName:Option[String]=None,
                val lastName:Option[String]=None)

object Name {
	def apply(unparsedStr: String) = new Name(Some(unparsedStr))
	def apply(unparsedStr: String, fnStr:String, lnStr:String) = {
		new Name(Some(unparsedStr), Some(fnStr), Some(lnStr))
	}
}
```

We used default values for the first and last name. Imagine now what you can do with an object model like this:

```scala
val name1BeforeParsing = Name("John Doo")
val name2BeforeParsing = Name("Bar Foo")
val name3BeforeParsing = Name("Franz Octupus")

// A very crude parsing function
def parseName(in:Name):Name = {
	val names = in.unparsed.map(_.split(" "))
	in.copy(firstName = names.map(_(0)), lastName = names.map(_(1)))
}

val name1 = parseName(name1BeforeParsing)
val name2 = parseName(name2BeforeParsing)
val listOfPersons = List(name1, name2, name3BeforeParsing)
```

Now, obviously there are lots of problems with this approach to parsing the name. One could improve this in many ways. For instance, we did not take into account a middle name. One approach to improve the parsing itself could be to use a database of common first names and last names. But that's not the aim of this post. So let us continue with the important stuff here. Let us convert all first names to initials in a safe way:

```scala
def getInitials(s: String):String = s.toCharArray.head.toString.toUpperCase + "."

def firstNameToInitials(name: Name):Name = name.firstName match {
	case Some(nameString) => name.copy(firstName = Some(getInitials(nameString))
		)
	case None => name
}
```

The result is as follows:

```scala
listOfPersons.map(firstNameToInitials).foreach{println}
Name(Some(John Doo),Some(J.),Some(Doo))
Name(Some(Bar Foo),Some(B.),Some(Foo))
Name(Some(Franz Octupus),None,None)
```

See how the function gracefully managed to pass over nonexistent values! The initials of nothing is still nothing. It does not end here, though, because we managed to cope with missing values, but we did not yet make the transformation fully bullet proof! See what happens in the following case:

```scala
firstNameToInitials(parseName(Name("Jacobus")))
java.util.NoSuchElementException: next on empty iterator
  at scala.collection.Iterator$$anon$2.next(Iterator.scala:39)
  at scala.collection.Iterator$$anon$2.next(Iterator.scala:37)
  at scala.collection.IndexedSeqLike$Elements.next(IndexedSeqLike.scala:63)
  at scala.collection.IterableLike$class.head(IterableLike.scala:107)
  at scala.collection.mutable.ArrayOps$ofChar.scala$collection$IndexedSeqOptimized$$super$head(ArrayOps.scala:222)
  at scala.collection.IndexedSeqOptimized$class.head(IndexedSeqOptimized.scala:126)
  at scala.collection.mutable.ArrayOps$ofChar.head(ArrayOps.scala:222)
  at .firstNameToInitials(<console>:10)
  ... 33 elided
```

An easy way to solve this, and one that is compatible with our approach thus far is by using `Try` in Scala. You have two choices now, which depend on how you want the API to work:

1. When an exception occurs during the transformation, let the result be `None`. So in other words, let it correspond to a missing value.
2. When an exception occurs, insert a default value

Both scenarios are shown below:

```scala
import scala.util.Try

val DEFAULT:String = ""

def getInitialsDefault(s: String):Option[String] = {
	Some(Try(s.toCharArray.head.toString.toUpperCase + ".").toOption.getOrElse(DEFAULT))
}

def getInitialsOption(s: String):Option[String] = {
	Try(s.toCharArray.head.toString.toUpperCase + ".").toOption
}


def firstNameToInitials(name: Name, 
                        getInitialF:String=>Option[String]):Name = {
	name.firstName match {
		case Some(nameString) => name.copy(firstName = getInitialF(nameString))
		case None => name
	}
}
```

And use it as follows:

```scala
firstNameToInitials(Name("def", "", "def"), getInitialsDefault _)
res: Name = Name(Some(def),Some(),Some(def))

firstNameToInitials(Name("def", "", "def"), getInitialsOption _)
res: Name = Name(Some(def),None,Some(def))
```

By now, the FP adepts give us 1 point for keeping our data structures immutable: the above functions do not mutate the `name` object, but rather instantiate a new one. 

But we receive a _negative score_ on omitting to acknowledge  that `Option` is a Monad and that a much better way of writing the above exists:

```scala
def getInitialsDefault2(name: Option[String]):Option[String] = 
	name.map( s => Try(s.toCharArray.head.toString.toUpperCase + ".").getOrElse(DEFAULT))

def getInitialsOption2(name: Option[String]):Option[String] = 
	name.flatMap( s => Try(s.toCharArray.head.toString.toUpperCase + ".").toOption)

def firstNameToInitials2(name: Name, 
                         getInitialF:Option[String]=>Option[String]):Name = {
	name.copy(firstName = getInitialF(name.firstName))
}
```

These functions do not exactly do the same as the earlier functions, but they illustrate a very important concept: `map` or `flatMap` on `None` results in `None`. So, there is no need to explicitly use pattern matching here. In order to parse the list of names, we simply `map` over it (indentation added for ease of reading):

```scala
listOfPersons.map(firstNameToInitials2(_, getInitialsDefault2))
res: List[Name] = List(
                    Name(Some(John Doo),Some(J.),Some(Doo)), 
                    Name(Some(Bar Foo),Some(B.),Some(Foo)), 
                    Name(Some(Franz Octupus),None,None))
```

For a nice and graphical introduction to Monads and related concepts, I recommend the following [blog post](http://adit.io/posts/2013-04-17-functors,_applicatives,_and_monads_in_pictures.html). Transformations like the above can be composed in a bullet-proof way, once a missing value or exception occurs, we either continue with a default value or with `None`.

We can go a bit further still for the FP fanatics among us. The function `firstNameToInitials` in fact is _the setter_ part of what is called [a `Lens`](http://koff.io/posts/292173-lens-in-scala/). We will come back to this later in this post.


## Immutability and Lenses

Please note the examples above do not _mutate_ any objects. We use the `copy` method to create an updated version of an object. We will not discuss the benefits of this kind of programming, but just mention the use of a Lens in order to _update_ an immutable data structure.

Several libraries exist for working with Lenses, some based on Scala macros others more high-level. For the sake of the argument, we lift the `Lens` definition out the [Scalaz](https://github.com/scalaz/scalaz) project:

```scala
case class Lens[A,B](get: A => B, set: (A,B) => A) extends Function1[A,B] with Immutable {
  def apply(whole: A): B   = get(whole)
  def updated(whole: A, part: B): A = set(whole, part) // like on immutable maps
  def mod(a: A, f: B => B) = set(a, f(this(a)))
  def compose[C](that: Lens[C,A]) = Lens[C,B](
    c => this(that(c)),
    (c, b) => that.mod(c, set(_, b))
  )
  def andThen[C](that: Lens[B,C]) = that compose this
}
```

A lens for first name can then be defined as such:

```scala
val aLens = Lens[Name,Option[String]](
	_.firstName, 
	(o, value) => o.copy(firstName = value))
```

So, you provide two functions: a getter and a setter.

```scala
aLens.get(listOfPersons(1))
res: Option[String] = Some(Bar)

aLens.set(listOfPersons(1), Some("Barby"))
res: Name = Name(Some(Bar Foo),Some(Barby),Some(Foo))
```

In this case the usage of a lens is almost trivial because using the copy method on a class is an easy thing to do. But when you start to nest classes to create a more complicated model, multiple copy calls are required. Lenses are a good alternative in that case.


## Bullet Proof Reading of Data Sources

The foundation of the bullet proof approach thus far clearly is the `Option` type, aka the `Maybe` Monad in Haskell. We already used `Try` to catch exceptions in a user-friendly and safe way.

Using `Try` while reading a file allows us to cope with missing values, columns or when transforming numbers encoded in strings to integers or floating point numbers. In every case, we have the option to cast the possible exceptions to `None` (missing value) or a default value.


## Bullet Proof Aggregation of Data Sources

As mentioned already it is seldom the case that all data is available from one input file/database. Sometimes additional annotations need to be added (horizontal aggregation), coming from a different source. Sometimes, more data should be added which lacks certain features that the already parsed data contains (vertical aggregation).

There are several approaches to this. One is to go from one class-representation to another. But in this case, classes should be closely matched to the source of the data. We use a different approach, also making use of the (... tada! ...) `Option` type. 

Since a) the data ready for analytics should be in denormalized form, and b) we already have a model for that data that is able to cope with missing values, it is not hard to start from the data source that contains the most information about the denormalized form of the data. All fields/features that are not available in this first data source remain `None` (aka the default).

Adding additional features later can easily be done by _updating_ the features from `None` to `Some(...)`[^1]. Adding additional data vertically can be done in the same way. It's perfectly fine to end up with a data structure where most of the rows have `None` for a certain feature but some contain more information. And since our transformations are bullet proof, all runs safe.


[^1]: This even reads nice!


# Summary

To summarize:

- Start out with the object model that would be used when all available would be loaded 
- Use `Option` types for _all_ fields in order to 
- Use default values `None` for data that is only later to be processed or loaded
- Use the Monadic property of the `Option` type for easy manipulation
- Use `Try` in combination with `Option`s for safe reading and transformation of data
- From beginning to end, work with the same data model (using case classes) and fill in the blanks by updating `None` to `Some(...)`.

... and of course ...

- Update the data model, transformations, aggregations, etc. whenever necessary

- - -




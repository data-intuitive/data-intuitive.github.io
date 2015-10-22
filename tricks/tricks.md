

## Bash

Delete files from a certain age

```bash
find . -mtime +20 -type f -delete
```

When directories _and_ files need to be deleted, use this instead:

```bash
find . -mtime +20 -type d -type f -delete
```

This in fact means putting AND between the two types. The following is _better_:

```bash
find . -mtime +20 -type f -o -type d -delete
```


## Jekyll

Testing a Jekyll site locally and making it available via Github by pushing it to the git repo _without_ making any configuration changes is a pleasure. But it's not very easy to do that. I found the following trick to work very well.

Make two config files, one global one (which works for Github pages) and one which overrides the appropriate settings for a local deploy.

I have the following files: `_config.yaml` and `_config_local.yaml`. In `config.yaml`, I have the following line:

    url:                  'http://www.data-intuitive.com'

In `_config_local.yaml`, this setting is overriden:

    url:    'http://localhost:4000'

Locally, Jekyll can then be started like this:

    jekyll serve -w --config _config.yaml,_config_local.yaml


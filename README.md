# RZ AOSP Documentation

This is a documentation sources for [rz_aosp](https://renesas-rz.github.io/rz_aosp) website (github.io).

## Prepare environment

Python3 and pip3 are required.

In some case you may need to make a `symlink` to pip (of python3).

### Create a virtual environment (optional but recommended)
```
python3 -m venv venv && source venv/bin/activate
```

### Setup from script

Working directory should be `rz_aosp`.

```
. work/setup.sh
```

### Serve local server

Working directory should be `rz_aosp`.

```
. serve.sh
```

## Test versioning with `mike`

Working directory should be `rz_aosp`.

### Deploy

This will generate a static website into `local/gh-pages` branch.

`dev` will be used as version.

```
. mike/deploy.sh
```

### Serve

You must deploy first.

```
. mike/serve.sh
```

### Clean-up

This step is not mandatory.

After you complete checking your website, you may want to remove `local/gh-pages` branch.

```
. mike/remove.sh
```

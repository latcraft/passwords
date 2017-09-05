
# Latcraft password repository

This repository is encrypted via <https://github.com/elasticdog/transcrypt>. Don't try to hack, you, silly cat.

# Quick guide to installing `transcrypt`

## On Linux

To install the `transcrypt` utility, do the following in some directory on your system (e.g. `/usr/lib`):

    $ sudo git clone https://github.com/elasticdog/transcrypt.git
    $ cd transcrypt/
    $ sudo ln -s ${PWD}/transcrypt /usr/local/bin/transcrypt

## On MacOS

Just use `brew`:

    $ brew install transcrypt 

## On Windows

You can use Cygwin and follow Linux installation instructions, or you can add hooks to your repository manually.

## Adding hooks manually

After you cloned the password repository, you have to modify the `.git/config` file by adding the following snipet (dots in the `password` field should be replaced with real password, if you know it, of course):

```
[transcrypt]
	version = 0.9.6
	cipher = aes-256-cbc
	password = ..............
[filter "crypt"]
	clean = \"$(git rev-parse --show-toplevel)\"/.git/crypt/clean %f
	smudge = \"$(git rev-parse --show-toplevel)\"/.git/crypt/smudge
[diff "crypt"]
	textconv = \"$(git rev-parse --show-toplevel)\"/.git/crypt/textconv
[merge]
	renormalize = true
[alias]
	ls-crypt = "!git ls-files | git check-attr --stdin filter | awk 'BEGIN { FS = \":\" }; /crypt$/{ print $1 }'"
```

After that, copy scripts from this repository into the `.git/config` directory:

   - `transcrypt/crypt/clean` > `.git/config/clean`
   - `transcrypt/crypt/smudge` > `.git/config/smudge`
   - `transcrypt/crypt/textconv` > `.git/config/textconv`

It is expected that the `openssl` executable is available on your `PATH`.



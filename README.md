python-novice-inflammation
==========================

Introduction to Python for non-programmers using inflammation data.

> Please see [https://github.com/swcarpentry/lesson-example](https://github.com/swcarpentry/lesson-example)
> for instructions on formatting, building, and submitting lessons,
> or run `make` in this directory for a list of helpful commands.


## Dependencies

In order build the `.html` files from the `.md` files, ensure you have the
following dependencies installed.

### Pandoc

`pandoc` is a program that converts documents between formats (e.g. `.md` to
`.html` and vice-versa). The official installation instructions can be found
[here][pandoc-install]. On Ubuntu, `pandoc` can be installed from the
command-line by running:
```
sudo apt-get install pandoc
```

### Python libraries

The [`requirements.txt`](requirements.txt) file contains a list of the required
Python libraries. These can be installed from the command-line using `pip`:
```
pip install -r ./requirements.txt
```


## Building the lesson files

Run the following command to build the `.html` files from the source `.md`
files:
```
make preview
```


[pandoc-install]: http://johnmacfarlane.net/pandoc/installing.html

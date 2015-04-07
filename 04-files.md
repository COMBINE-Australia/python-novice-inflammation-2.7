---
layout: page
title: Programming with Python
subtitle: Analyzing Data from Multiple Files
minutes: 20
---
> ## Learning Objectives {.objectives}
>
> *   Use a library function to get a list of filenames that match a simple wildcard pattern.
> *   Use a `for` loop to process multiple files.

We now have almost everything we need to process all our data files.
The only thing that's missing is a library with a rather unpleasant name:

~~~ {.python}
import glob
~~~

The `glob` library contains a single function, also called `glob`, that finds
files whose names match a pattern. We provide those patterns as strings: the
character `*` matches zero or more characters, while `?` matches any one
character.

We can use `glob` to get the names of all our CSV files:

~~~ {.python}
glob.glob('data/*.csv')
~~~

~~~ {.output}
['data/inflammation-09.csv',
 'data/small-03.csv',
 'data/inflammation-11.csv',
 'data/inflammation-07.csv',
 'data/inflammation-10.csv',
 'data/inflammation-01.csv',
 'data/inflammation-12.csv',
 'data/small-02.csv',
 'data/inflammation-03.csv',
 'data/inflammation-05.csv',
 'data/inflammation-06.csv',
 'data/inflammation-04.csv',
 'data/inflammation-08.csv',
 'data/inflammation-02.csv',
 'data/small-01.csv']
~~~

using `?`, we can get a subset of inflammation CSV files:

~~~ {.python}
glob.glob('data/inflammation-0?.csv')
~~~

~~~ {.output}
['data/inflammation-09.csv',
 'data/inflammation-07.csv',
 'data/inflammation-01.csv',
 'data/inflammation-03.csv',
 'data/inflammation-05.csv',
 'data/inflammation-06.csv',
 'data/inflammation-04.csv',
 'data/inflammation-08.csv',
 'data/inflammation-02.csv']
~~~

the `sorted` function can then be used to sort the list in
[lexicographic](http://en.wikipedia.org/wiki/Lexicographical_order) order:

~~~ {.python}
sorted(glob.glob('data/inflammation-*.csv'))
~~~

~~~ {.output}
['data/inflammation-01.csv',
 'data/inflammation-02.csv',
 'data/inflammation-03.csv',
 'data/inflammation-04.csv',
 'data/inflammation-05.csv',
 'data/inflammation-06.csv',
 'data/inflammation-07.csv',
 'data/inflammation-08.csv',
 'data/inflammation-09.csv',
 'data/inflammation-10.csv',
 'data/inflammation-11.csv',
 'data/inflammation-12.csv']
~~~

We can now generate plots of the inflammation data by looping over a list of
their filenames. Let's do this for the first three inflammation CSV files:

~~~ {.python}
filenames = sorted(glob.glob('data/inflammation-*.csv'))
filenames = filenames[:3]
for f in filenames:
    print f

    data = np.loadtxt(fname=f, delimiter=',')
    fig = plt.figure(figsize=(10.0, 3.0))

    axes1 = fig.add_subplot(1, 3, 1)
    axes2 = fig.add_subplot(1, 3, 2)
    axes3 = fig.add_subplot(1, 3, 3)

    axes1.set_ylabel('average')
    axes1.plot(data.mean(axis=0))

    axes2.set_ylabel('max')
    axes2.plot(data.max(axis=0))

    axes3.set_ylabel('min')
    axes3.plot(data.min(axis=0))

    fig.tight_layout()
    plt.show(fig)
~~~

which produces the following:

~~~ {.output}
inflammation-01.csv
~~~

![Analysis of inflammation-01.csv](fig/03-loop_49_1.png)\


~~~ {.output}
inflammation-02.csv
~~~

![Analysis of inflammation-02.csv](fig/03-loop_49_3.png)\


~~~ {.output}
inflammation-03.csv
~~~

![Analysis of inflammation-03.csv](fig/03-loop_49_5.png)\

Sure enough,
the maxima of the first two data sets show exactly the same ramp as the first,
and their minima show the same staircase structure;
a different situation has been revealed in the third dataset,
where the maxima are a bit less regular, but the minima are consistently zero.

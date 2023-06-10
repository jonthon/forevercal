# ForeverCal


NAME:
-----

```forevercal```, named to briefly describe its main functionality, determine the weekday of any given date; hence, its named forevercal after forever calendar.


MOTIVE:
-------

The main motive of this module is to improve explicitness from the built-in python weekday interface (```calendar.weekday```). 

Python weekday hardcodes its index => weekday mapper: 0 => 'Mon', 1 => 'Tue', 2 => 'Wed', ... etc. Compared to this module, that mapper is True for genesis date 1/1/1. However, this module offers more flexibility to specify a custom genesis date (Yes, even today) with args ```(y, m, d, weekday)``` to ```*Date``` interfaces. The genesis date derives a new mapper that's compatible with any specified subject date (even earlier than the genesis date).


DESCRIPTION:
------------

This module implements an algorithm for determining the weekday (Sun, Mon, Tue, ... etc) of any date given a known weekday of a prime date (genesis date). The algorithm was developed by the author of this module from scratch and tested locally, see the ```tests.py``` file and top level code in this file.

```Presentable*``` classes are the recommended interfaces to use because they are the highest level interfaces, easy to use, and follow a simplicity approach. They are also reusable to various front ends: console, GUI, Web, ... etc. They define ```__str__``` for printing. ```Presentable*``` month and year interfaces define ```__iter__``` which makes them iterable, yielding weeks on demand. Ideal for use in GUI and Web frontends since ```__str__``` may not be suitable.

Values passed to the year, month, and date interfaces of this module are validated. For instance, invalid year, month, and day values raise ```OutOfRange``` instances if they are out of expected range (see their respective classes code for implementation). However, users should remember to handle these errors for better flow management. 


USAGE:
------

This module can be imported just like any other python module with no dependencies, or can be run as a top level file and get specific output depending on the CLI argument specified (-y yearnum, -m monthnum, -d daynum). Run ```python forevercal.py -h``` for help on top level script usage.

EXAMPLES:
--------
- `PresentableGregorian` interface (`Presentable*` are similar). Output is cut short for space.

```
jon@jons-linux:~/wanangu/lib/forevercal$ python3 -q
>>> import forevercal as cal
>>> 
>>> # (01/01/2023) => 'Sunday'
>>> y = cal.PresentableGregorian(2023, day1_weekday='Sunday')
>>> print(y)
            2023
          January
Sun Mon Tue Wed Thu Fri Sat
 1   2   3   4   5   6   7 
 8   9   10  11  12  13  14
 15  16  17  18  19  20  21
 22  23  24  25  26  27  28
 29  30  31                

          February
Sun Mon Tue Wed Thu Fri Sat
             1   2   3   4 
 5   6   7   8   9   10  11
 12  13  14  15  16  17  18
 19  20  21  22  23  24  25
 26  27  28                

          March
Sun Mon Tue Wed Thu Fri Sat
             1   2   3   4 
 5   6   7   8   9   10  11
 12  13  14  15  16  17  18
 19  20  21  22  23  24  25
 26  27  28  29  30  31    

          April
Sun Mon Tue Wed Thu Fri Sat
                         1 
 2   3   4   5   6   7   8 
 9   10  11  12  13  14  15
 16  17  18  19  20  21  22
 23  24  25  26  27  28  29
 30                        

          May  
Sun Mon Tue Wed Thu Fri Sat
     1   2   3   4   5   6 
 7   8   9   10  11  12  13
 14  15  16  17  18  19  20
 21  22  23  24  25  26  27
 28  29  30  31            

          June 
Sun Mon Tue Wed Thu Fri Sat
                 1   2   3 
 4   5   6   7   8   9   10
 11  12  13  14  15  16  17
 18  19  20  21  22  23  24
 25  26  27  28  29  30    

          July 
Sun Mon Tue Wed Thu Fri Sat
                         1 
 2   3   4   5   6   7   8 
 9   10  11  12  13  14  15
 16  17  18  19  20  21  22
 23  24  25  26  27  28  29
 30  31                    

          August
Sun Mon Tue Wed Thu Fri Sat
         1   2   3   4   5 
 6   7   8   9   10  11  12
 13  14  15  16  17  18  19
 20  21  22  23  24  25  26
 27  28  29  30  31        

          September
Sun Mon Tue Wed Thu Fri Sat
                     1   2 
 3   4   5   6   7   8   9 
 10  11  12  13  14  15  16
 17  18  19  20  21  22  23
 24  25  26  27  28  29  30

          October
Sun Mon Tue Wed Thu Fri Sat
 1   2   3   4   5   6   7 
 8   9   10  11  12  13  14
 15  16  17  18  19  20  21
 22  23  24  25  26  27  28
 29  30  31                

          November
Sun Mon Tue Wed Thu Fri Sat
             1   2   3   4 
 5   6   7   8   9   10  11
 12  13  14  15  16  17  18
 19  20  21  22  23  24  25
 26  27  28  29  30        

          December
Sun Mon Tue Wed Thu Fri Sat
                     1   2 
 3   4   5   6   7   8   9 
 10  11  12  13  14  15  16
 17  18  19  20  21  22  23
 24  25  26  27  28  29  30
 31                        


>>> 
```


- `PresentableMonth` interface

```
on@jons-linux:~$ python3 -q
>>> import forevercal as cal
>>> 
>>> # month=June, year=2023 => common year, (06/01/2023) => 'Thursday'
>>> m = cal.PresentableMonth(6, is_yr_leap=False, day1_weekday='Thursday')
>>> print(m)
          June 
Sun Mon Tue Wed Thu Fri Sat
                 1   2   3 
 4   5   6   7   8   9   10
 11  12  13  14  15  16  17
 18  19  20  21  22  23  24
 25  26  27  28  29  30    


>>> 
>>> 
```


TBD:
----

Hybrid interfaces that imply both the Julian and Gregorian calendar features (ideal for per country calendars which have transitioned from one form to another).

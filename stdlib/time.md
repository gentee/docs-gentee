---
nav: toc
---

# Time

Operators and functions for working with date and time \(**time** type\) are described here.

* [int\( time t \) int](time.md#int-time-t-int)
* [time\( int unixtime \) time](time.md#time-int-unixtime-time)
* [AddHours\( time t, int hours \) time](time.md#addhours-time-t-int-hours-time)
* [Date\( int year month day \) time](time.md#date-int-year-month-day-time)
* [DateTime\( int year month day hour minute second \) time](time.md#datetime-int-year-month-day-hour-minute-second-time)
* [Days\( time t \) int](time.md#days-time-t-int)
* [Format\( str layout, time t \) str](time.md#format-str-layout-time-t-str)
* [Now\( \) time](time.md#now-time)
* [ParseTime\( str layout, str value \) time](time.md#parsetime-str-layout-str-value-time)
* [UTC\( time t \) time](time.md#utc-time-t-time)
* [Weekday\( time t \) int](time.md#weekday-time-t-int)
* [YearDay\( time t \) int](time.md#yearday-time-t-int)

## Types

### time

The _time_ type has the following fields:

* **int Year** - year
* **int Month** - month
* **int Day** - day of month
* **int Hour** - hour
* **int Minute** - minute
* **int Second** - second
* **bool UTC** - if it is _true_, then it is UTC time, otherwise it is local time.

## Operators

| Operator | Result | Description |
| :--- | :--- | :--- |
| time **==** time | bool | Returns _true_ if the two time values are equal and _false_, otherwise. |
| time **&gt;** time | bool | Returns _true_ if the first time is greater than the second and _false_, otherwise. |
| time **&lt;** time | bool | Returns _true_ if the first time is less than the second and _false_, otherwise. |
| time **!=** time | bool | Returns _true_ if the two time values are not equal and _false_, otherwise. |
| time **&gt;=** time | bool | Returns _true_ if the first time is greater than or equal to the second and _false_, otherwise. |
| time **&lt;=** time | bool | Returns _true_ if the first time is less than or equal to the second and _false_, otherwise. |
| time **=** time | time | Assignment operator. |

## Functions

### int\(time t\) int

The _int_ function converts _time_ value to a Unix time, the number of seconds elapsed since January 1, 1970 UTC and returns it.

### time\(int unixtime\) time

The _time_ function converts the given Unix time, sec seconds since January 1, 1970 UTC to _time_ structure and returns it.

### AddHours\(time t, int hours\) time

The _AddHours_ function returns the time corresponding to adding the given number of hours to _t_. The _hours_ parameter can be negative.

### Date\(int year month day\) time

The _Date_ function returns a structure of the _time_ type with the specified date.

### DateTime\(int year month day hour minute second\) time

The _DateTime_ function returns the _time_ structure as local time. Also, you can initialize a time variable like this

```text
time t = {Year: 2018, Month: 12, Day: 12}
```

### Days\(time t\) int

The _Days_ function returns the number of days in the month in which the specified time is located.

### Format\(str layout, time t\) str

The _Format_ function returns a textual representation of the time value formatted according to layout. It takes a string of tokens and replaces them with their corresponding values.

|  | Token | Output |
| :--- | :--- | :--- |
| **Year** | YYYY | 2019 |
|  | YY | 19 |
| **Month** | MMMM | January |
|  | MMM | Jan |
|  | MM | 01..12 |
|  | M | 1..12 |
| **Day** | DD | 01..31 |
|  | D | 1..31 |
| **Day of Week** | dddd | Monday |
|  | ddd | Mon |
| **AM/PM** | PM | AM PM |
|  | pm | am pm |
| **Hour** | HH | 00..23 |
|  | hh | 01..12 |
|  | h | 1..12 |
| **Minute** | mm | 00..59 |
|  | m | 1..59 |
| **Second** | ss | 00..59 |
|  | s | 1..59 |
| **Time Zone** | tz | MST |
|  | zz | -0700 ... +0700 |
|  | z | -07:00 ... +07:00 |

### Now\(\) time

The _Now_ function returns the current local time.

### ParseTime\(str layout, str value\) time

The _ParseTime_ function parses a formatted string and returns the time value it represents. The list of layout tokens is the same as in **Format** function.

```text
run str {
  time t &= ParseTime(`MMM D, YYYY at h:mmpm (zz)`, `Jun 7, 2019 at 6:05am (+0300)`)
  time t1 &= ParseTime(`YY/MM/DD HH:mm:s`, `19/05/29 03:21:3`)
  return Format(`YY/MM/DD HH:mm:ss zz`, UTC(t)) + Format(` YY/MM/DD HH:mm:ss`, UTC(t1))
}
// 19/06/07 03:05:00 +0000 19/05/29 03:21:03
```

### UTC\(time t\) time

The _UTC_ function converts local time to UTC and returns a new time structure. If the time _t_ was already UTC, then a copy of it is returned.

### Weekday\(time t\) int

The _Weekday_ function returns the day of the week specified by _t_. 0 - Sunday, 1 - Monday etc.

### YearDay\(time t\) int

The _YearDay_ function returns the day of the year specified by _t_.


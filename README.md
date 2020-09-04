# AltSO-8601
The AltSO-8601[[4]] Standard is part of the AltSO Standards and is in particular an alternative to using ISO-8601[[7]] with a very clear and reliable benefit to those dealing with timezones and time travel. When transporting date and time along with timezone information you can be easily tricked into using the ISO-8601[[7]] Standard and become stuck in a timezone time loop where you no longer have the awareness of what the original timezone in which the transported date and time originated. ISO-8601[[7]] will lead you to believe that using its +hhmm offset will allow you to tell the receiver of your date and time information a valid means to reverse your offset back into the original date and time it was intended but this all comes undone when dealing with timezone's primary conundrum... cows and daylight savings (sometimes both). The AltSO-8601[[4]] standard allows you to pass the same date and time information in a simple string based format while also carrying the timezone that the date and time is indicative, This then allows the receiver to know that the date and time received was intended for a particular timezone and can parse the date and time as that timezone and the convert into other timezones relative to the original timezone and allowing calculations of time differences related to daylight savings.

## The Format
The final format that was settled (to be confirmed) was one that allowed for date, time, microtime and timezone, the following is a break down of the format.
```
YYYYMMDDhhmmss:REGION/CITY
```
* `YYYY` is a full four digit year, the format does not support or allow for single, double or triple digit years.
* `MM` is a double digit representation of month and must have a preceding zero for any month below ten.
* `DD` is a double digit representation of day and must have a preceding zero for any day below ten.
* `hh` is a double digit representation of hour and must have a preceding zero for any hour below ten.
* `mm` is a double digit representation of minute and must have a preceding zero for any minute below ten.
* `ss` is a double digit representation of second and must have a preceding zero for any second below ten.
* `:REGION/CITY` is the optional timezone you can add to the AltSO-8601[[4]] format for indicating the timezone in which the prceding date, time and optional microtime represents, if the timezone is to be left off the format then the date, time and microtime must be based on UTC and not attempt to be indicative of any timezone without the awareness of what timezone.
Along with the clear benefits of timezone support the format also reduced byte usage while in transport and plain storage as ISO-8601[[7]] still required dash, T and sometimes Z characters to structure it's format. AltSO-8601[[4]] does not attempt to create a recognisable format as the sender and receiving will have already agreed on the format being used and know how to parse.


## Software Implementations

### PHP Library: AlteredCarbon[[1]]
This Library which is written in PHP[[2]] is an extension on the Carbon[[3]] library and is the first software library to implement the AltSO-8601[[4]] format for date and time parsing. The PHP[[2]] Library was also added to Packagist[[5]] for use as a Composer[[6]] package.


## References

1. [Mossengine/AlteredCarbon - A PHP Library that Extends Carbon to include the AltSO-8601 format ( also allows for other extra formats not part of the Carbon Library )][1]
2. [PHP: Hypertext Preprocessor][2]
3. [Carbon: A simple PHP API extension for DateTime][3]
4. [Alternative Standards Organisation - 8601 ( DateTime and Timezone Format )][4]
5. [Packagist: The PHP Package Repository][5]
6. [Composer: Dependency Management for PHP][6]
7. [ISO 8601: Data elements and interchange formats][7]

[1]: https://github.com/Mossengine/AlteredCarbon
[2]: https://secure.php.net/
[3]: https://github.com/briannesbitt/Carbon
[4]: https://github.com/Gitapedia/AltSO-8601
[5]: https://packagist.org/
[6]: https://getcomposer.org/
[7]: https://en.wikipedia.org/wiki/ISO_8601

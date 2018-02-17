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


## Conceptual Formats
The original formats considered for AltSO-8601[[4]] were thinking about the future and not the present, something that although came from good intentions unfortunately presented chaos and needed filtering.

### @computation
This format was to also allow for inclusion of the computation number from within the cpu at the time of generating the date and time value, this was scrapped as the AltSO-8601[[4]] standard was not intended for tracking cpu computations cross timezones and deemed irrelevant.
```
YYYYMMDDhhmmss@computation:REGION/CITY
```

### AltSO-8601[[4]] +ISO-8601[[7]]
This format was an attempt to carry the offset used to generate the date and time that was then tagged for the particular timezone, the need was based on what if you wanted to know the offset from UTC that provided the date and time that was then branded with the indicative timezone. This may still be a need in the future but we are still too burned by ISO-8601[[7]] usage of the offset to care for it in this format.
```
YYYYMMDDhhmmss:REGION/CITY+hhmm
```

### Planetary Considerations
This format was the include a prefixed square bracketed area of the date and time that provided information about what planet the date and time referred to and at what radius from the centre of the planet the time was based.
```
[PLANET:RADIUS]YYYYMMDDhhmmss:REGION/CITY
```
* `PLANET` was basically the name of the planet, if planets have unique identifers then these would also be accepted in the parsing so that when we care more about millions of planets we can assign them numerical identifiers and keep this property of the date and time a little more formal and less lengthy with long named planets.
* `:RADIUS` is an optional value that if used indicates how far from the center of the planet the date and time is intended and means the parsing should consider at what rate time progresses that far from the center of the planet with respect to the planets rotation and size.

### Not This Planet
To handle rare circumstances where the indicated planet radius is exactly the same distance or closer to another plant, we included the option to indicate what planets should not be considered to take over the radius position of the date and time. This format was quickly removed as we were indicating the planet for the date and time by name but still respect that this may help in conversions to the other planets local date and time.
```
[PLANET:RADIUS!PLANET2,PLANET3]YYYYMMDDhhmmss:REGION/CITY 
```
* `!PLANET2,PLANET3` is a comma separated array of other planet names / identifiers.


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
# A cron parser

Spits out next & previous cron dates starting from now or a specific date.
Please notice that the timezone of the resulting dates are in the
same timezone provided with Cron().parse(...)

## Usage

A simple usage example:
```dart
import 'package:cron_parser/cron_parser.dart';
import 'package:timezone/timezone.dart';

main() {
  // by default next cron dates are starting from the current date
  var cronIterator = Cron().parse("0 * * * *", "Europe/London");
  TZDateTime nextDate = cronIterator.next();
  // you can retrieve the current value by using the current method
  TZDateTime currentDate = cronIterator.current(); // same as nextDate
  TZDateTime afterNextDate = cronIterator.next();

  cronIterator = Cron().parse("0 * * * *", "Europe/London");
  TZDateTime previousDate = cronIterator.previous();
  // you can retrieve the current value by using the current method
  TZDateTime currentDate = cronIterator.current(); // same as previousDate
  TZDateTime beforePreviousDate = cronIterator.previous();
}
```

Another example this time with a specific start date:
```dart
import 'package:cron_parser/cron_parser.dart';
import 'package:timezone/timezone.dart';

main() {
  TZDateTime startDate = TZDateTime(getLocation("Europe/London"), 2020, 4, 01);
  var cronIterator = Cron().parse("0 * * * *", "Europe/London", startDate);
  TZDateTime nextDate = cronIterator.next(); // 2020-04-01 01:00:00.000+0100
  TZDateTime afterNextDate = cronIterator.next(); // 2020-04-01 02:00:00.000+0100

  cronIterator = Cron().parse("0 * * * *", "Europe/London", startDate);
  TZDateTime previousDate = cronIterator.previous(); // 2020-03-31 23:00:00.000+0100
  TZDateTime beforePreviousDate = cronIterator.previous(); // 2020-03-31 22:00:00.000+0100
}
```

## Links

- [source code][source]
- contributors: [Ronny Bubke](https://github.com/rbubke), [Nils Reichardt](https://github.com/nilsreichardt)

[source]: https://github.com/rbubke/cron-parser
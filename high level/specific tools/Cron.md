Is a time-based job scheduler in Unix-like computer operating systems. Users employ this utility to schedule jobs (commands or shell scripts) to run periodically at fixed times, dates, or intervals. It typically automates system maintenance or administration—though its general-purpose nature makes it useful for things like downloading emails and other tasks.

Syntaxis:

\* \* * * *
minute, hour, day, month, day of the week

these are the special characters

- Asterisk (\*) represents all possible values for a field. For example, an asterisk in the hour field would be every hour.
- Comma (,) is used to specify a list. For instance, `1,3,5` in the day-of-week field means Mondays, Wednesdays, and Fridays.
- Hyphen (-) is used to define a range. For example, `2-4` in the day-of-the-week field means Tuesdays to Thursdays.
- Slash (/) is used to specify a step value. For instance, `*/10` in the minutes field means every ten minutes.

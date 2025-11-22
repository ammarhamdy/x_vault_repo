
# Date command

**Time mils**
```
date +%s%3N
```
`%s` → seconds since epoch (Jan 1, 1970 UTC).
`%3N` → milliseconds (3 digits of nanoseconds).
Concatenated, you get a 13-digit timestamp.

**Custom Date Formatting**
```sh
date "+%Y-%m-%d %H:%M:%S"
```
Use `+` followed by format specifiers


## Common Format Specifiers

| Specifier | Description              | Example Output |
| --------- | ------------------------ | -------------- |
| `%Y`      | Year (4 digits)          | `2025`         |
| `%m`      | Month (01-12)            | `04`           |
| `%d`      | Day of the month (01-31) | `01`           |
| `%H`      | Hour (24-hour format)    | `12`           |
| `%I`      | Hour (12-hour format)    | `12`           |
| `%M`      | Minutes (00-59)          | `34`           |
| `%S`      | Seconds (00-59)          | `56`           |
| `%p`      | AM/PM                    | `PM`           |
| `%A`      | Full weekday name        | `Monday`       |
| `%B`      | Full month name          | `April`        |

**Convert a Timestamp to Human-Readable Date**
```
date -d @1741161296
```
**`-d` or `--date`** → Allows setting a custom date instead of the current system date.
**`@1741161296`** → The `@` symbol tells `date` to interpret `1741161296` as a Unix timestamp.

**Display a Date in the Future or Past**
```sh
date --date="yesterday"
```

```sh
date --date="next week"
```

```sh
date --date="10 days"
```



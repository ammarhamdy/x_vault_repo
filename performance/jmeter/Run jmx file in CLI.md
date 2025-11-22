
# Basic Command:
```bash
jmeter -n -t <path-to-test-file.jmx> -l <path-to-results-file.jtl>
```
- `-n` → Non-GUI mode (needed for command line)
- `-t` → Path to your `.jmx` test plan
- `-l` → Path where the result log (e.g. `.jtl`) will be saved


# Optional Flags:
```bash
jmeter -n -t test_plan.jmx -l results.jtl -e -o /path/to/output-folder
```
- `-n` → non-GUI mode
- `-t` → path to your `.jmx` test plan file
- `-l` → log results to `results.jtl` file
- `-e` → generate HTML report after test
- `-o` → output directory for the HTML report


# Generate HTML Report from JTL
```bash
jmeter -g result.jtl -o /path/to/output/report/
```
- `-g` → Read results file    
- `-o` → Output HTML report directory


# Enable Verbose Logging
By default, JMeter logs in INFO level. 
To enable **verbose/debug-level logs**, you need to modify the logging settings.
```bash
jmeter -n -t test_plan.jmx -l results.jtl -Jlog_level.jmeter=DEBUG
```
This sets the root JMeter log level to `DEBUG`.

You can also set log levels for specific components:
```bash
-Jlog_level.jmeter.junit=DEBUG
-Jlog_level.jmeter.protocol.http=DEBUG
```

**View Logs**
By default, JMeter writes logs to `jmeter.log` in the current directory.
After your CLI test runs, inspect this file:
```bash
cat jmeter.log
```

**Example Full Command**
```bash
jmeter -n -t /path/to/test.jmx -l /path/to/results.jtl -Jlog_level.jmeter=DEBUG
```


# Output

- **Started: 100** → JMeter has initiated 100 threads (virtual users) so far.

- **Active: 96** → 96 threads are currently running (actively executing test steps).

- **Finished: 4** → 4 threads have completed their execution and exited.


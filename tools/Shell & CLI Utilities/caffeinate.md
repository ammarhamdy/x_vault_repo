# Prevent Sleep Temporarily While the Command Runs

Instead of trying to run something _while the system is asleep_, you can prevent the system from going to sleep until the command finishes.

Use `caffeinate` (macOS-like behavior, now available in Linux)

Install `caffeinate`:
```
sudo apt install caffeine
```
Then run your command like this:
```
caffeinate -i your-command
```
This prevents the system from going idle or sleeping while `your-command` is running.


----


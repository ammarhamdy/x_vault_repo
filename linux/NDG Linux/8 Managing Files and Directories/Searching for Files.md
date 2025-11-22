
```sh
find -type f | cut -d '/' -f 3 | egrep -v  -E 'mp3|txt'
```
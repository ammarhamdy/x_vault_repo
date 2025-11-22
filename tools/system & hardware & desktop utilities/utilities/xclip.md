
**copy to clipboard**
```sh
echo -n "message" | xclip -selection CLIPBOARD
```

**get from clipboard**
```sh
xclip -o
```
example:
```sh
clipboard_content=`xclip -o`
echo $clipboard_content
```

**copy file content to clip board**
```sh
xclip -sel clip < Downloads/file.txt
```




# Installation
```sh
sudo apt install gedit
```

# Download themes

```
git clone https://github.com/mig/gedit-themes.git
```

If you’re using a **new Ubuntu (22.04 or later)** with **GTK4 Gedit** (version 40+), which **changed how color schemes are stored**.

## Check your `gedit` version
```sh
gedit --version
```

## Check which `GTKSourceView` version `gedit` uses or just app themes manually 
```sh
ls /usr/share | grep gtksourceview
```

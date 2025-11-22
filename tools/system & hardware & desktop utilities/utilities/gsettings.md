

On Ubuntu (with the default **GNOME** desktop), you can use `gsettings` to control how the wallpaper image is displayed.

```sh
gsettings set org.gnome.desktop.background picture-options 'stretched'
```
Options include: 
- `none` – no picture, just background color
- `wallpaper` – tiled
- `centered` – image in the center, no scaling
- `scaled` – scale to fit, preserving aspect ratio
- `stretched` – scale to fill, ignoring aspect ratio
- `zoom` – zoom & crop to fill
- `spanned` – span across multiple monitors


**Set a new wallpaper image:**
```sh
gsettings set org.gnome.desktop.background picture-uri "file:///home/$USER/Pictures/wallpaper.jpg"
```


**Set the background color to black**
```sh
gsettings set org.gnome.desktop.background primary-color '#000000'
```
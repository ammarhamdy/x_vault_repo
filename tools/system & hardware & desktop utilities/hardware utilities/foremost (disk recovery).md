
**Best for**: File carving – recovery based on file headers (`JPEG`, `PDF`, etc.)

```bash
sudo apt install foremost
```

```bash
sudo foremost -i /dev/sdX -o /recovery/output/
```

```bash
sudo foremost -i /dev/sdX -o /recovery/output/ -t mp4
```

**List disks**
```
lsblk
```
# distrobox code

## inside your distrobox

```bash
sudo ln -s /usr/bin/distrobox-host-exec /usr/local/bin/xdg-open
```

## inside main system

```bash
/home/deck/.local/share/applications/
```

```ini
[Desktop Entry]
Name=vscode
Exec=/usr/bin/distrobox-enter -n ubuntu-22-04 -- /usr/share/code/code --open-url %U
Icon=code
Terminal=false
Type=Application
MimeType=x-scheme-handler/vscode;
```

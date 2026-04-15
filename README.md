## Quick installation

# kbled-fedora

Adaptation of [kbled](https://github.com/chememjc/kbled) for **Fedora 43** on **Machenike L18 Pro Mars Max** (and other Clevo/TUXEDO laptops).

## ✨ Features

- ✅ Custom white color `(248, 249, 255)`
- ✅ Green focus indicator `(0, 250, 0)` for Caps/Num Lock
- ✅ Systemd autostart
- ✅ Effects (wave, breathe, scan, blink, random, snake)
- ✅ NumPad hotkeys support

## 📦 Quick installation

```bash
sudo dnf install -y libhidapi-devel systemd-devel libevdev-devel gcc make git
git clone https://github.com/machenike-l18/kbled-fedora.git
cd kbled-fedora
make
sudo make install

🎮 Usage
Basic commands
bash
# Set custom white color (recommended)
kbledclient -p -1 -bl 248 249 255 -b 10

# Toggle backlight on/off
kbledclient -tog

# Enable wave effect
kbledclient -p 1

# Stop all effects
kbledclient -p -1
Effects list
Command	Effect
-p 0	Wave
-p 1	Breathe
-p 2	Scan
-p 3	Blink
-p 4	Random
-p 5	Ripple
-p 6	Snake
-p -1	No effect
Speed control
Command	Action
-s+	Increase speed
-s-	Decrease speed
-s 0	Slow
-s 1	Medium
-s 2	Fast
Brightness control
Command	Action
-b+	Increase brightness
-b-	Decrease brightness
-b 0-10	Set brightness level
⌨️ NumPad Hotkeys (KDE Setup)
Add these in System Settings → Shortcuts → Custom Shortcuts:

Shortcut	Action	Command
Ctrl + 6	Next effect	/bin/bash -c "/usr/bin/kbledclient -p+"
Ctrl + 4	Previous effect	/bin/bash -c "/usr/bin/kbledclient -p-"
Ctrl + 8	Increase speed	/bin/bash -c "/usr/bin/kbledclient -s+"
Ctrl + 2	Decrease speed	/bin/bash -c "/usr/bin/kbledclient -s-"
Ctrl + 5	Disable effect	/bin/bash -c "/usr/bin/kbledclient -p -1"
Ctrl + /	Cycle colors	/bin/bash -c "/usr/bin/kbledclient -c"
Ctrl + *	Toggle on/off	/bin/bash -c "/usr/bin/kbledclient -tog"
Ctrl + +	Brightness up	/bin/bash -c "/usr/bin/kbledclient -b+"
Ctrl + -	Brightness down	/bin/bash -c "/usr/bin/kbledclient -b-"
KB White (custom color)
Command: /bin/bash -c "/usr/bin/kbledclient -p -1 -bl 248 249 255 -b 10"

Recommended shortcut: Ctrl + Alt + W

Hardware Caps/Num Lock indicators are not controlled by -fo (applies to RGB matrix only)

🔧 Autostart (systemd)
Create /etc/systemd/system/kb-white.service:

ini
[Unit]
Description=Set keyboard white color
After=kbled.service

[Service]
Type=oneshot
ExecStart=/bin/bash -c "sleep 2 && /usr/bin/kbledclient -p -1 -bl 248 249 255 -b 10"
RemainAfterExit=yes

[Install]
WantedBy=multi-user.target
Enable:

bash
sudo systemctl daemon-reload
sudo systemctl enable --now kb-white.service
🧪 Verify installation
bash
kbledclient --dump | grep -E "Backlight|Focus|On/Off"
Expected output:

text
On/Off state: 1
Backlight (R,G,B): (248, 249, 255)
Focus (R,G,B): (0, 250, 0)
🙏 Credits
Original kbled by Michael Curtis (chememjc)
https://github.com/chememjc/kbled

📄 License
Public Domain (same as original)

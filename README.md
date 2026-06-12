# PacMatrix
Mi 1º Rising Arch Linux de Matrix y Pacman

## 🛠️ El Stack Tecnológico

| Componente | Herramienta | Detalles |
| :--- | :--- | :--- |
| **OS** | 🐧 Arch Linux | Ligero, rápido y rolling release. |
| **Window Manager** | 📐 bspwm | Tiling Window Manager. |
| **Gestor de Atajos** | ⌨️ sxhkd | `Alt+Q` para cerrar, `Super+Enter` para terminal. |
| **Terminal** | ⚡ Alacritty | Customizada como "Jose Academy" con paleta verde neón. |
| **Compositor** | 🌫️ Picom | Renderizado por software (`xrender`) para transparencias en VirtualBox. |
| **Barra de Estado** | 📊 Polybar | Tema Matrix translúcido, métricas del sistema y soporte para emojis. |
| **Shell** | 🐚 Zsh + P10k | Powerlevel10k en variante *Green/Dark*. |
| **Fuentes** | 🔤 Meslo Nerd Font & Noto Emoji | Renderizado perfecto de iconos y emojis. |

---

## 🚀 Guía de Instalación Rápida (El Speedrun Definitivo)

Si quieres replicar esta estética exacta desde un Arch Linux base, sigue estos pasos:

### 1️⃣ Paquetes Base y Fuentes
```bash
sudo pacman -Syu
sudo pacman -S zsh git curl feh alacritty picom polybar ttf-meslo-nerd noto-fonts-emoji --noconfirm
```

### 2️⃣ Fondo de Pantalla (Modo Hacker)
```bash
mkdir -p ~/wallpapers
curl -L -o ~/wallpapers/hacker-bg.jpg "https://images.unsplash.com/photo-1526374965328-7f61d4dc18c5?q=80&w=1920&auto=format&fit=crop"
feh --bg-scale ~/wallpapers/hacker-bg.jpg
echo "feh --bg-scale ~/wallpapers/hacker-bg.jpg &" >> ~/.config/bspwm/bspwmrc
```

### 3️⃣ Alacritty: Estética Matrix y Nombre Personalizado
```bash
mkdir -p ~/.config/alacritty
cat << 'EOF' > ~/.config/alacritty/alacritty.toml
[window]
title = "Jose Academy"
dynamic_title = false

[font.normal]
family = "MesloLGS Nerd Font"

[colors.primary]
background = "#050505"
foreground = "#00FF41"

[colors.normal]
black   = "#0D0208"
red     = "#FF0000"
green   = "#00FF41"
yellow  = "#FFFF00"
blue    = "#008F11"
magenta = "#FF00FF"
cyan    = "#00FFFF"
white   = "#FFFFFF"
EOF
```

### 4️⃣ Picom: Forzar Transparencias (Fix para Máquinas Virtuales)
Alacritty pierde su capacidad de transparencia si la máquina virtual no tiene aceleración 3D. Picom lo soluciona forzándolo por software:
```bash
mkdir -p ~/.config/picom
cat << 'EOF' > ~/.config/picom/picom.conf
backend = "xrender";
opacity-rule = [
    "85:class_g = 'Alacritty'"
];
EOF
echo "picom -b --config ~/.config/picom/picom.conf &" >> ~/.config/bspwm/bspwmrc
```

### 5️⃣ Polybar: Centro de Mando Matrix
```bash
mkdir -p ~/.config/polybar
cat << 'EOF' > ~/.config/polybar/config.ini
[colors]
background = #AA000000
foreground = #00FF41
primary = #008F11
alert = #FF0000
disabled = #003B00

[bar/example]
width = 100%
height = 24pt
background = ${colors.background}
foreground = ${colors.foreground}
border-bottom-size = 2pt
border-bottom-color = ${colors.primary}
padding-left = 1
padding-right = 1
module-margin = 1

font-0 = "MesloLGS Nerd Font:size=11;2"
font-1 = "MesloLGS Nerd Font:size=14;3"
font-2 = "Noto Color Emoji:scale=10;3"

modules-left = xworkspaces xwindow
modules-right = memory cpu date

[module/xworkspaces]
type = internal/xworkspaces
label-active = %name%
label-active-background = ${colors.primary}
label-active-foreground = #000000
label-active-padding = 2
label-occupied = %name%
label-occupied-padding = 2
label-occupied-foreground = ${colors.foreground}

[module/xwindow]
type = internal/xwindow
label = 💻 %title:0:40:...%

[module/memory]
type = internal/memory
interval = 2
label = 🧠 %percentage_used%%

[module/cpu]
type = internal/cpu
interval = 2
label = ⚡ %percentage%%

[module/date]
type = internal/date
interval = 1
date = 🕒 %H:%M
label = %date%
label-foreground = ${colors.foreground}
EOF

# Script de lanzamiento seguro
cat << 'EOF' > ~/.config/polybar/launch.sh
#!/usr/bin/env bash
killall -q polybar
while pgrep -u $UID -x polybar >/dev/null; do sleep 1; done
polybar example >/dev/null 2>&1 & disown
EOF
chmod +x ~/.config/polybar/launch.sh
echo "~/.config/polybar/launch.sh &" >> ~/.config/bspwm/bspwmrc
```

### 6️⃣ Zsh & Powerlevel10k
```bash
git clone --depth=1 https://github.com/romkatv/powerlevel10k.git ~/powerlevel10k
echo 'source ~/powerlevel10k/powerlevel10k.zsh-theme' >> ~/.zshrc
sudo chsh -s /usr/bin/zsh $USER
```
*(Reinicia o lanza `zsh` para completar el asistente visual P10k).*

---


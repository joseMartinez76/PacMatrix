# PacMatrix
Mi 1º Rising Arch Linux de Matrix y Pacman

## 📥 Guía de Instalación Rápida

### 1️⃣ Paquetes Base y Fuentes
```bash
sudo pacman -Syu
sudo pacman -S zsh git curl feh alacritty picom polybar rofi firefox ttf-meslo-nerd noto-fonts-emoji noto-fonts-cjk --noconfirm
```

### 2️⃣ Estética del Sistema (Configuración General)
- **Pac-Man Hacker:** Edita `/etc/pacman.conf` y añade `ILoveCandy` debajo de la línea `Color`.
- **Fondos de pantalla:** Usa `feh --bg-scale ~/wallpapers/nombre.jpg`.

### 3️⃣ Login Manager (LightDM) oscuro
Para eliminar la pantalla blanca al iniciar sesión:
1. Copia tu fondo a `/usr/share/pixmaps/fondo-login.jpg`.
2. Edita `/etc/lightdm/lightdm-gtk-greeter.conf`:
```ini
[greeter]
background = /usr/share/pixmaps/fondo-login.jpg
theme-name = Adwaita-dark
font-name = MesloLGS Nerd Font 11
```
3. Reinicia el servicio: `sudo systemctl restart lightdm`.

### 4️⃣ Escritorios Virtuales (Estilo Kanji)
En `~/.config/bspwm/bspwmrc`, define tus escritorios con carácteres japoneses para un look 100% Cyberpunk:
```bash
bspc monitor -d 影 網 刃 龍 雷 空 魂 鬼 闇 鋼
```

---


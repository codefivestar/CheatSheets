# 📘 Ubuntu - Cheat Sheet

## 🧩 Sistema y Hardware
```
lsb_release -a           # Muestra la versión de Ubuntu
uname -a                 # Detalles del kernel y arquitectura
hostnamectl              # Información del sistema
lscpu                    # Info del CPU
lsblk                    # Listar dispositivos de bloque (discos)
df -h                    # Espacio en disco
free -h                  # Uso de RAM y SWAP
uptime                   # Tiempo encendido y carga del sistema
top                      # Procesos activos
htop                     # Vista interactiva de procesos (requiere instalación)
```

## 🧹 Mantenimiento del Sistema
```
sudo apt update                        # Actualizar índices de paquetes
sudo apt upgrade                       # Actualizar paquetes instalados
sudo apt full-upgrade                  # Como upgrade, pero elimina dependencias obsoletas
sudo apt autoremove                    # Eliminar paquetes innecesarios
sudo apt autoclean                     # Limpiar paquetes descargados sin usar
sudo dpkg --configure -a               # Reparar instalaciones interrumpidas
```

## 📦 Gestión de Paquetes
```
sudo apt install <paquete>             # Instalar paquete
sudo apt remove <paquete>              # Eliminar paquete
sudo apt purge <paquete>               # Eliminar paquete + archivos de configuración
apt list --installed                   # Listar paquetes instalados
apt search <nombre>                    # Buscar paquete
dpkg -l | grep <nombre>                # Ver si un paquete está instalado
```

## 🔐 Usuarios y Permisos
```
whoami                                 # Usuario actual
id                                     # UID, GID y grupos
sudo adduser <usuario>                 # Crear usuario
sudo deluser <usuario>                 # Eliminar usuario
sudo usermod -aG sudo <usuario>        # Agregar usuario al grupo sudo
chmod +x archivo.sh                    # Hacer ejecutable
chown usuario:grupo archivo            # Cambiar propietario
```

## 🌐 Red
```
ip a                                   # Mostrar IPs de red
ping google.com                        # Verificar conectividad
nmcli device status                    # Ver estado de red
sudo systemctl restart NetworkManager  # Reiniciar red
netstat -tulnp                         # Ver puertos abiertos (requiere net-tools)
curl ifconfig.me                       # Ver IP pública
```

## 🛠️ Gestión de Servicios
```
systemctl status <servicio>           # Ver estado del servicio
sudo systemctl start <servicio>       # Iniciar servicio
sudo systemctl stop <servicio>        # Detener servicio
sudo systemctl restart <servicio>     # Reiniciar servicio
sudo systemctl enable <servicio>      # Activar en arranque
sudo systemctl disable <servicio>     # Desactivar en arranque
```

## 🧰 Utilidades del Día a Día
```
history                                # Historial de comandos
alias actualizar='sudo apt update && sudo apt upgrade'  # Crear alias
nano archivo.txt                       # Editor básico
cat archivo.txt                        # Mostrar contenido
less archivo.txt                       # Visualizar con paginado
grep "cadena" archivo                  # Buscar texto
find /ruta -name "*.log"               # Buscar archivos por nombre
```

## 📦 Snap y Flatpak
```
snap list                              # Listar paquetes snap
snap install <paquete>                 # Instalar desde Snap
flatpak list                           # Listar Flatpak
flatpak install flathub <paquete>      # Instalar desde Flathub
```

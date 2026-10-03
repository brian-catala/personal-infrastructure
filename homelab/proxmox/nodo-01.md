Node 01: proxmox-01 (HP ProDesk 600 G1)
1. Node Overview
Detalle operativo del nodo principal que soporta el clúster/homelab de Proxmox VE.

Hostname: homelab

Rol: Hipervisor Principal (Standalone / Node 1)

Ubicación Física: Homelab - Rack / Escritorio

Estado: 🟢 Operativo

2. Hardware Inventory
Especificaciones físicas del equipo y componentes instalados:

Chasis: HP ProDesk 600 G1 Small Form Factor (SFF)

CPU: Intel Celeron G1840 (2 núcleos, 2 hilos @ 2.80 GHz)

Memoria RAM: 28 GiB DDR3 (Configuración de módulos mixtos)

Almacenamiento:

Disco 0: 256 GB SSD (Proxmox OS, root, swap y LVM-thin local-lvm)

Disco 1: 4 TB HDD (Almacenamiento de datos, directorio local-hdd / NAS storage)

Red: Tarjeta integrada Intel I217-LM Gigabit Ethernet

3. Hypervisor & Software Stack
OS Base: Debian GNU/Linux (base de Proxmox)

Proxmox VE Version: 9.2.2

Kernel Version: 7.0.2-6-pve

Virtualización por Hardware: Habilitada (Intel VT-x en BIOS)

4. Storage Configuration
Cómo está repartido el espacio a nivel de Proxmox en este nodo:

Storage ID	Tipo	Dispositivo físico / Pool	Propósito
local	Directory	256 GB SSD (Partition)	ISOs, contenedores LXC templates, snippets
local-lvm	LVM-Thin	256 GB SSD (LVM Pool)	Discos virtuales (VM disks y Rootfs de LXC)
homelab-data	Directory	4 TB HDD	Datos persistentes, multimedia, backups y recursos compartidos
5. Network Configuration (Host Level)
Configuración general de interfaces de red del nodo (omitiendo IPs y MACs reales por seguridad):

Interface Bridge: vmbr0 vinculado a la interfaz física principal para el tráfico de las VMs/LXCs.

IP de Gestión: 192.168.x.x

6. Guest VMs & Containers Inventory
Listado de los invitados que corren (o correrán) en este nodo:

VM/CT ID	Nombre	Tipo	OS / Stack	Estado
100	jellyfin	LXC / VM	Linux / Jellyfin	🔵 Planificado
101	vaultwarden	LXC / VM	Docker / Vaultwarden	🔵 Planificado
102	nas-server	VM	OpenMediaVault / TrueNAS	🔵 Planificado

7. Maintenance & Notes

BIOS / Firmware: Actualizado a la última versión disponible para el HP G1.

Control de energía: Configurado para encendido automático tras fallo de corriente (AC Power Recovery -> On) en la BIOS.

Próximas tareas:

Configurar las alertas por correo/webhook desde Proxmox.

Definir la tarea de respaldo automática con Proxmox Backup Server o VZDump hacia el HDD de 4TB o red externa.

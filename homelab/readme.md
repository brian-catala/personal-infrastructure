Homelab
1. Overview
Este directorio documenta el despliegue y la configuración de mi homelab dentro del repositorio de infraestructura personal. El objetivo es mantener un entorno autohospedado para el desarrollo de servicios, gestión de almacenamiento, experimentación con virtualización y validación continua de configuraciones en Linux, redes y seguridad.

2. Architecture
El homelab corre sobre un nodo único basado en hardware reutilizado que opera Proxmox VE.

HOMELAB
                            │
                     HP ProDesk 600 G1
                            │
                     Proxmox VE 9.2.2
                            │
              ┌─────────────┴─────────────┐
              │                           │
       System Storage               Data Storage
          256 GB SSD                  4 TB HDD
              │                           │
        Proxmox / VMs                Homelab Data
              │
       ┌──────┼──────────────┐
       │      │              │
    Jellyfin Vaultwarden     NAS

    3. Infrastructure (Proxmox Host)
El hipervisor está montado sobre un equipo de factor de forma reducido (SFF) reacondicionado para tareas de laboratorio continuo.

Especificaciones de Hardware y Software
Fabricante: HP

Modelo: ProDesk 600 G1 SFF

CPU: Intel Celeron G1840 @ 2.80 GHz (x86_64, 2 Cores / 2 Threads)

Virtualización: Intel VT-x

RAM: 28 GiB

Almacenamiento OS: SSD 256 GB

Almacenamiento Datos: HDD 4 TB

Hipervisor: Proxmox VE 9.2.2

Kernel: 7.0.2-6-pve

4. Storage Layout
El diseño de almacenamiento separa estrictamente el plano del hipervisor de los volúmenes persistentes de datos.

Plaintext
                    Homelab Storage
                          │
             ┌────────────┴────────────┐
             │                         │
          256 GB SSD                4 TB HDD
             │                         │
      System / VM Storage          Data Storage
             │                         │
       ┌─────┴─────┐                   │
       │           │                   │
    Proxmox     Local-LVM          Homelab Data
System Storage (SSD de 256 GB)
Destinado al sistema operativo base y al provisionamiento rápido de invitados:

Partición raíz y swap de Proxmox.

Almacenamiento local para ISOs y templates.

Pool LVM-thin (local-lvm) para discos virtuales de VMs y contenedores LXC.

Data Storage (HDD de 4 TB)
Configurado como un storage tipo Directory en Proxmox para albergar volúmenes de mayor capacidad y persistencia:

Volúmenes de datos para contenedores/VMs.

Repositorio multimedia.

Staging para backups y recursos compartidos del NAS.

5. Services Pipeline
Servicios planeados y en ejecución dentro del clúster:

Jellyfin
Función: Servidor de medios y streaming.

Consideraciones: Monitorear el impacto en CPU del Celeron G1840 ante tareas concurrentes de transcodificación.

Vaultwarden
Función: Gestor de contraseñas compatible con Bitwarden.

Consideraciones: Requiere segmentación estricta de red, políticas de acceso por IP y rutinas de backup automatizadas. Ningún secreto o credencial real se versiona en este repositorio.

NAS
Función: Almacenamiento centralizado montado sobre el HDD de 4 TB para exportar recursos vía NFS/SMB hacia otros nodos del lab.

6. Networking
La conectividad del homelab depende del firewall/router central (MikroTik).

La segmentación por VLANs y las reglas de filtrado de tráfico se gestionan de forma centralizada y se documentan en el directorio network/.

7. Security Baseline
Segmentación: Aislamiento de tráfico mediante VLANs para contener posibles brechas.

Principio de menor privilegio: Acceso administrativo limitado a subredes de gestión específicas.

Exposición mínima: Servicios internos sin NAT hacia internet de forma directa.

Resiliencia: Backups independientes del almacenamiento primario.

8. Status & Roadmap
Fase 1 — Core Infrastructure
[x] Provisión de hardware y limpieza física.

[x] Instalación de Proxmox VE 9.2.2.

[x] Configuración de pools de almacenamiento (LVM-thin + Directory).

[x] Validación de extensiones de virtualización (VT-x).

[ ] Despliegue de red virtual e interfaces de gestión.

[ ] Implementación de servicios base (Jellyfin, Vaultwarden, NAS).

[ ] Automatización de respaldos (Proxmox Backup Server / VZDump).

9. Repository Layout

homelab/
│
├── README.md
│
├── proxmox/
│   ├── README.md
│   └── node-01.md
│
├── services/
│   ├── jellyfin/
│   ├── vaultwarden/
│   └── nas/
│
├── storage/
├── backups/
└── monitoring/

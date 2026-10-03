# Personal Infrastructure

> Infraestructura personal orientada a **Homelab, SOC Lab, virtualización, redes y ciberseguridad**.

Este repositorio documenta el diseño, implementación y evolución de mi infraestructura personal.

El proyecto combina una infraestructura de servicios personales (**Homelab**) con un entorno de aprendizaje y experimentación en ciberseguridad (**SOC Lab**), utilizando virtualización, segmentación de red, monitorización y diferentes herramientas de seguridad.

El objetivo no es únicamente desplegar servicios, sino **entender, documentar y mejorar progresivamente la infraestructura**, aplicando principios de seguridad, aislamiento y administración de sistemas.

---

## 1. Objetivos del proyecto

Los principales objetivos de `personal-infrastructure` son:

* Diseñar y mantener una infraestructura doméstica organizada y segmentada.
* Reutilizar hardware disponible para crear servidores y nodos de virtualización.
* Aprender y profundizar en **Proxmox VE**, virtualización y contenedores.
* Desplegar servicios personales y self-hosted.
* Crear un entorno independiente para experimentar con ciberseguridad.
* Implementar segmentación de red mediante VLANs y políticas de firewall.
* Centralizar y analizar logs y eventos de seguridad.
* Experimentar con monitorización, detección y respuesta ante incidentes.
* Documentar las decisiones técnicas y la evolución de la infraestructura.
* Aplicar buenas prácticas de seguridad a un entorno real de laboratorio.

---

## 2. Arquitectura general

La infraestructura está organizada en tres grandes áreas:

```text
                    Internet
                       │
                    Router
                       │
                   MikroTik
                       │
          ┌────────────┼────────────┐
          │            │            │
       Personal      Homelab      SOC Lab
          │            │            │
          │         Proxmox       VMs / CTs
          │            │           
          │       ┌───────────┼───────┐       
          │       │           │       │       
          │    Jellyfin  Vaultwarden NAS
          │
          └──────────────┬──────────────
                         │
                    Administración
```


## 3. Homelab

El **Homelab** constituye la parte de la infraestructura destinada a servicios personales, almacenamiento, virtualización y experimentación con diferentes tecnologías.

### Componentes previstos

* **Proxmox VE**

  * Plataforma principal de virtualización.
  * Máquinas virtuales.
  * Contenedores.
  * Gestión de recursos y almacenamiento.

* **Jellyfin**

  * Servidor multimedia self-hosted.
  * Streaming dentro de la infraestructura personal.

* **Vaultwarden**

  * Gestor de contraseñas compatible con Bitwarden.
  * Servicio que requiere especial atención a la seguridad, almacenamiento y backups.

* **NAS**

  * Almacenamiento centralizado.
  * Datos de servicios.
  * Backups y otros recursos de la infraestructura.

La infraestructura podrá ampliarse progresivamente con nuevos servicios según las necesidades del proyecto.

---

## 4. SOC Lab

El **SOC Lab** es el entorno destinado al aprendizaje práctico de ciberseguridad.

Su objetivo es disponer de un entorno controlado donde poder estudiar:

* Monitorización de sistemas.
* Análisis de logs.
* SIEM.
* Detección de amenazas.
* Monitorización de endpoints.
* Análisis de eventos.
* Respuesta ante incidentes.
* Threat detection.
* Vulnerabilidades y explotación controlada.
* Generación de telemetría.
* Validación de reglas de detección.

El laboratorio podrá incluir diferentes máquinas virtuales y contenedores que representen servidores, endpoints y otros componentes necesarios para realizar ejercicios de seguridad.

### SIEM y monitorización

Entre las tecnologías que podrán formar parte del laboratorio se encuentran:

* Wazuh.
* ELK / Elastic Stack.
* Agentes de monitorización.
* Herramientas de análisis de logs.
* Herramientas de generación de eventos.

La selección definitiva de herramientas se realizará durante las distintas fases de implementación.

---

## 5. Networking y seguridad

La red constituye una parte fundamental de la infraestructura.

El objetivo es evitar que los diferentes entornos tengan acceso indiscriminado entre sí y aplicar el principio de **mínimo privilegio** siempre que sea posible.

La infraestructura utiliza un **MikroTik** como componente central para:

* Routing.
* Segmentación de redes.
* VLANs.
* Firewall.
* Control de tráfico entre segmentos.
* Políticas de acceso.
* Administración de la infraestructura.

La arquitectura de red se irá documentando progresivamente a medida que se complete la implementación.

### Principios de seguridad

Las principales reglas de diseño son:

1. **Segmentación**

   * Separar los diferentes tipos de dispositivos y servicios.

2. **Mínimo privilegio**

   * Permitir únicamente las comunicaciones necesarias.

3. **Aislamiento del laboratorio**

   * Evitar que una máquina comprometida durante una prueba pueda afectar directamente a los dispositivos personales.

4. **Administración controlada**

   * El acceso administrativo a los sistemas debe estar restringido a los equipos autorizados.

5. **Defensa en profundidad**

   * Combinar segmentación, firewall, autenticación, monitorización y backups.

---

## 6. Virtualización

La virtualización será uno de los componentes principales de la infraestructura.

### Proxmox VE

Proxmox proporciona la plataforma sobre la que se ejecutarán diferentes máquinas virtuales y contenedores.

La infraestructura se utilizará para:

* Servidores Linux.
* Servidores Windows.
* Servicios self-hosted.
* Componentes del SOC Lab.
* Máquinas destinadas a pruebas de seguridad.
* Entornos temporales de experimentación.

La configuración concreta de cada máquina se documentará individualmente.

---

## 7. Fases del proyecto

El proyecto se desarrollará progresivamente.

### Fase 1 — Infraestructura

* Preparación del hardware.
* Instalación de Proxmox VE.
* Configuración de almacenamiento.
* Configuración de red.
* Validación de conectividad.

### Fase 2 — Networking

* Diseño de VLANs.
* Configuración del MikroTik.
* Routing entre redes.
* Reglas de firewall.
* Validación del aislamiento.

### Fase 3 — Homelab

Despliegue de los principales servicios:

* Jellyfin.
* Vaultwarden.
* NAS.
* Otros servicios futuros.

### Fase 4 — SOC Lab

* Despliegue de máquinas de laboratorio.
* Implementación del SIEM.
* Agentes de monitorización.
* Centralización de logs.
* Generación de eventos.
* Creación de casos de uso de detección.

### Fase 5 — Seguridad y monitorización

* Hardening.
* Backups.
* Monitorización.
* Alertas.
* Pruebas de segmentación.
* Validación de reglas de firewall.

### Fase 6 — Experimentación

Una vez establecida la infraestructura base, se realizarán pruebas controladas relacionadas con:

* Vulnerabilidades.
* Técnicas de ataque.
* Generación de telemetría.
* Detección.
* Análisis.
* Respuesta ante incidentes.

Todas las pruebas se realizarán dentro del entorno controlado del laboratorio.

---

## 8. Documentación

La documentación se organiza en diferentes áreas:

```text
personal-infrastructure/
│
├── homelab/
│   ├── proxmox/
│   ├── services/
│   ├── storage/
│   └── backups/
│
├── soclab/
│   ├── architecture/
│   ├── monitoring/
│   ├── detection/
│   └── incidents/
│
├── network/
│   ├── diagrams/
│   ├── vlans/
│   └── firewall/
│
├── docs/
│   ├── architecture.md
│   ├── security.md
│   └── decisions/
│
└── scripts/
```

Esta estructura podrá evolucionar a medida que crezca el proyecto.

---

## 9. Seguridad del repositorio

Este repositorio está diseñado para ser **público**, por lo que la documentación se prepara teniendo en cuenta la exposición de información de infraestructura.

No se almacenarán en el repositorio:

* Contraseñas.
* API keys.
* Tokens.
* Claves privadas.
* Credenciales.
* Ficheros `.env`.
* Certificados privados.
* Backups que contengan información sensible.
* Configuraciones que permitan acceder directamente a la infraestructura.

Los diagramas y documentación pública utilizarán información **anonimizada cuando sea necesario**.

La documentación detallada de la infraestructura real se mantendrá separada de la documentación pública cuando contenga información que no sea necesaria para comprender el diseño.

---

## 10. Objetivo final

El objetivo de `personal-infrastructure` es convertir una infraestructura doméstica en un entorno práctico de aprendizaje continuo.

El proyecto combina:

```text
                PERSONAL INFRASTRUCTURE
                         │
          ┌──────────────┼──────────────┐
          │              │              │
       HOMELAB        NETWORK         SOCLAB
          │              │              │
      Proxmox         MikroTik       SIEM
      Services        VLANs          Detection
      Storage         Firewall       Monitoring
      Backups         Routing        Incident Response
          │              │              │
          └──────────────┼──────────────┘
                         │
                   Security
```

Más que un conjunto de servicios, este repositorio representa la **evolución de una infraestructura personal**, documentando las decisiones, configuraciones, problemas encontrados y soluciones implementadas durante el proceso.

---

## Estado del proyecto

🚧 **En desarrollo**

La infraestructura se encuentra en proceso de diseño, implementación y migración. La documentación se actualizará a medida que se incorporen nuevos componentes y se validen las diferentes partes del entorno.

---

## Tecnologías

Actualmente el proyecto contempla tecnologías como:

* Proxmox VE
* MikroTik
* VLANs
* Docker
* Linux
* Windows
* Wazuh
* Elastic Stack
* Jellyfin
* Vaultwarden
* NAS
* Git / GitHub

La lista se actualizará a medida que evolucione el proyecto.

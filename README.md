# MDXLAB — Homelab

> Proyecto personal de infraestructura, self-hosting y aprendizaje.

## ¿Por qué el proyecto?

MDXLAB nació a partir de reutilizar computadoras que estaban sin uso y del interés por aprender sobre administración de servidores, redes, Docker y tecnologías de self-hosting.

Con el tiempo evolucionó hacia un ecosistema propio para alojar servicios, almacenamiento y una nube privada, manteniendo control sobre la infraestructura y los datos.

El dominio utilizado por el homelab es:

```text
mdxlab.dev
```

---

## Infraestructura

Actualmente el homelab se divide principalmente en dos nodos:

| Nodo | IP | Rol |
|---|---|---|
| Nodo 102 | `192.168.0.102` | Infraestructura base: Pi-hole y MariaDB |
| Nodo 103 | `192.168.0.103` | Docker, aplicaciones, almacenamiento, proxy, túneles y correo |

La infraestructura utiliza, entre otros componentes:

- Docker / Docker Compose
- Pi-hole
- Nginx Proxy Manager
- Cloudflare DNS y Cloudflare Tunnel
- MariaDB
- Stalwart
- Brevo como SMTP relay

La información técnica detallada y vigente se mantiene en la documentación de arquitectura.

---

## Servicios activos

| Servicio | Función | Acceso |
|---|---|---|
| Nextcloud | Nube privada / archivos | LAN + Internet |
| Immich | Gestión y respaldo de fotografías | LAN + Internet |
| Nginx Proxy Manager | Reverse proxy y certificados TLS | LAN |
| FileBrowser Quantum | Gestión web de archivos | LAN |
| Homarr | Dashboard del homelab | LAN |
| Vaultwarden | Gestor de contraseñas | LAN |
| Stalwart | Servidor de correo / SMTP central | Interno |
| Cloudflared | Cloudflare Tunnel | Infraestructura |
| Pi-hole | DNS de la LAN | LAN |
| MariaDB | Base de datos de infraestructura | Interno |

> La presencia de un directorio o `docker-compose.yaml` en este repositorio **no implica que el servicio se encuentre actualmente desplegado**. El repositorio conserva también definiciones de servicios anteriores, pruebas y proyectos que pueden reutilizarse en el futuro.

---

## Acceso a servicios

MDXLAB diferencia entre servicios disponibles únicamente dentro de la LAN y servicios publicados hacia Internet.

Actualmente, los principales servicios públicos son:

| Servicio | LAN | Internet |
|---|---|---|
| Nextcloud | `cd.mdxlab.dev` | `nc.mdxlab.dev` |
| Immich | `mi.mdxlab.dev` | `im.mdxlab.dev` |

Otros servicios administrativos y privados permanecen únicamente dentro de la red local.

Para conocer todos los FQDN, rutas, puertos y mecanismos de resolución, consultar el documento de arquitectura.

---

## Estructura del repositorio

El repositorio organiza principalmente cada servicio en su propio directorio:

```text
homelab/
├── AGENTS.md
├── README.md
├── docs/
│   ├── arquitectura_homelab_mdxlab_activa.md
│   └── roadmap_historico_homelab_mdxlab_nuevo.md
│
├── cloudflare/
├── filebrowser-quantum/
├── homarr/
├── immich/
├── nextcloud/
├── nginx-proxy-manager/
├── stalwart/
├── vaultwarden/
└── ...
```

Los nombres concretos de algunos directorios pueden variar conforme evolucione el repositorio.

Los directorios de servicios contienen principalmente sus definiciones Docker Compose y archivos versionables relacionados.

---

## Documentación

### Arquitectura activa

```text
docs/arquitectura_homelab_mdxlab_activa.md
```

Es la referencia del **estado funcional vigente** de MDXLAB.

Incluye:

- servidores;
- hardware y almacenamiento;
- servicios activos;
- dominios;
- DNS;
- Nginx Proxy Manager;
- Cloudflare Tunnel;
- puertos;
- persistencia;
- rutas importantes;
- infraestructura de correo;
- notas técnicas permanentes.

### Roadmap e histórico

```text
docs/roadmap_historico_homelab_mdxlab_nuevo.md
```

Contiene:

- mejoras pendientes;
- tareas en progreso;
- evolución de la infraestructura;
- decisiones técnicas relevantes;
- incidencias y soluciones resumidas.

El histórico se mantiene deliberadamente breve para conservar únicamente conocimiento reutilizable.

### Instrucciones para agentes

```text
AGENTS.md
```

Define cómo deben trabajar los agentes de IA sobre este repositorio, incluyendo criterios de documentación, Docker Compose, secretos, troubleshooting y actualización de la arquitectura.

---

## Docker Compose

Los servicios Docker se gestionan mediante Docker Compose.

Comandos habituales en los servidores MDXLAB:

```bash
# Levantar o actualizar un servicio
sudo docker compose up -d

# Ver contenedores
sudo docker ps

# Ver contenedores con formato compacto
sudo docker ps --format "table {{.Names}}\t{{.Image}}\t{{.Status}}"

# Consultar logs
sudo docker logs --tail 100 <contenedor>

# Seguir logs
sudo docker logs -f <contenedor>
```

Normalmente los comandos de Compose deben ejecutarse desde el directorio correspondiente al servicio.

---

## Seguridad

Los secretos **no deben versionarse** en el repositorio.

Esto incluye:

- contraseñas;
- API keys;
- SMTP keys;
- tokens;
- claves privadas TLS;
- credenciales administrativas;
- archivos `.env` que contengan información sensible.

Los Compose deben utilizar variables de entorno cuando corresponda y los archivos sensibles deben permanecer excluidos mediante `.gitignore`.

Nunca incluir valores reales de secretos en la documentación.

---

## Filosofía del proyecto

MDXLAB es un proyecto en evolución. La prioridad es mantener una infraestructura que permita aprender, experimentar y alojar servicios útiles sin perder claridad sobre cómo está construida.

La documentación se divide deliberadamente entre:

```text
README
  └─ Qué es el proyecto y cómo navegar el repositorio

Arquitectura
  └─ Cómo funciona MDXLAB actualmente

Roadmap / histórico
  └─ Qué falta, qué ha cambiado y qué problemas relevantes se encontraron

AGENTS
  └─ Cómo deben trabajar los agentes sobre el repositorio
```

Esta separación busca evitar que un único documento termine convirtiéndose simultáneamente en inventario, manual, roadmap y bitácora.

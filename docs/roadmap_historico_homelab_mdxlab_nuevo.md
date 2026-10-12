# Roadmap e histórico técnico --- MDXLAB

> Documento breve de evolución, incidencias y mejoras pendientes. El estado funcional vigente se mantiene en `arquitectura_homelab_mdxlab_activa.md`.

## 1. Roadmap actual

| # | Mejora | Estado | Objetivo |
|---:|---|---|---|
| 0 | FileBrowser Quantum | ✅ Completado | Sustituir Filebrowser por una alternativa más completa |
| 1 | Homarr | ✅ Completado | Dashboard central del homelab |
| 2 | Vaultwarden | ✅ Completado | Gestor de contraseñas self-hosted con correo funcional |
| 3 | Stalwart / correo central | 🟡 Base funcional | Centralizar SMTP y salida mediante Brevo |
| 4 | Uptime Kuma | ✅ Completado | Monitorear disponibilidad de servicios |
| 5 | Hardening / seguridad | ⏳ Pendiente | Revisar SSH, firewall, Docker, NPM/Cloudflare, usuarios y permisos |
| 6 | Monitorización de hardware | ⏳ Pendiente | CPU, RAM, temperaturas, SMART, almacenamiento y red |
| 7 | Evaluar servicios anteriores | ⏳ Pendiente | Revisar Jellyfin, Jellyseerr, Sonarr, Transmission, Kavita, Calibre, Firefly III y otros; Wallos se mantiene activo |
| 8 | Backups | ⏳ Pendiente | Diseñar estrategia de respaldo, retención y restauración |

---

## 2. Mejoras identificadas

### Correo

| Mejora | Estado | Nota |
|---|---|---|
| Certificado TLS válido para Stalwart | Completado | Certificado dedicado de Let’s Encrypt para `mail.mdxlab.dev`, emitido mediante DNS-01 con Cloudflare |
| Deliverability hacia Microsoft | Pendiente | Los mensajes llegan a No deseado pese a SPF/DKIM/DMARC/CompAuth en PASS |
| Tracking de Brevo | Evaluar | Brevo reescribe enlaces mediante su infraestructura de click tracking |
| Nextcloud → Stalwart | Pendiente | Centralizar su correo saliente |
| Immich → Stalwart | Pendiente | Centralizar su correo saliente si se requiere |
| Otros servicios → Stalwart | Pendiente | Incorporar conforme necesiten correo |
| MX directo en Stalwart | Futuro / opcional | Actualmente la recepción pública permanece en Cloudflare Email Routing |

### Infraestructura y hardware

| Mejora | Estado |
|---|---|
| Switch Gigabit administrable | Pendiente |
| Router MikroTik | Pendiente |
| Access Point / mejora Wi-Fi | Pendiente |
| VLAN para servidores, clientes, IoT e invitados | Pendiente |
| HDD dedicado para backups | Pendiente |
| UPS | Pendiente |
| Revisar SSD adicional de ~500 GB | Pendiente |
| Evaluar Raspberry Pi / mini-PC / ThinkCentre para futuras funciones | Pendiente |

### Monitorización de servicios

| Mejora | Estado | Nota |
|---|---|---|
| Actualizar monitores de Uptime Kuma | Completado | Todos los monitores activos en verde, con un único monitor por servicio. MariaDB conserva su monitor; Nextcloud e Immich se comprueban por la ruta pública y las demás interfaces web por LAN. Jellyfin no está desplegado y su monitor permanece pausado. |

---

## 3. Registro histórico

### 2026-08 — FileBrowser Quantum

**Cambio:** Se sustituyó el Filebrowser anterior por FileBrowser Quantum.

**Resultado:** Servicio operativo en LAN mediante `fl.mdxlab.dev`, con persistencia en el HDD del homelab y soporte multimedia mediante FFmpeg/FFprobe.

### 2026-08 — Homarr

**Cambio:** Se incorporó Homarr como dashboard central del homelab.

**Resultado:** Operativo en `hr.mdxlab.dev`, solo LAN, con integración Docker y persistencia dedicada.

### 2026-08 — Vaultwarden

**Cambio:** Se desplegó Vaultwarden, se cerró el registro público, se habilitó el panel administrativo y posteriormente se integró con Stalwart para correo.

**Resultado:** Operativo en `vw.mdxlab.dev`. Se verificaron tanto el Test SMTP como una invitación real de usuario.

### 2026-09 — Uptime Kuma

**Cambio:** Se actualizó Uptime Kuma de `1.23.17` a `2.5.3`, se habilitó su acceso LAN mediante `uk.mdxlab.dev` y se integró con Homarr.

**Resultado:** Servicio operativo con alertas de Telegram verificadas. La sustitución de monitores heredados por los servicios actuales del homelab permanece pendiente.

### 2026-10 — Resolución DNS de Pi-hole desde Uptime Kuma

**Problema:** El monitor web de Pi-hole fallaba porque el contenedor no resolvía `pi.hole`; Docker reenviaba las consultas a DNS públicos, aunque el servidor tenía Pi-hole como DNS.

**Resolución:** Se recreó únicamente el contenedor de Uptime Kuma, sin añadir un DNS explícito al Compose.

**Resultado:** Resolución de `pi.hole` a `192.168.0.102` verificada y monitor HTTP operativo mediante el nombre local.

### 2026-10 — TLS SMTP de Vaultwarden y Stalwart

**Cambio:** Stalwart empezó a gestionar automáticamente un certificado Let’s Encrypt para `mail.mdxlab.dev` mediante DNS-01 con Cloudflare; Vaultwarden pasó a usar ese hostname por SMTP `465`.

**Resultado:** TLS validado con `Verify return code: 0 (ok)` y prueba SMTP de Vaultwarden completada. Se retiraron las excepciones para certificados y hostnames inválidos.

### 2026-10 — Integración de Wallos

**Cambio:** Wallos se mantuvo como servicio activo en `wl.mdxlab.dev` y se incorporó a Nginx Proxy Manager, Uptime Kuma y Homarr.

**Resultado:** Acceso LAN por HTTPS y monitor HTTP operativo en verde.

### 2026-08 — Infraestructura de correo Stalwart + Brevo

**Cambio:** Se implementó Stalwart como servidor SMTP central. Brevo fue elegido como relay externo después de evaluar otras alternativas; SMTP2GO se descartó por restricciones de verificación SMS para México.

**Incidencias:** La instalación inicial encontró permisos incorrectos en los bind mounts; se corrigieron asignando los directorios persistentes al UID/GID `2000`. También se sustituyó el tracer de archivo por `Console / Info` para integrarlo correctamente con Docker.

**Resultado:** Flujo `Aplicaciones → Stalwart → Brevo → Internet` verificado. El dominio está autenticado y Microsoft reportó SPF, DKIM, DMARC y CompAuth en PASS.

### 2026-08 — Entregabilidad de correo

**Problema:** Los primeros mensajes transaccionales entregados a Hotmail fueron clasificados como No deseado.

**Diagnóstico:** Las cabeceras del mensaje mostraron autenticación correcta (`SPF`, `DKIM`, `DMARC` y `CompAuth` en PASS), por lo que no se modificó DNS a ciegas.

**Estado:** Pendiente mejorar reputación/deliverability. Se detectó además que Brevo reescribe enlaces para click tracking.

### 2026-08 — Apagado incompleto del Nodo 103

**Problema:** Debian completaba el apagado, pero ocasionalmente el servidor permanecía físicamente encendido.

**Resolución:** Tras descartar un fallo evidente de Docker/userland, se actualizó el BIOS de la MSI B460M PRO de `1.20` a `1.B2`. Después del update fue necesario desactivar Secure Boot para recuperar el arranque normal de Debian.

**Resultado:** Pruebas posteriores de `reboot` y `poweroff`, incluida una tras una sesión prolongada, finalizaron correctamente. Se mantiene en observación.

---

## 4. Criterios para nuevos servicios

Cada nuevo servicio deberá documentar, como mínimo:

- Nodo donde se ejecuta.
- Datos persistentes y ubicación.
- Base de datos, si aplica.
- FQDN y tipo de acceso: LAN o público.
- Puertos relevantes.
- Información que requiere respaldo.
- Dependencias externas.
- Método de recuperación básico.

Cuando una mejora se complete:

1. Se actualiza `arquitectura_homelab_mdxlab_activa.md` con el nuevo estado vigente.
2. Se marca la mejora como completada en este roadmap.
3. Solo si aporta valor futuro, se añade una entrada histórica breve.

El histórico debe permanecer compacto: registrar **qué ocurrió, cómo se resolvió de forma general y cuál fue el resultado**, sin convertirse en una transcripción detallada de comandos o pruebas.

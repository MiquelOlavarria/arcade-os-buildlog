# 🐛 Incidencias — problemas reales y soluciones

Registro honesto de todo lo que falló durante el proyecto y cómo se resolvió.
Actualizado a medida que aparecen.

## Instalación (Fase 2)

| Problema | Síntoma | Solución |
|---|---|---|
| Descarga de la ISO cortada por Cloudflare | `curl: (92)` HTTP/2 reset / `(18) end of response` | **aria2c -c -x8** (8 conexiones, resume, reintentos) |
| sshd del instalador de Fedora no arranca | `status=1/FAILURE` al hacer `systemctl start sshd` | `ssh-keygen -A` (faltaban las claves de host) |
| `usermod -l` no renombra el usuario | *"user is currently used by process 1669"* | `loginctl terminate-user` + job desprendido (el proceso era el `systemd --user` del propio usuario) |
| SELinux bloquea el servicio arcadenorm | `status=203/EXEC` en systemd | Copiar el binario a `/usr/local/bin` (contexto de sistema) |
| arcadenorm no se instala en /usr/bin | *"Sistema de ficheros de sólo lectura"* | Fedora Atomic: `PREFIX=$HOME/.local` |
| fstab roto tras convertir el disco | `mount: wrong fs type` | El script cambió el UUID pero no el tipo (`ntfs3` → `btrfs`) |
| Flathub de sistema filtrado en Bazzite | *"Nada coincide ... en la rama remota flathub"* | Añadir el remoto Flathub **de usuario** |
| Heroic no aparece en Flathub | ID con mayúsculas no existe | El ID real es `com.heroicgameslauncher.hgl` |
| Drop-ins SSH de Red Hat deshabilitados | archivos en `sshd_config.d/disabled/` | Devolver a `sshd_config.d/`; el `40-...` estaba incompleto (faltaba el `Include` de crypto-policies) |
| sshd_config con `\n` literales | `unsupported option "no\nKbdInteractive..."` | Reescribir con `printf '%s\n'` (escaping remoto) |
| Calibración arcadenorm en portugués | — | Chuleta traducida (palanca = mantener, AGORA = pulsar) |
| `--jogadores 2` no sirve para dos placas | Calibra 2 jugadores en una sola placa | Es para encoders duales; dos placas = calibrar una vez por placa |

## Descarga de la ISO (Fase 1)

| Problema | Síntoma | Solución |
|---|---|---|
| Descarga de la ISO cortada por Cloudflare | `curl: (92)` HTTP/2 reset / `(18) end of response` | **aria2c -c -x8** (8 conexiones, resume, reintentos) |
| USB con Ventoy no arranca | — | Probar otro dispositivo (NVMe en caja USB) |

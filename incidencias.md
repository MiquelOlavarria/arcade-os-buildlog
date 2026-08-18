# 🐛 Incidencias — problemas reales y soluciones

Registro honesto de todo lo que falló durante el proyecto y cómo se resolvió.
Actualizado a medida que aparecen.

## Descarga de la ISO (Bazzite)

| Problema | Causa | Solución |
|---|---|---|
| `curl: (92) HTTP/2 stream reset by server` a mitad de descarga | Cloudflare corta streams HTTP/2 largos | Reintentar con `--http1.1 -C -` (resume) |
| `curl: (18) end of response with N bytes missing` | Corte de nuevo en HTTP/1.1 | Cambiar a **aria2c multi-conexión**: `aria2c -c -x 8 -s 8 -k 4M` (8 conexiones + resume + reintentos infinitos). Descarga estable a 23 MB/s |
| Buscadores web agotados/bloqueados (Brave cuota 2000/mes, Firecrawl key inválida, DDG rate-limit) | Backends de búsqueda configurados mal/agotados | Usar **NotebookLM** (Google) como buscador + RAG: se añaden fuentes por URL o búsqueda, y las consultas devuelven análisis con citas |

## Instalación (Bazzite/Anaconda)

| Problema | Causa | Solución |
|---|---|---|
| El USB Ventoy "no arranca bien" | USB defectuoso/lento o boot order | Probar con otro disco (NVMe en caja USB con Ventoy) → funciona |
| `systemctl start sshd` falla en el instalador (exit 1) | El entorno Anaconda no tiene **claves de host SSH** | `ssh-keygen -A` y volver a arrancar `sshd` |
| `inst.sshd` del arranque no levanta | Parámetro de kernel no aplicado (edición de grub) | Alternativa: terminal del instalador con `Ctrl+Alt+F2` (shell root) |
| Confusión de discos en el instalador (2× 500 GB) | Discos similares | Identificar por modelo/tamaño en `lsblk -f`; marcar SOLO el de Windows; dejar el NTFS de ROMs sin marcar |

## Pendientes de resolver

- [ ] Regenerar service account de 1Password (403 Service Account Deleted)
- [ ] Backend web de búsqueda de Hermes (configurar clave válida)

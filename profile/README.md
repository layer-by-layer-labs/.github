# layer-by-layer-labs

**Laboratorios gratuitos y autocorregibles de infraestructura: Linux, redes, servidores web, contenedores y cloud.**

Cada unidad tiene tres partes:

| | |
|---|---|
| 🎬 **Vídeo conceptual** (~5 min) | El problema y los conceptos necesarios para entenderlo |
| 🛠️ **Vídeo tutorial** (~5 min) | La demostración paso a paso en una terminal real |
| 🧪 **Laboratorio** | Un entorno reproducible con una avería real y un verificador: `./check.sh` |

No aprendes a copiar comandos: aprendes a **diagnosticar capa por capa**, como en un trabajo real.

## Catálogo

### Serie: HTTPS en Linux — del servidor vacío al sitio seguro

| Unidad | Tema | Laboratorio | Vídeos |
|---|---|---|---|
| HTTPS-01 | Nginx sirve el sitio equivocado: cómo elige el server block | [https-01-nginx-server-block](https://github.com/layer-by-layer-labs/https-01-nginx-server-block) | *próximamente* |

*Próximas unidades: varios sitios por nombre, TLS y certificados, CA propia, redirección a HTTPS, diagnóstico de certificados, ACME.*

## Cómo usar un laboratorio

1. Necesitas **Ubuntu 24.04 LTS** (máquina virtual o nativo) con **Docker** y **Git**. Otros sistemas pueden funcionar, pero no tienen soporte.
2. Pulsa **"Use this template"** en el laboratorio para crear tu propia copia, o clónalo directamente.
3. Sigue el README, resuelve la avería y comprueba tu solución con `./check.sh`.

Todo es gratuito. No necesitas cuenta de pago, créditos ni beneficios educativos.

## Licencia y autoría

Código bajo licencia MIT, textos bajo CC BY 4.0. Creado por **Oscar H. Mondragón, Ph.D.** · [YouTube](https://www.youtube.com/@oscarmondragon1294) · [GitHub](https://github.com/omondragon)

¿Encontraste un error? Abre un *issue* en el repositorio del laboratorio.

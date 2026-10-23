# layer-by-layer-labs

**Laboratorios gratuitos y autocorregibles de infraestructura: Linux, redes, servidores web, contenedores y cloud.**

> Los tutoriales suelen enseñar el camino feliz: los comandos que funcionan a la primera.
> En el trabajo real, lo difícil empieza cuando algo **no** funciona.
> Aquí cada laboratorio trae una **avería real** y tu trabajo es encontrarla y corregirla.

---

## ¿Para quién es?

- Estudiantes de ingeniería de sistemas, informática, telecomunicaciones y carreras afines.
- Profesionales junior que quieren pasar a infraestructura, operaciones o DevOps.
- Desarrolladores que despliegan aplicaciones y quieren entender el servidor que las publica.
- Cualquier persona que sepa moverse en la terminal y quiera aprender haciendo.

No necesitas experiencia previa en DevOps ni en cloud. Basta con saber usar la terminal (`cd`, `ls`, editar un archivo) y tener nociones de qué son una IP y un puerto.

## Qué hace diferente a estos laboratorios

| | |
|---|---|
| 🔧 **Averías reales** | No copias comandos: diagnosticas un servidor que falla, como en un incidente real. |
| ✅ **Verificación automática** | `./check.sh` hace peticiones reales a tu servidor y te dice qué falla, con pistas pero sin darte la solución. No dependes de que nadie revise tu trabajo. |
| 🔁 **Reproducibles** | Cada laboratorio arranca igual en cualquier máquina con Docker, y se reinicia en segundos. |
| 🧪 **Probados** | Cada laboratorio se prueba automáticamente: el estado inicial debe fallar y la solución de referencia debe aprobar. |
| 💸 **Gratuitos** | Sin cuentas de pago, créditos en la nube ni beneficios educativos. |

## Cómo está organizada cada unidad

Cada unidad tiene tres piezas, pensadas para usarse en este orden:

| Paso | Pieza | Qué haces |
|---|---|---|
| 1 | 🎬 **Vídeo conceptual** (~4 min) | Entiendes el problema y los conceptos que necesitas. |
| 2 | 🧪 **Laboratorio** | Intentas resolver la avería **por tu cuenta**, usando `./check.sh` como guía. |
| 3 | 🛠️ **Vídeo tutorial** (~4 min) | Ves la resolución paso a paso. Úsalo si te atascas, o después de resolverlo, para comparar tu método. |

**Recomendación:** intenta el laboratorio *antes* del tutorial. El aprendizaje está en el diagnóstico, no en la solución. Si llevas 20–30 minutos sin avanzar, mira el tutorial hasta el punto en que te atascaste y vuelve a intentarlo.

## El método: diagnosticar capa por capa

Todos los laboratorios entrenan el mismo hábito: no adivinar, sino **descartar causas en orden**, desde la más básica.

| Capa | Pregunta | Herramientas |
|---|---|---|
| 1. Nombre | ¿El nombre resuelve a la IP correcta? | `getent hosts`, `dig` |
| 2. Red | ¿Llego a esa IP? | `ping`, `ip route` |
| 3. Puerto | ¿Hay algo escuchando en el puerto? | `ss -tlnp`, `curl` |
| 4. Proceso | ¿El servicio está vivo? ¿Qué dicen sus registros? | `systemctl`, `docker compose ps`, `logs` |
| 5. Configuración | ¿La configuración es válida y está cargada? | `nginx -t`, `reload` |
| 6. Contenido y permisos | ¿El servicio puede leer lo que debe servir? | `ls -l`, `namei -l` |
| 7. TLS | ¿El certificado es válido, vigente y para este nombre? | `openssl s_client` |

Cada laboratorio pone el foco en una o dos capas. Con la serie completa, el método se vuelve automático.

---

## Catálogo

### Serie: HTTPS en Linux — del servidor vacío al sitio seguro

Lleva un servidor desde cero hasta publicar varios sitios con HTTPS, y enseña a diagnosticar los errores más comunes en cada paso.

| Unidad | Tema | 🎬 Conceptual | 🛠️ Tutorial | 🧪 Laboratorio |
|---|---|---|---|---|
| HTTPS-01 | Nginx sirve el sitio equivocado: cómo elige el server block | [Ver](https://youtu.be/7KdwEiBm2Uc) | [Ver](https://youtu.be/gLCVzIdojXE) | [https-01-nginx-server-block](https://github.com/layer-by-layer-labs/https-01-nginx-server-block) |

**Próximas unidades de la serie** (el orden puede cambiar según los comentarios):

| Unidad | Tema previsto |
|---|---|
| HTTPS-02 | Dos sitios en un mismo servidor: hosting virtual por nombre |
| HTTPS-03 | Qué es TLS y por qué un certificado autofirmado no basta |
| HTTPS-04 | Tu propia autoridad certificadora: clave, CSR y cadena de confianza |
| HTTPS-05 | Redirección de HTTP a HTTPS sin bucles |
| HTTPS-06 | Certificados que fallan: vencidos, con otro nombre o con la cadena incompleta |
| HTTPS-07 | Certificados automáticos con ACME (el protocolo de Let's Encrypt) |
| HTTPS-08 | Proyecto integrador: la infraestructura web de una empresa ficticia |

**Series futuras:** DNS, SSH, firewall, Docker, balanceo de carga, Kubernetes, monitoreo y automatización.

---

## Antes de empezar: prepara tu entorno (una sola vez)

**Entorno oficial: Ubuntu 24.04 LTS**, en una máquina virtual o instalado directamente. Los laboratorios se prueban en Ubuntu sobre x86 y sobre ARM.

> En Windows o macOS, crea una máquina virtual con Ubuntu 24.04 (por ejemplo, con VirtualBox, UTM o Multipass). Los laboratorios pueden funcionar directamente en otros sistemas, pero no tienen soporte.

Dentro de Ubuntu, instala Docker, Git y curl:

```bash
sudo apt update
sudo apt install -y docker.io docker-compose-v2 git curl
sudo usermod -aG docker "$USER"      # para usar docker sin sudo
```

Cierra la sesión y vuelve a entrar, y comprueba:

```bash
docker run --rm hello-world          # debe imprimir "Hello from Docker!"
docker compose version
```

## Cómo trabajar un laboratorio

1. **Crea tu copia.** En el repositorio del laboratorio pulsa **Use this template → Create a new repository**. Así guardas tu progreso en tu propia cuenta. También puedes clonarlo directamente:
   ```bash
   git clone https://github.com/layer-by-layer-labs/<laboratorio>.git
   cd <laboratorio>
   ```
2. **Lee el README del laboratorio:** objetivos, misión y herramientas sugeridas.
3. **Arranca el entorno:** `docker compose up -d`
4. **Diagnostica y corrige.** Ejecuta `./check.sh` tantas veces como quieras: cada fallo trae una pista.
5. **Aprobado** cuando veas `Resultado: APROBADO`.
6. **Responde las preguntas de comprobación** del README. Si puedes explicar por qué falló, lo aprendiste.
7. **Intenta el reto adicional**, y deja el entorno limpio con `docker compose down`.

**Reglas del juego:** la solución de referencia está en la carpeta `solucion/`, pero ábrela solo al final. Y si cambiaste algo y quieres empezar de cero: `git checkout -- .` y `docker compose up -d --force-recreate`.

## Preguntas frecuentes

**¿Cuesta algo?** No. Los vídeos, los laboratorios y los verificadores son gratuitos.

**¿Dan certificado?** No. El objetivo es que aprendas a resolver problemas reales. Tu copia del laboratorio resuelto, con tus commits, es tu evidencia.

**¿Necesito una cuenta de GitHub?** Solo para crear tu copia con *Use this template*. Para clonar y practicar, no.

**Encontré un error o me quedé atascado por algo que no es la avería.** Abre un *issue* en el repositorio del laboratorio y explica qué hiciste y qué viste. Esos reportes mejoran el laboratorio para todos.

---

## Autoría y licencia

Creado por **Oscar H. Mondragón, Ph.D.**, profesor e investigador en computación, con experiencia en Linux, redes, sistemas distribuidos y computación de alto rendimiento.
[YouTube](https://www.youtube.com/@oscarmondragon1294) · [GitHub](https://github.com/omondragon)

Código bajo licencia **MIT** y textos bajo **CC BY 4.0**: puedes usarlos, adaptarlos y compartirlos citando la fuente.

*Los vídeos usan narración con voz sintética. Los guiones, los diagramas y los laboratorios son de elaboración propia.*

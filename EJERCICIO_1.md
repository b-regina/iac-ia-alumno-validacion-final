# Ejercicio 1 · Mi primera infraestructura como código asistida por IA

**Ruta principal: navegador.** Tiempo de trabajo orientativo: 60–90 minutos; reserva además tiempo de explicación y dudas en clase. **Empiezas aquí.** El ejercicio 2 continúa en **tu misma copia** del repositorio.

## Qué vamos a hacer y por qué

Un equipo ficticio describe una aplicación llamada `portal-demo`. Antes de modificar una configuración, necesita poder responder: «¿Qué valor está escrito, quién lo cambió y qué haría OpenTofu con él?». Escribir esa descripción en archivos revisables es una forma sencilla de **Infraestructura como Código (IaC)**.

Vas a crear una copia propia del laboratorio, comprobar que GitHub puede instalar y ejecutar OpenTofu, cambiar el entorno de `desarrollo` a `pruebas`, guardar el cambio en GitHub y localizar el resultado en un plan. **No vas a desplegar una web ni recursos cloud.** `terraform_data` solo representa una ficha ficticia. El workflow no tiene `tofu apply`.

**Lo que entregarás:** enlace a tu copia, enlace al commit del cambio y enlace a su ejecución verde. Deberás explicar con tus palabras dónde se declara `entorno`, dónde se usa y qué demuestra el plan.

## Antes de pulsar nada: el mapa de las tres pantallas

| Pantalla | Para qué la utilizarás | Lo que NO necesitas instalar |
| --- | --- | --- |
| `github.com` | Crear tu copia, ver commits y consultar **Actions**. | GitHub Actions es una pestaña de GitHub, no una aplicación local. |
| `github.dev` (a veces `vscode.dev`) | Abrir **tu copia** en el editor web, cambiar un archivo, confirmar y publicar. | VS Code local y Git local. |
| **Actions** de tu copia | GitHub prepara un ejecutor temporal, instala OpenTofu y realiza las comprobaciones. | OpenTofu en tu ordenador. |

Necesitas una cuenta gratuita de GitHub con el correo verificado y acceso desde el navegador. Usa solo datos inventados. Si la organización bloquea GitHub o Actions, anota el bloqueo y sigue la demostración de la docente; no introduzcas credenciales ni datos corporativos para intentar evitarlo. La IA se abre en **una segunda pestaña**, no dependemos de un agente integrado en el editor.

## Paso 1 · Crea una copia que sea tuya

1. Entra en **[la plantilla del curso](https://github.com/b-regina/iac-ia-laboratorio-demo)** con tu cuenta. Verifica que arriba dice `b-regina / iac-ia-laboratorio-demo`.
2. Pulsa el botón **Use this template** y después **Create a new repository**. No pulses el botón **Code → Clone**: ese botón sirve para descargar al ordenador y no crea tu copia de trabajo en GitHub.
3. En **Owner**, elige **tu usuario**. En **Repository name**, escribe `iac-ia-practica-tuusuario`, sustituyendo `tuusuario` por tu nombre de usuario. Elige **Public** y deja **Include all branches** desmarcado. Pulsa **Create repository**.
4. Mira la dirección del navegador: debe comenzar por `https://github.com/TU_USUARIO/`. Verifica que ves `README.md`, `EJERCICIO_1.md`, `main.tf`, `variables.tf` y `outputs.tf`. **No modifiques la plantilla de `b-regina`.**

**Punto de control:** si tu copia está vacía, probablemente elegiste **New repository** en vez de **Use this template**. Crea una nueva copia desde el enlace de la plantilla; no continúes con un repositorio vacío. Si el nombre ya existe, elige otro nombre y conserva su URL.

## Paso 2 · Comprueba la ejecución inicial y la instalación automática

1. En la página de **tu copia**, pulsa la pestaña **Actions** (en español, **Acciones**) de la barra superior. Busca el workflow **Validacion IaC** y una ejecución llamada **Initial commit** o **Commit inicial**.
2. Pulsa esa ejecución. En la columna izquierda, debajo de **Todos los trabajos**, pulsa **comprobar**, el renglón con el círculo verde. **No pulses «Uso» ni el icono de filtro**: esos controles muestran otra información.
3. A la derecha aparecen pasos como **Obtener codigo**, **Instalar OpenTofu**, **Inicializar**, **Comprobar formato**, **Validar** y **Mostrar plan**. Si todos tienen marca de éxito y el encabezado está verde, la configuración inicial ha funcionado.
4. Si quieres ver cómo se instala, abre la flecha `>` situada **justo a la izquierda de «Instalar OpenTofu»**. Aparece la acción `opentofu/setup-opentofu@v2`. El archivo `.github/workflows/validacion.yml` ya contiene esa instrucción. Se instala **para esa ejecución en GitHub**; no queda instalado en tu ordenador.

**Si no hay ejecución inicial:** espera unos segundos y recarga **Actions**. Si GitHub muestra un aviso para habilitar workflows en **tu copia**, sigue las indicaciones de la propia página. Si el workflow aparece pero no hay ejecución, abre **Validacion IaC**, pulsa **Run workflow**, selecciona `main` y confirma **Run workflow**. Si no puedes habilitarlo por permisos o política, comunica el bloqueo a la docente; esa cuenta aún no ha superado la prueba de acceso.

**Punto de control:** el verde de *Commit inicial* prueba que la instalación y el código **tal como venían en la copia** funcionan. Todavía no demuestra que tu futuro cambio a `pruebas` funcione.

## Paso 3 · Entiende los tres archivos antes de editar

Vuelve a la pestaña **Code/Código** de **tu repositorio**. Abre estos archivos de uno en uno:

```hcl
# variables.tf: valor inicial
default = "desarrollo"

# main.tf: el recurso ficticio usa la variable
entorno = var.entorno
```

`outputs.tf` define el resumen previsto. `terraform_data` está integrado en OpenTofu: aquí solo calculamos un plan de una ficha, sin proveedores cloud. **Predicción:** si el valor inicial es `desarrollo`, ¿qué entorno debería mostrar el plan inicial? Escríbelo antes de consultar la IA.

En otra pestaña abre Copilot Chat en GitHub.com o ChatGPT. Puedes usar este prompt con **solo el código ficticio**:

> Explícame como principiante qué hacen `variables.tf`, `main.tf` y `outputs.tf` en este laboratorio. ¿Dónde se declara `entorno` y dónde se utiliza? ¿Qué mostrará un plan si el valor inicial es `desarrollo`? No propongas credenciales, proveedores cloud ni `tofu apply`. Dime cómo comprobar cada afirmación en el código o en Actions.

Compara la respuesta con los archivos. Si la IA dice que se ha creado una web real, corrígela: este laboratorio no aplica el plan.

## Paso 4 · Abre tu copia en VS Code Web y cambia un valor

1. En la dirección de **tu propia copia**, cambia solo `github.com` por `github.dev` y pulsa **Intro**. Por ejemplo, `https://github.dev/TU_USUARIO/iac-ia-practica-tuusuario`. Puede redirigirte a `vscode.dev`.
2. Si aparece una autorización de GitHub o Visual Studio Code, comprueba que está seleccionada **tu cuenta** y revisa los permisos antes de continuar. En el panel izquierdo del editor, pulsa **`variables.tf`**. Debe mostrar `default = "desarrollo"`.
3. Sustituye únicamente `desarrollo` por `pruebas`. La línea debe quedar **`default = "pruebas"`**, con ambas comillas. Guarda con **Ctrl+S** (en macOS, **Cmd+S**).
4. Pulsa **Control de código fuente / Source Control** en la barra de la izquierda (icono de rama). Comprueba que el único archivo modificado es `variables.tf`; púlsalo si quieres ver el antes y el después.
5. Escribe el mensaje **`Ejercicio 1: cambiar entorno a pruebas`**. Pulsa **Commit & Push** si aparece. Si ves **Commit** y luego **Sync Changes/Push**, realiza ambos. Si el editor te pide preparar el archivo, pulsa **+** junto a `variables.tf` y vuelve a confirmar.
6. Vuelve a `github.com` en **tu copia**. Abre `variables.tf`: ahora debe decir `pruebas`. Comprueba también que aparece tu nuevo commit. **Guardar no publica**; el commit registra una versión y Push la envía a GitHub.

**Si el editor web está bloqueado:** haz el mismo cambio en `github.com` dentro de **tu copia**: abre `variables.tf`, pulsa el lápiz **Edit this file**, cambia el valor y pulsa **Commit changes**. Así también se activa Actions. No necesitas clonar ni instalar nada.

## Paso 5 · Comprueba tu cambio en una ejecución nueva

1. En `github.com`, abre **Actions** en **tu copia**. Elige la ejecución cuyo título sea **`Ejercicio 1: cambiar entorno a pruebas`**. No abras **Commit inicial**: esa corresponde al valor anterior.
2. En la columna izquierda pulsa **comprobar**. Debe estar verde. En la zona de la derecha busca **Mostrar plan**. Si no está a la vista, desplázate hacia abajo **en esa zona**; los pasos abiertos encima pueden hacerlo quedar más abajo.
3. Pulsa la **flecha `>` a la izquierda de «Mostrar plan»**. En el texto desplegado busca `terraform_data.aplicacion`, dentro de `input` la línea `entorno = "pruebas"`, y `Plan: 1 to add, 0 to change, 0 to destroy`.

**Qué significa:** `tofu plan` anuncia lo que haría una aplicación posterior. El workflow no ejecuta `tofu apply`; no hay despliegue. Cada ejecución utiliza un ejecutor nuevo, por eso puede mostrar `1 to add` aunque hayas hecho planes anteriores. Una marca verde en **Validar** confirma que la configuración es válida; **Mostrar plan** enseña el efecto del valor cambiado.

## Reto de refuerzo · Un error que se puede corregir (20–30 min)

Cuando la ejecución de `pruebas` esté verde, crea **una rama en tu copia** desde `main` llamada `prueba-error-e1`. En esa rama quita la comilla final del valor `"pruebas"` en `variables.tf`, confirma y publica el cambio. En **Actions**, busca el nuevo commit: el trabajo debe fallar. Abre el **primer paso rojo**, lee el error y localiza la línea de `variables.tf`. Repón la comilla, confirma otra vez y comprueba una nueva ejecución verde. **No fusiones esa rama en `main`**; `main` debe conservar `pruebas` para el ejercicio 2.

Si aún no sabes crear una rama, la docente hará el primer intento en pantalla y puedes repetirlo en tu copia. El objetivo es interpretar el fallo y verificar la corrección, no memorizar botones.

## Comprueba que has terminado

- [ ] Tu URL empieza por `github.com/TU_USUARIO/` y el archivo `variables.tf` en `main` dice `pruebas`.
- [ ] Tu commit está publicado y su propia ejecución terminó en verde.
- [ ] Has localizado `entorno = "pruebas"` en **Mostrar plan**.
- [ ] Puedes explicar qué instala Actions, dónde lo instala y por qué el plan no ha desplegado una web.
- [ ] Sabes distinguir **Commit inicial** de la ejecución de tu cambio.

**Preguntas:** ¿En qué archivo se declara `entorno` y en cuál se usa? ¿Qué diferencia hay entre guardar, confirmar y publicar? ¿Qué comprobarías si Actions no se inicia? ¿Por qué `1 to add` no significa que ya exista un recurso real?

**Continúa con [el ejercicio 2](EJERCICIO_2.md) sobre la misma copia personal.** No crees otro repositorio.

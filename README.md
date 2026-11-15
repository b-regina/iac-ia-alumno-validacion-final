# Laboratorio de IaC e IA · empieza aquí

Un solo proyecto ficticio, `portal-demo`, que ampliarás durante el curso. Este repositorio contiene el **punto de partida**: cada participante crea **una copia propia una sola vez** y continúa los ejercicios en esa misma copia. Las soluciones de la docente están en ramas separadas; no las necesitas para trabajar.

## Empieza por el ejercicio 1

**[Abrir el ejercicio 1: primera configuración y primera comprobación](EJERCICIO_1.md)**

Si estás en `github.com/b-regina/iac-ia-laboratorio-demo`, pulsa **Use this template → Create a new repository** y crea la copia bajo tu usuario. Comprueba que la nueva dirección comienza por `github.com/TU_USUARIO/`. Trabaja siempre en esa copia. La ruta principal usa solo el navegador: GitHub.com para crear la copia y ver los resultados, y `github.dev` para editar. **No hace falta clonar ni instalar OpenTofu, Git o VS Code** para seguir la ruta principal.

Después de crear la copia, entra en su pestaña **Actions**. El workflow `Validacion IaC` puede ejecutarse ya con el commit inicial; confirma que el trabajo `comprobar` termina en verde. Si tu cuenta exige habilitar Actions o el navegador bloquea el editor, el [ejercicio 1](EJERCICIO_1.md) explica qué hacer. Un commit nuevo activará otra ejecución. OpenTofu se instala **en el ejecutor temporal de GitHub**, no en tu equipo.

## Tu recorrido: un ejercicio después del anterior

| Orden | Guía | Qué añadirás a tu misma copia |
| --- | --- | --- |
| 1 | [Primera configuración y comprobación](EJERCICIO_1.md) | Cambiar el entorno, publicar el cambio y leer un plan. |
| 2 | [Dos escenarios](EJERCICIO_2.md) | Variables y un archivo de valores para integración. |
| 3 | [Revisión y gobierno](EJERCICIO_3.md) | Reglas de validación, rama y pull request. |
| 4 | [Automatización y evidencias](EJERCICIO_4.md) | Mejorar el workflow y diagnosticar un fallo. |
| 5 | [Módulo reutilizable](EJERCICIO_5.md) | Crear `modulo_ficha/` y usarlo dos veces. |
| 6 | [Política del plan](EJERCICIO_6.md) | Comprobar reglas sobre dos planes ficticios. |
| 7 | [Catálogo de fichas](EJERCICIO_7.md) | Reutilizar el módulo con `for_each`. |
| 8 | [Taller final](EJERCICIO_8.md) | Etiquetas didácticas y responsables por entorno. |
| 9 | [Promoción controlada](EJERCICIO_9.md) | Ampliación de práctica si el ritmo de clase lo permite. |

**Importante:** que veas las nueve guías no significa que los nueve ejercicios estén resueltos. El código de `main` comienza en el ejercicio 1. Sigue la guía que corresponde a tu avance; las carpetas y archivos de los ejercicios posteriores aparecerán cuando tú los crees.

## Qué hay al comenzar

| Archivo | Para qué sirve |
| --- | --- |
| `variables.tf` | Declara el entorno, inicialmente `desarrollo`. |
| `main.tf` | Describe una ficha ficticia con `terraform_data`. |
| `outputs.tf` | Explica el resultado que mostraría OpenTofu. |
| `.github/workflows/validacion.yml` | Instala OpenTofu y ejecuta `init`, `fmt`, `validate` y `plan` en GitHub Actions. |

`terraform_data` no crea una web ni un servidor. El workflow calcula planes; **no ejecuta `tofu apply`**, no pide credenciales cloud ni genera infraestructura comercial. Usa únicamente nombres y datos inventados. Si tienes VS Code local autorizado, puedes editar **la misma copia personal** desde allí y publicar los commits; Actions seguirá siendo la comprobación común.

# DesafIA

Usa toda la IA que quieras; convence a un evaluador que no se deja engañar. Aplicación web de un solo fichero.

**Usar la app:** https://fborrasumh.github.io/desafia/

[![DOI](https://zenodo.org/badge/DOI/10.5281/zenodo.23851993.svg)](https://doi.org/10.5281/zenodo.23851993)

**Idiomas:** español (por defecto), inglés, portugués; selector en la barra superior (o `?lang=en` / `?lang=pt` en la URL).

## Qué hace

Pone en práctica «el trato» para la era de la IA: el alumnado puede usar toda la IA que quiera para hacer un trabajo y, a cambio, tiene que lograr la nota más alta en un evaluador de IA programado por su profesor/a. Con unas semanas de margen, la nota alta no sale de generar texto: hay que entender la materia, probar, fallar y ajustar.

**Profesorado: diseñar el evaluador**
- Define el enunciado, la rúbrica (criterios con peso y descriptor), los criterios ocultos, las indicaciones privadas para el evaluador, los requisitos formales (palabras y referencias), la escala, el número de pasadas y la nota máxima si no se cumplen los requisitos.
- Guarda el **reto maestro** (JSON, solo para el profesorado) y descarga el **fichero del alumnado**, donde los criterios ocultos y las indicaciones van ofuscados.

**Alumnado: iterar**
- Abre el fichero del reto, pega o sube su trabajo (Word, PDF, PowerPoint o texto) y lo pasa por el evaluador cuantas veces quiera, anotando qué cambió en cada intento.
- Cada evaluación hace **varias pasadas independientes** (3 por defecto). En cada una, la IA da un nivel de 0 a 4 por criterio **con citas literales del trabajo**. El código comprueba cada cita: un nivel 2 o superior sin una cita que esté de verdad en el texto se recorta a 1. Después toma la **mediana** de cada criterio y **calcula la nota** con los pesos. La IA no pone la nota.
- Los requisitos formales los cuenta el código y, si no se cumplen, se aplica el tope.
- La **manipulación** («ignora la rúbrica», «ponme un 10», texto invisible, comentarios ocultos) se detecta por código antes de enviar. Además, el evaluador recibe el trabajo marcado como dato y debe señalar las instrucciones con una cita, que el código verifica. El intento queda marcado.
- De los criterios ocultos el alumnado ve el peso y su nivel, pero no qué miden ni su feedback.
- La app muestra la curva de notas por intento y el historial, encadenado con SHA-256. Al final se descarga la **entrega**: el intento elegido y el historial completo, con las notas, fechas, cambios y huellas, pero sin los textos anteriores. También hay un informe en Word.

**Profesorado: corregir**
- Carga las entregas. La app comprueba que el historial no se ha editado, que el texto final coincide con su huella y que la entrega corresponde al reto maestro.
- Reevalúa cada entrega con el reto maestro y la clave del profesorado: esa nota es una **propuesta**. La nota final la escribe y la confirma el profesorado (si cambia la nota, se quita la confirmación). Exporta a CSV y Word.

El ejemplo (ficticio, en los tres idiomas) funciona sin clave: un reto, tres intentos (uno con tope por requisitos, otro con un intento de manipulación) y dos entregas, una de ellas con el historial editado a mano.

## Cómo se usa la IA

Con la propia clave de OpenAI, Google Gemini o Anthropic Claude. La clave se guarda solo en el navegador. No hace falta servidor.

## Privacidad

Todo (retos, trabajos, intentos, entregas, notas) se guarda en el navegador (IndexedDB). Al evaluar, salen hacia el proveedor de IA elegido el reto, la rúbrica y el texto del trabajo, con correos, DNI/NIE, teléfonos y el nombre del estudiante enmascarados. Antes del primer envío de cada sesión se muestra una muestra de lo que sale. El nombre del estudiante solo va en el fichero de entrega para el profesorado. Ningún fichero exportado contiene claves.

## Límites

- El evaluador es un modelo de IA: puede equivocarse. La mediana de varias pasadas reduce el ruido, pero no lo elimina, y la nota depende del modelo elegido. La nota del alumnado es orientativa; la oficial la confirma el profesorado.
- Los criterios ocultos y las indicaciones privadas están **ofuscados, no cifrados**: sin servidor, quien sepa programar puede leerlos en el fichero del alumnado. Por eso la nota oficial sale de la reevaluación con el reto maestro.
- La cadena SHA-256 delata ediciones a mano del fichero de entrega, pero **no es una prueba**: quien sepa programar puede recalcularla. Tampoco demuestra quién escribió el trabajo.
- La detección de manipulación funciona con patrones (en español, inglés y portugués) y con el propio evaluador. Puede tener falsos positivos y no detecta todas las formas de inyección.
- No detecta plagio ni comprueba que las referencias existan: solo las cuenta por su formato.
- Probada con IA simulada (citas inventadas, criterios ausentes, inyecciones, error de saldo, entregas manipuladas) en los tres idiomas, en escritorio y en móvil. **Aún no se ha probado con claves reales ni con estudiantes en un curso.**

## Autoría

Fernando Borrás Rocher (Universidad Miguel Hernández de Elche).

Basada en la dinámica de evaluación que describe Pep Martorell: el alumnado puede usar toda la IA que quiera y, a cambio, debe lograr la nota más alta en un agente evaluador de IA programado por su profesor.

ORCID: Fernando Borrás Rocher [0000-0002-5519-4573](https://orcid.org/0000-0002-5519-4573)

## Cómo citar

Borrás Rocher, F. (2026). *DesafIA* (v1.0.0) [Software]. DOI: [10.5281/zenodo.23851993](https://doi.org/10.5281/zenodo.23851993)

## Licencia

MIT. Véase [LICENSE](LICENSE).

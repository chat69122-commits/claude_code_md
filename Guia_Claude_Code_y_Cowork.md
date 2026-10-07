GUÍA PRÁCTICA EN ESPAÑOL

## Claude Code y Claude Cowork

Cómo funcionan, en qué se diferencian y cómo usarlos

## Qué encontrarás en esta guía

- El motor agéntico que comparten ambos productos

- Claude Code: instalación, CLAUDE.md, permisos, hooks, MCP y subagentes

- Cowork: tareas, carpetas, plugins, tareas programadas y seguridad

- Comparación lado a lado y árbol de decisión

- Casos de uso para estudiantes de ingeniería y analítica de datos

- Buenas prácticas, solución de problemas y glosario

Basada en la documentación oficial de Anthropic (consultada en octubre de 2026). Los productos cambian con frecuencia: confirma los detalles en support.claude.com y code.claude.com/docs.


## Contenido

## 1. Panorama general: Claude, Claude Code y Cowork

La familia de herramientas

Cuándo usar cada una en una frase

Del chat al agente

El ciclo planear, actuar, verificar

Superficies e instalación Primer uso CLAUDE.md, skills, MCP, subagentes, hooks y plugins Permisos y seguridad Flujo de trabajo recomendado

Requisitos y disponibilidad Cómo corre una tarea Instrucciones, plugins, tareas programadas y proyectos Seguridad, privacidad y límites

- 5. Comparación y árbol de decisión

- 6. Casos de uso para estudiantes de ingeniería y datos

- 7. Buenas prácticas para trabajar con agentes

- 8. Solución de problemas frecuentes

- 9. Glosario

- 10. Fuentes y próximos pasos

Si solo quieres decidir qué herramienta usar, ve directo al capítulo 5. Si vas a instalar algo hoy, lee el capítulo 3 (Claude Code) o el 4 (Cowork). Los capítulos 6 y 7 te dan ejemplos de prompts listos para adaptar.

## 2. El motor común: la arquitectura agéntica

## 3. Claude Code

## 4. Claude Cowork

## Cómo leer esta guía


## 1. Panorama general

Anthropic ofrece hoy varias formas de trabajar con Claude. Las tres que más se confunden son el chat de Claude, Claude Code y Claude Cowork. Las tres funcionan con los mismos modelos de Claude; lo que cambia es cuánta autonomía tiene Claude, a qué puede acceder y para qué tipo de trabajo está pensada la interfaz.

## 1.1 La familia de herramientas

|   | Chat de Claude | Claude Code | Claude Cowork |
| --- | --- | --- | --- |
| Pensado para | Conversar, pensar, | Desarrollo de software: leer y | Trabajo de conocimiento fuera |
|   | redactar, preguntar. Tú | editar código, ejecutar | del código: documentos, hojas |
|   | guías cada paso. | comandos, manejar git. | de cálculo, investigación, |
|   |   |   | archivos. |
| Dónde vive | Web, móvil y escritorio. Terminal, VS Code, JetBrains, |   | App de escritorio Claude |
|   |   | app de escritorio y web. | Desktop (macOS y Windows). |
|   |   |   | No está en web ni móvil. |
| Autonomía | Responde a cada | Alta: planea y ejecuta tareas | Alta: planea, divide en |
|   | mensaje. | de varios pasos. | subtareas y entrega resultados |
|   |   |   | terminados. |
| Acceso a tus | Solo lo que subes a la | Tu repositorio y tu terminal, | Solo las carpetas que conectas |
| archivos | conversación. | según los permisos que | explícitamente. |
|   |   | concedas. |   |
| Interfaz | Conversación. | Línea de comandos o | Interfaz gráfica, sin abrir la |
|   |   | extensiones de IDE. | terminal. |

## 1.2 Cuándo usar cada una, en una frase

- Chat: cuando quieres pensar o redactar con Claude y mantener el control de cada paso.

- Claude Code: cuando el resultado final es software (código que se versiona y se revisa).

- Cowork: cuando el resultado final es un documento, una hoja de cálculo, una presentación o archivos organizados, y prefieres no usar la terminal.

Anthropic describe a Cowork como la misma arquitectura agéntica de Claude Code, pero accesible desde Claude Desktop y sin abrir la terminal. Por eso entender uno te ayuda a entender el otro.

## Idea clave


## 2. El motor común: la arquitectura agéntica

## 2.1 Del chat al agente

Un chat tradicional funciona por turnos: tú escribes, el modelo responde y ahí termina su trabajo. Un agente, en cambio, recibe un objetivo y decide por sí mismo qué pasos dar para lograrlo: leer archivos, buscar información, ejecutar código, revisar el resultado y corregirse. Tanto Claude Code como Cowork funcionan así.

## 2.2 El ciclo planear, actuar, verificar

- 1. Planear: Claude analiza tu petición y arma un plan. Si el trabajo es complejo, lo divide en subtareas.

- 2. Actuar: usa herramientas para ejecutar cada paso (leer y escribir archivos, correr comandos, buscar en la web, llamar a conectores).

- 3. Verificar: revisa lo que produjo (por ejemplo, ejecuta las pruebas o relee el documento) y corrige lo que haga falta.

- 4. Entregar: deja el resultado en tu sistema de archivos o en tu repositorio y te resume lo que hizo.

## 2.3 Qué hace posible el ciclo

- Herramientas: operaciones de archivos, búsqueda, ejecución de comandos y acceso a la web. Claude Code las combina con un modelo que razona sobre el código.

- Contexto persistente: archivos de instrucciones (CLAUDE.md en Code; instrucciones globales y de carpeta en Cowork) que Claude lee para no empezar de cero cada vez.

- Conectores (MCP): un estándar para conectar a Claude con servicios externos como Google Drive, Jira o Slack.

- Subagentes: instancias de Claude que trabajan en paralelo o con contexto aislado y devuelven un resultado a la tarea principal.

Con un agente cambia tu rol: pasas de escribir cada instrucción a definir un buen objetivo, supervisar el plan y revisar el resultado. La calidad del resultado depende mucho de qué tan claro sea el objetivo y de qué tan bien configures el contexto.

## Para recordar


## 3. Claude Code

Claude Code es la herramienta agéntica de Anthropic para programar. Combina un modelo que razona sobre tu código con herramientas integradas para operar sobre archivos, buscar, ejecutar comandos y acceder a la web. Trabaja directamente con git, por lo que puede leer el estado de tu repositorio, hacer cambios y prepararlos para commit.

## 3.1 Superficies disponibles

Claude Code corre en varias superficies. Tu configuración (por ejemplo CLAUDE.md, ajustes y servidores MCP) funciona en todas, así que lo que configures en la terminal también te sirve en la app

de escritorio.

| Superficie | Para qué sirve |
| --- | --- |
| Terminal (CLI) | La versión con más funciones: editas archivos, ejecutas comandos y manejas todo |
|   | el proyecto desde la línea de comandos. |
| VS Code (y Cursor) | Extensión con diffs en línea, menciones con @, revisión de planes e historial de |
|   | conversación dentro del editor. |
| JetBrains | Integración con los IDE de JetBrains. |
| App de escritorio | Aplicación independiente para usar Claude Code fuera del IDE o la terminal, con |
|   | revisión visual de cambios. |
| Web (claude.ai/code) | Para iniciar tareas largas desde el navegador y continuarlas luego en el móvil o en |
|   | la terminal. |

La mayoría de las superficies requieren una suscripción a Claude o una cuenta de Anthropic Console. La terminal y VS Code también admiten proveedores de terceros.

## 3.2 Instalación

El método recomendado por la documentación es la instalación nativa. Estos son los comandos publicados para cada sistema:

```
\# macOS / Linux
curl -fsSL https://claude.ai/install.sh | bash
# Windows (PowerShell)
irm https://claude.ai/install.ps1 | iex
# Alternativas
brew install --cask claude-code
winget install Anthropic.ClaudeCode
```

También puedes instalarlo con apt, dnf o apk en Debian, Fedora, RHEL y Alpine. Para VS Code o Cursor, instala la extensión oficial de Anthropic desde el panel de extensiones.


## Consejo

Antes de ejecutar cualquier comando de instalación copiado de internet, verifica en la documentación oficial (code.claude.com/docs) que sigue siendo el método vigente. Los comandos pueden cambiar.

## 3.3 Primer uso

- 1. Abre una terminal y entra a la carpeta de tu proyecto (por ejemplo, cd mi-proyecto).

- 2. Escribe claude. En el primer uso te pedirá iniciar sesión.

- 3. Pídele que explore: «Explícame la estructura de este proyecto y cómo se ejecuta».

- 4. Pide un cambio pequeño y concreto: «Corrige el error cuando el campo email está vacío».

- 5. Revisa los cambios propuestos antes de aceptarlos y, si todo está bien, pídele que haga el commit.

Para ir más lejos, la documentación oficial incluye una guía rápida (Quickstart) que recorre una primera tarea real: desde explorar un repositorio hasta confirmar una corrección.

## 3.4 El sistema de extensión de Claude Code

Claude Code se personaliza con varios mecanismos. Cada uno resuelve un problema distinto, y elegir el correcto evita configuraciones confusas.

| Mecanismo | Qué hace | Ejemplo |
| --- | --- | --- |
| CLAUDE.md | Contexto persistente que Claude lee en | Convenciones del proyecto, comandos de |
|   | cada sesión. | prueba, reglas de estilo. |
| Skills | Instrucciones y flujos de trabajo que Claude | Un comando /deploy que ejecuta tu lista de |
|   | carga cuando hacen falta. | despliegue. |
| MCP | Conecta a Claude con servicios y | Leer documentos de diseño en Google Drive |
|   | herramientas externas. | o actualizar tickets en Jira. |
| Subagentes | Trabajan con contexto aislado y devuelven | Un revisor de código que no ensucia la |
|   | un resultado. | conversación principal. |
| Hooks | Ejecutan tu script u otra acción en eventos | Correr el linter después de cada edición. |
|   | del ciclo de vida. |   |
| Plugins | Empaquetan skills, hooks, subagentes y | Un paquete de herramientas para tu equipo. |
|   | servidores MCP en una unidad instalable. |   |

## Regla práctica

Si Claude se equivoca dos veces en una convención o comando, agrégala a CLAUDE.md. Si necesitas que algo ocurra siempre y sin excepciones, usa un hook o un permiso, no solo una instrucción.


## 3.5 CLAUDE.md a fondo

CLAUDE.md es un archivo de texto en la raíz de tu proyecto que Claude lee al inicio de cada sesión. Los archivos de varios niveles se suman: todos aportan contenido al contexto al mismo tiempo. Por ejemplo, puedes tener preferencias globales en tu carpeta de usuario, convenciones del proyecto en la raíz y reglas específicas en subcarpetas (útil en repositorios con varios módulos).

## Qué conviene incluir

- Cómo construir, ejecutar y probar el proyecto (los comandos exactos).

- Convenciones de código y de nombres que no sean obvias.

- Decisiones de arquitectura importantes y carpetas clave.

- Cosas que Claude no debe tocar o advertencias frecuentes.

## Cuánto debe medir

La documentación recomienda mantener CLAUDE.md por debajo de unas 200 líneas. Si crece mucho, mueve el material de referencia a skills o a archivos separados que puedas importar con la sintaxis @ruta.

## Ejemplo mínimo

```
\# Proyecto: App web de convocatorias
## Comandos
- Instalar: npm install
- Pruebas: npm test
- Servidor local: npm run dev
## Convenciones
- TypeScript estricto; evitar 'any'.
- Componentes en src/components, uno por archivo.
- Mensajes de commit en español, en presente.
## No hacer
- No editar archivos dentro de /migrations sin pedir confirmación.
```

## 3.6 Permisos y seguridad

Claude Code puede ejecutar comandos y modificar archivos, así que su modelo de seguridad es importante. La clave es distinguir entre instrucciones y mecanismos que se hacen cumplir:

| Tipo | Ejemplos | Garantía |
| --- | --- | --- |
| Instrucciones | Tu prompt, CLAUDE.md, skills. | Moldean lo que Claude intenta hacer, pero |
| (piden) |   | no cambian lo que Claude Code permite. |
| Cumplimiento | Permisos (deny / ask) y hooks. | Se aplican siempre que la condición |
| (obligan) |   | coincide. |


Por ejemplo, escribir «nunca edites .env» en CLAUDE.md es una petición, mientras que un hook que bloquea esa edición antes de que ocurra es una garantía. Claude Code usa además aislamiento (sandboxing) como defensa en profundidad: los permisos impiden que Claude intente acceder a recursos restringidos, y el sandbox limita lo que puede hacer el comando aunque se ejecute.

- Revisa los planes y los cambios antes de aceptarlos, sobre todo al inicio.

- Empieza con permisos restrictivos y amplíalos con el tiempo.

- Trabaja sobre una rama de git para poder descartar cambios fácilmente.

- Evita dar acceso a credenciales o a datos sensibles que no necesites para la tarea.

## 3.7 Integraciones y modos de uso

| Quiero… | Mejor opción |
| --- | --- |
| Empezar una tarea local y seguirla en el | Web o app móvil de Claude |
| móvil |   |
| Pasar una tarea larga de la web a mi | Comando claude --teleport (requiere suscripción de |
| terminal | claude.ai) |
| Revisar cambios visualmente | Pasar la sesión a la app de escritorio con /desktop |
| Ejecutar algo de forma recurrente | Routines o tareas programadas de escritorio |
| Depurar aplicaciones web en vivo | Integración con Chrome |

Claude Code también se integra con flujos de CI/CD y con herramientas de chat, y es composable: sigue la filosofía de Unix, por lo que puedes encadenarlo con otros comandos y scripts.

## 3.8 Flujo de trabajo recomendado

- 1. Explora primero: pide un resumen del proyecto y de la zona que vas a tocar.

- 2. Planea: pide un plan antes de editar y corrígelo si hace falta.

- 3. Implementa en pasos pequeños: un cambio, una prueba, una revisión.

- 4. Verifica: que corra las pruebas y revisa el diff completo.

- 5. Registra lo aprendido: si descubriste una convención, añádela a CLAUDE.md.

- 6. Confirma: haz el commit solo cuando entiendas todos los cambios.


## 4. Claude Cowork

Cowork lleva las capacidades agénticas de Claude Code a Claude Desktop para trabajo de conocimiento más allá de programar. En lugar de responder una instrucción a la vez, Claude asume tareas complejas de varios pasos y las ejecuta por ti. La idea es que describas un resultado, te alejes y regreses a trabajo terminado: documentos con formato, archivos organizados o investigación sintetizada.

## 4.1 Requisitos y disponibilidad

- Plan de pago: Pro, Max, Team o Enterprise.

- App de escritorio: Claude Desktop para macOS o Windows (con la versión más reciente en Windows). No está disponible en web ni en móvil.

- Conexión a internet: necesaria durante toda la sesión.

- App abierta: Claude Desktop debe permanecer abierta y el equipo despierto mientras Claude trabaja; si la cierras, la sesión termina.

Para entrar, abre Claude Desktop, busca el selector de modo que incluye Chat y la pestaña Cowork, haz clic en Cowork, describe la tarea, revisa el enfoque que propone Claude y déjalo correr.

## 4.2 Cómo corre una tarea

Cowork se ejecuta directamente en tu computador y Claude accede a los archivos que decidas compartir. El código se ejecuta en un espacio aislado, pero Claude sí puede hacer cambios reales en tus archivos. Al iniciar una tarea, Claude:

- 1. Analiza tu petición y crea un plan.

- 2. Divide el trabajo complejo en subtareas cuando es necesario.

- 3. Ejecuta código y comandos de shell en una máquina virtual (VM) aislada en tu computador.

- 4. Coordina varios flujos de trabajo en paralelo si corresponde.

- 5. Entrega los resultados directamente en tu sistema de archivos.

Durante el proceso ves indicadores de progreso, el razonamiento de Claude y puedes intervenir para corregir el rumbo en cualquier momento.

## 4.3 Capacidades clave

| Capacidad | Descripción |
| --- | --- |
| Acceso local a archivos | Lee y escribe en tus archivos locales sin subir ni descargar manualmente. |
| Coordinación de | Divide el trabajo complejo y coordina tareas en paralelo. |
| subagentes |   |
| Entregables profesionales | Hojas de Excel con fórmulas que funcionan, presentaciones de PowerPoint y |
|   | documentos con formato. |


| Capacidad | Descripción |
| --- | --- |
| Tareas de larga duración | Trabaja por periodos largos sin que se corten por tiempo o por límites de |
|   | contexto de la conversación. |
| Tareas programadas | Guarda tareas para ejecutarlas bajo demanda o con una cadencia |
|   | automática. |
| Proyectos | Espacios de trabajo persistentes con sus propios archivos, enlaces, |
|   | instrucciones y memoria. |
| Acceso desde el móvil | En Pro y Max, envías mensajes desde el teléfono mientras Claude trabaja en |
|   | tu escritorio. |

## 4.4 Instrucciones globales y de carpeta

Cowork tiene dos niveles de contexto persistente, equivalentes a lo que CLAUDE.md hace en Claude

Code:

- Instrucciones globales: se aplican a todas las sesiones de Cowork. Úsalas para tu tono preferido, formato de salida o contexto sobre tu rol. Se configuran en Ajustes, sección Cowork, de Claude Desktop.

- Instrucciones de carpeta: añaden contexto específico cuando seleccionas una carpeta local. Claude también puede actualizarlas por su cuenta durante una sesión.

## 4.5 Plugins

Los plugins personalizan cómo trabaja Claude para tu rol, equipo y empresa. Cada uno agrupa skills, conectores y subagentes en un solo paquete.

## 4.6 Tareas programadas

Puedes crear tareas que Claude ejecute automáticamente o bajo demanda. Para programar una, escribe /schedule en cualquier tarea de Cowork, o usa la sección «Scheduled» de la barra lateral para ver, crear y gestionar las que ya tienes.

Las tareas programadas solo se ejecutan mientras tu computador está despierto y la app Claude Desktop está abierta.

## Limitación importante

## 4.7 Proyectos

Los proyectos de Cowork permiten agrupar tareas relacionadas en espacios de trabajo separados, cada uno con sus archivos, contexto, instrucciones y memoria. Son ideales para trabajo recurrente o de largo plazo, como un trabajo final, un curso o un proceso que repites cada semana.


## 4.8 Seguridad y privacidad

Cowork funciona con protecciones por capas, pero tiene riesgos propios por ser agéntico y tener acceso a internet. Lo esencial:

- Aislamiento de código: los comandos y el código que Claude escribe se ejecutan en una VM aislada de tu sistema operativo.

- Acceso controlado: Claude solo lee y escribe en las carpetas que conectaste, y el acceso de red respeta tus permisos de salida (egress).

- Protección contra borrado: Claude necesita tu permiso explícito antes de eliminar archivos de forma permanente.

- Datos locales: el historial de conversaciones se guarda en tu computador, por lo que no está sujeto al plazo de retención de datos de Anthropic.

- Sin auditoría: la actividad de Cowork no queda en los registros de auditoría, la API de cumplimiento ni las exportaciones de datos. La documentación indica no usarlo para cargas de trabajo reguladas.

- Conectores y web: los permisos de red no se aplican a la búsqueda web ni a los MCP; evalúa cuánto confías en un conector o sitio antes de darle acceso.

Revisa el plan de Claude antes de permitir que avance, sobre todo si hay archivos sensibles en la carpeta. Conecta únicamente las carpetas necesarias para la tarea.

## Buena práctica

## 4.9 Límites actuales y consumo de uso

- La memoria funciona dentro de proyectos, pero no se conserva entre sesiones independientes de Cowork.

- No se pueden compartir sesiones con otras personas.

- Requiere la app de escritorio, abierta y con el equipo despierto.

- Cowork consume más de tu cuota de uso que el chat, porque las tareas de varios pasos requieren más cómputo.

Para cuidar tu cuota, agrupa trabajo relacionado en una misma sesión, usa el chat normal para tareas simples que no necesitan archivos y revisa tu consumo en Ajustes, sección Uso.


## 5. Comparación y árbol de decisión

## 5.1 Claude Code frente a Cowork

| Aspecto | Claude Code | Cowork |
| --- | --- | --- |
| Público principal | Desarrolladores y personas cómodas con | Personas que hacen trabajo de |
|   | la terminal. | conocimiento, sin necesidad de código. |
| Resultado típico | Código, commits, pruebas, cambios en un | Documentos, hojas de cálculo, |
|   | repositorio. | presentaciones, archivos organizados, |
|   |   | investigación. |
| Interfaz | Terminal, IDE, escritorio y web. | Interfaz gráfica dentro de Claude Desktop. |
| Contexto | CLAUDE.md, skills, hooks, plugins, | Instrucciones globales y de carpeta, |
| persistente | memoria. | plugins, proyectos. |
| Aislamiento | Permisos, hooks y sandbox. | VM aislada, carpetas conectadas, |
|   |   | protección contra borrado. |
| Control | Más profundo y más configurable. | Valores por defecto más seguros y |
|   |   | accesibles. |
| Programación de | Routines y tareas programadas de | /schedule dentro de Cowork. |
| tareas | escritorio. |   |
| Disponibilidad | Suscripción de Claude o cuenta Console | Solo planes de pago, en app de escritorio. |
|   | (según superficie). |   |

Hay solapamiento: el análisis de datos, la investigación web y la generación de reportes se pueden hacer en cualquiera de los dos. En esos casos, decide por tu preferencia de interfaz y por si el entregable final es código o un documento.

## 5.2 Árbol de decisión

- 1. ¿El entregable es código que irá a un repositorio? Usa Claude Code.

- 2. ¿El entregable es un documento, una hoja de cálculo, una presentación o una carpeta ordenada? Usa Cowork.

- 3. ¿Solo quieres conversar, pensar o redactar con control total de cada paso? Usa el chat.

- 4. ¿No estás seguro? Empieza con Cowork si no te gusta la terminal, o con Claude Code si ya programas, y cambia cuando necesites más control.

## 5.3 Cómo se combinan

Un mismo proyecto puede usar las tres herramientas. Por ejemplo: pensar el diseño de una aplicación en el chat, construirla en Claude Code y resolver el trabajo operativo alrededor (resumen de requisitos, informes recurrentes, organización de evidencias) en Cowork.


## 6. Casos de uso para estudiantes de ingeniería y datos

Estos ejemplos están pensados para el trabajo académico de un estudiante de ingeniería de sistemas o analítica de datos. Los prompts son ejemplos para adaptar; ajusta nombres de archivos y detalles a

tu caso.

## 6.1 Con Claude Code

## a) Entender un repositorio nuevo

Explícame la estructura de este proyecto, las tecnologías que usa y cómo se ejecuta localmente. Luego dime qué archivos debería leer primero para entender el flujo de autenticación.

## b) Construir una aplicación web por módulos

Vamos a construir una app web de postulaciones. Primero propón un plan modular con el stack, las entidades y los roles de usuario. No escribas código todavía; espera mi aprobación.

## c) Escribir pruebas y corregir errores

Ejecuta las pruebas, identifica las que fallan y explica la causa de cada una. Corrige solo la primera y muéstrame el diff antes de continuar.

## d) Documentar el proyecto para la entrega

Genera un README en español con instrucciones de instalación, variables de entorno, estructura de carpetas y ejemplos de uso, a partir del código actual.

## 6.2 Con Cowork

## a) Organizar entregables y material de cursos

Organiza esta carpeta por materia y semestre, renombra los archivos con el formato AAAA-MM-DD_materia_descripcion y crea un índice en una hoja de cálculo.

## b) Analizar un conjunto de datos

Limpia este CSV, detecta valores atípicos, haz un análisis descriptivo y entrega un Excel con tablas dinámicas y dos gráficos que resuman los hallazgos principales.


## c) Sintetizar investigación para un trabajo

Lee los artículos de la carpeta /fuentes, extrae la pregunta, el método y las conclusiones de cada uno y arma una tabla comparativa. Marca dónde no coinciden.

## d) Preparar una presentación a partir de notas

Con mis notas de la carpeta /caso-empresa, crea una presentación de 10 diapositivas con el problema, el análisis, la propuesta y las conclusiones. Incluye notas del orador.

## 6.3 Trabajo recurrente

- Resumen semanal: una tarea programada en Cowork que revise tu carpeta de apuntes y arme un resumen de pendientes.

- Preparación de exámenes o certificaciones: un proyecto de Cowork con tus apuntes y temario; pídele resúmenes, tarjetas de estudio y preguntas de práctica.

- Proyecto de curso: un CLAUDE.md con las reglas del proyecto, para que Claude Code mantenga convenciones coherentes entre sesiones.

Revisa las políticas de tu universidad sobre uso de IA en trabajos. Usa estas herramientas para aprender, organizar y verificar, y asegúrate de entender y poder explicar todo lo que entregues.

## Integridad académica

## 7. Buenas prácticas para trabajar con agentes

## 7.1 Escribe objetivos claros

- Describe el resultado esperado, no solo la tarea («un Excel con tres hojas: datos limpios, resumen y gráficos»).

- Indica restricciones: formato, extensión, idioma, qué no tocar.

- Da criterios de éxito: «las pruebas deben pasar» o «la tabla debe sumar el total de la fuente».

- Pide un plan primero en tareas grandes y apruébalo antes de que ejecute.

## 7.2 Trabaja en pasos pequeños

Dividir el trabajo en bloques revisables reduce errores y te permite corregir pronto. Con Claude Code, un cambio por vez con su prueba. Con Cowork, entregas parciales (primero la estructura, luego el contenido, luego el formato).


## 7.3 Configura el contexto una vez

- Escribe un CLAUDE.md corto y útil; actualízalo cuando Claude se equivoque en lo mismo.

- En Cowork, usa instrucciones globales para tu tono y formato, e instrucciones de carpeta para cada proyecto.

- Usa skills para flujos que repites con frecuencia.

## 7.4 Verifica siempre

- Revisa el diff y ejecuta las pruebas por tu cuenta.

- Si hay cifras, comprueba una muestra contra la fuente original.

- Desconfía de resultados demasiado perfectos: pregúntale a Claude cómo verificó su trabajo.

- Mantén copias o control de versiones antes de dejar que modifique archivos importantes.

## 7.5 Cuida la seguridad

- Da acceso solo a las carpetas y herramientas necesarias.

- Trata con cautela el contenido que viene de internet o de archivos de terceros: puede contener instrucciones que no vienen de ti.

- No pongas contraseñas ni datos personales de otras personas en los archivos que Claude procesa si no es indispensable.

- Recuerda que Cowork no deja registros de auditoría: no es apto para cargas de trabajo reguladas.

## 8. Solución de problemas frecuentes

| Problema | Qué revisar |
| --- | --- |
| Cowork se detuvo a mitad de | Confirma que Claude Desktop estuvo abierta todo el tiempo y que el |
| una tarea | equipo no se suspendió. |
| Llego rápido a los límites de uso | Cowork consume más que el chat. Agrupa trabajo relacionado, usa el |
|   | chat para tareas simples y revisa Ajustes, sección Uso. |
| No encuentro los archivos que | Verifica los permisos de carpeta y la ubicación de salida que Claude |
| generó | indicó al terminar. |
| Aparece «Setting up Claude's | Es normal: indica que Cowork se está actualizando a la versión más |
| workspace» al iniciar Cowork | reciente. |
| En Windows: «VM service not | Puede ocurrir si instalaste con el instalador antiguo. Reinstala desde la |
| running» | página de descargas o inicia el servicio Claude VM. |
| En Windows: «EXDEV: | Suele pasar cuando el almacenamiento de contenido nuevo apunta a |
| cross-device link not permitted» | otra unidad (por ejemplo D:). Vuelve a C:, reinstala y actualiza. |


| Problema | Qué revisar |
| --- | --- |
| Claude Code ignora una regla de | Es una instrucción, no una garantía. Si debe cumplirse siempre, |
| mi CLAUDE.md | conviértela en permiso o en hook. Revisa también que el archivo sea |
|   | corto y claro. |
| No puedo usar Cowork | Comprueba que tu plan sea de pago, que uses la app de escritorio |
|   | actualizada y que tu equipo cumpla los requisitos. |

## 9. Glosario

| Término | Significado |
| --- | --- |
| Agente | Sistema que recibe un objetivo, decide los pasos, usa herramientas y verifica |
|   | su propio trabajo. |
| Agéntico | Que funciona como un agente: planea y ejecuta tareas de varios pasos con |
|   | cierta autonomía. |
| CLAUDE.md | Archivo de contexto persistente que Claude Code lee al inicio de cada sesión. |
| Conector | Integración que permite a Claude acceder a un servicio externo. |
| MCP (Model Context | Estándar para conectar Claude con servicios y herramientas externas. |
| Protocol) |   |
| Subagente | Instancia de Claude con contexto aislado o que trabaja en paralelo y devuelve |
|   | un resultado. |
| Skill | Conjunto de instrucciones y flujos reutilizables que Claude carga cuando los |
|   | necesita. |
| Hook | Acción automática (script, solicitud HTTP, etc.) que se dispara en un evento del |
|   | ciclo de vida. |
| Plugin | Paquete que agrupa skills, conectores, hooks y subagentes. |
| VM (máquina virtual) | Entorno aislado donde Cowork ejecuta el código y los comandos. |
| Egress | Tráfico de red saliente; los permisos de egress controlan a qué sitios puede |
|   | conectarse el entorno. |
| Sandbox | Entorno restringido que limita lo que un comando puede hacer en tu sistema. |
| Diff | Comparación de lo que cambió entre dos versiones de un archivo. |
| Commit | Registro de cambios confirmados en un repositorio git. |
| Contexto | Información que Claude tiene disponible para responder en un momento dado. |


## 10. Fuentes y próximos pasos

## 10.1 Fuentes oficiales

- Centro de ayuda de Anthropic, artículo sobre Claude Cowork: https://support.claude.com/articles/13345190

- Documentación de Claude Code, visión general: https://code.claude.com/docs/en/overview

- Documentación de Claude Code, cómo extenderlo (CLAUDE.md, skills, MCP, subagentes, hooks): https://code.claude.com/docs/en/features-overview

## 10.2 Material de apoyo consultado

- Comparativas y guías de terceros sobre Claude Code y Cowork (por ejemplo HatchWorks, Parallel y DEV Community). Son útiles para ver ejemplos, pero conviene contrastarlas con la documentación oficial.

## 10.3 Próximos pasos sugeridos

- 1. Si programas: instala Claude Code, abre un proyecto pequeño y sigue el Quickstart oficial.

- 2. Escribe tu primer CLAUDE.md con comandos y convenciones, de máximo unas 200 líneas.

- 3. Si usas Cowork: crea instrucciones globales con tu tono y formato preferidos.

- 4. Prueba una tarea de bajo riesgo (organizar una carpeta de copias) y observa cómo planea y ejecuta Claude.

- 5. Crea un proyecto de Cowork para tu trabajo más recurrente y, cuando lo domines, programa una tarea con /schedule.

Esta guía resume la documentación oficial disponible en octubre de 2026. Las funciones, los planes y los límites cambian con frecuencia; verifica siempre en support.claude.com y code.claude.com/docs antes de tomar decisiones que dependan de un detalle específico.

## Aviso

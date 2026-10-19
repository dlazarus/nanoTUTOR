# nanoTUTOR

Un **system prompt de tutoría personal** para usar con cualquier agente de IA — o directamente pegado en un chat convencional.

nanoTUTOR no es una máquina de hacer deberes ni un examinador: es un **tutor** cuyo objetivo es que la alumna entienda, recuerde y llegue a hacerlo sola. Está calibrado para una alumna de 2º de ESO (12-13 años, currículo español), pero su método es general y adaptable (ver [Cómo usarlo](#cómo-usarlo)).

> El fichero [`nanoTUTOR.md`](nanoTUTOR.md) es el prompt completo: 137 líneas, ~11 KB, 13 secciones y 4 diálogos de ejemplo. Es texto puro: no requiere ninguna herramienta ni framework.

## En qué se apoya el diseño

El prompt aplica de forma explícita principios de ciencias del aprendizaje con amplio respaldo empírico:

- **Instrucción explícita para novatos.** La guía mínima (descubrimiento puro) no funciona con principiantes: la memoria de trabajo se desborda resolviendo en vez de aprendiendo (Kirschner, Sweller & Clark, 2006). nanoTUTOR explica y modela antes de preguntar.
- **Andamiaje que se retira** (*gradual release of responsibility*): el tutor **modela** (lo hace él pensando en voz alta), **acompaña** (lo hacen a medias) y **se retira** (lo hace ella sola). La ayuda se retira poco a poco; no se niega ni se regala.
- **Ejemplos resueltos con desvanecimiento** (*worked examples + fading*): estudiar ejemplos resueltos supera a resolver problemas en las fases iniciales, y la guía debe ir retirándose paso a paso a medida que crece la pericia (Sweller; Renkl; Pashler et al.).
- **Ni dependencia ni muro.** Dar sistemáticamente la respuesta a los ejercicios propios genera aprendizaje dependiente (Bastani et al., PNAS 2024; Aleven & Koedinger, 2000), pero negar la respuesta de forma absoluta (socratismo estricto) no mejora el aprendizaje y se percibe como menos útil (Blasco & Charisi, 2024). De ahí la **escalera de ayuda de 6 peldaños**: sube un peldaño por turno y llega hasta la solución explicada — a condición de que ella haga después un ejercicio parecido nueva.
- **Práctica de recuperación, espaciado e intercalado**: recuperar antes que releer es de las intervenciones mejor soportadas en contenidos escolares reales (Kang et al., 2021, 2022). El repaso empieza siempre con un intento de recuerdo; los resúmenes nunca van antes del intento.
- **Elogio de proceso, no de capacidad**: elogiar la inteligencia aumenta la fragilidad tras el fracaso; elogiar el proceso sostiene la persistencia (Mueller & Dweck, 1998). Prohibido el "eres muy lista" vacío.
- **Aspiración de tutoría 1:1**: la tutoría individual es el efecto documentado más potente en educación (Bloom, "2 Sigma", 1984); el formato y la calidad de la interacción importan mucho (Kulik & Fletcher, 2016; Nickow et al., 2024).

## Características

- **Regla de oro anti-deberes**: no resuelve el ejercicio que la alumna trae; resuelve uno **parecido** (misma estructura, otros datos) y ella hace el suyo con ayuda. No produce entregas ni productos de exámenes evaluables.
- **Escalera de ayuda (un peldaño por turno)**: pregunta guía abierta → pregunta guía cerrada → analogía cotidiana → ejemplo parecido resuelto → versión mínima o pasos iniciados → solución completa explicada + ejercicio nuevo que hace ella sola.
- **Método "un turno = una idea + una pregunta"**: explicar poco y concreto, ejemplo antes que definición, modelar pensando en voz alta, verificar comprensión (y si no entiende, *cambiar* la explicación, no repetirla), retirar ayuda al confirmar dominio.
- **Diagnóstico tipado del error**: conceptual (analogy + ejemplo), procedimental (micro-ejercicios del paso que falla) o *lapsus* (señalamiento breve y neutro). Ante duda, una pregunta que distinga. Nunca dice "incorrecto": dice qué está bien, dónde falla y cómo corregir.
- **Modo repaso deliberado**: recuperar antes que releer, 2-3 ejercicios por racha, variar la superficie (números, contexto, orden), intercalar temas anteriores, cierre de sesión con 2-3 preguntas, resúmenes con autoevaluación y plan de repaso para exámenes.
- **Formato duro**: párrafos de máximo 3 líneas, una idea cada vez, negritas para conceptos clave, sin muros de texto.
- **Estilo emocional**: cercano sin infantilizar; elogio específico de proceso; gestión de la frustración (reducir a un paso pequeño) y del auto-descenso ("soy tonta" → el error informa, no define).
- **Precisión escolar anti-alucinación**: no inventa lo que dice el libro de texto, lo que explicó el profesor ni la normativa autonómica; distingue explicación general de lo que depende de los apuntes; revisa sus propios cálculos; no promete notas.
- **Adaptación por materia**: recetas distintas para Matemáticas, Ciencias, Lengua/idiomas (conservando la voz de la alumna al corregir), Historia/Geografía y resto de asignaturas.
- **Fuera de nivel**: gestiona temas por encima (Bachillerato/EBAU) sin penalizar por adelantarse, bases por debajo (Primaria) sin bajar el tono, y temas profesionales derivándolos.
- **Raíles de seguridad**: redirige jailbreaks, neutralidad en temas sensibles, no pide datos personales innecesarios, protocolo ante señales de peligro, y **no finge memoria entre sesiones** (ofrece un resumen copiable para la siguiente sesión).
- **4 diálogos de ejemplo** que instancian el método: modelar y retirar, presión por la respuesta (ceder en forma, no en sustancia), lapsus, y repaso con recuperación previa.

## Cómo usarlo

**1. Chat convencional.** Copia el contenido de `nanoTUTOR.md` y pégalo como primer mensaje (o en el campo "instrucciones personalizadas" si el chat lo tiene). Funciona en cualquier modelo conversacional.

**2. System prompt en una API.** Usa el fichero completo como `system`/`instructions` de tu agente:

```python
system_prompt = open("nanoTUTOR.md").read()
```

**3. Como rol en [pi](https://pi.dev)** (con [pi-roles](https://github.com/dlazarus/pi-roles)): copia `nanoTUTOR.md` a `~/.pi/roles/` y actívalo con `/rol nanoTUTOR` o `pi --rol nanoTUTOR`.

**4. Adaptarlo a otra persona o curso.** El fichero está calibrado para una alumna concreta (nombre, 2º de ESO, materias LOMLOE). Para reutilizarlo: cambia el nombre y el curso en la sección *Contexto y rol* y ajusta la sección *Materias*. El método (escalera, diagnóstico, repaso, formato) no depende del curso.

> Nota: el prompt se envía íntegro en cada sesión (~11 KB). En modelos con ventana de contexto ajustada, puede convenir una versión recortada conservando regla de oro, escalera, diagnóstico y repaso.

## Límites honestos

- El prompt es una **hipótesis de diseño razonada**, no un resultado validado: la evidencia citada es sobre instrucción humana y tutores inteligentes en general, no sobre este prompt concreto.
- El cumplimiento del método puede degradarse en sesiones largas (el modelo acaba dando la respuesta o acumulando preguntas). Los diálogos de ejemplo ayudan, pero no garantizan.
- **Sin memoria entre sesiones** por diseño: el espaciado real entre días depende de copiar y pegar el resumen de cierre.
- No evalúa comprensión conceptual profunda ni detecta lagunas de cursos anteriores salvo que afloren en la conversación.

## Estructura

```
nanoTUTOR/
├── nanoTUTOR.md   # el system prompt (texto puro, portable)
└── README.md
```

## Licencia

AGPL-3.0-only — Copyright (C) 2026 dlazarus.

Este prompt es software libre: puede redistribuirlo y/o modificarlo bajo los términos de la [GNU Affero General Public License](https://www.gnu.org/licenses/agpl-3.0.html) publicada por la Free Software Foundation (versión 3).

Se distribuye sin garantía de ningún tipo. Los trabajos derivados que se expongan a usuarios por una red deben publicar también su código fuente.

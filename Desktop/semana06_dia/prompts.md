# Biblioteca de prompts — Laboratorio 06 (semana06_dia)

## FASE 1 — Prompt vago vs. prompt estructurado

### Prueba 1.1 — Prompt vago
**Herramienta:** ChatGPT / Claude / Gemini
**Prompt:**
> Escribe un correo pidiendo más plazo para un trabajo.

**Resultado (resumen):**
Genera un correo genérico con campos entre corchetes, de extensión mediana y con un tono algo impersonal.

### Prueba 1.2 — Prompt estructurado
**Herramienta:** ChatGPT / Claude / Gemini
**Prompt:**
> # Rol
> Actúa como un estudiante universitario que se comunica de forma formal y respetuosa.
> # Contexto
> Debo entregar el informe del proyecto final del curso de Diseño de Interfaces el viernes, pero dos integrantes del equipo estuvieron enfermos esta semana.
> # Tarea
> Redacta un correo al docente solicitando una prórroga de 3 días.
> # Formato de salida
> Incluye asunto, saludo, cuerpo en máximo 2 párrafos y despedida.
> # Restricciones
> No exageres la situación, no uses más de 120 palabras y propone una nueva fecha concreta.

**Resultado (resumen):**
Un correo directo de menos de 100 palabras, que propone explitícamente el lunes como nueva fecha de entrega, manteniendo un tono formal.

**Observaciones y diferencias:**
1. **Especificidad:** El prompt estructurado fijó la fecha exacta de prórroga (lunes), mientras que el vago dejó espacios en blanco.
2. **Concisión y Formato:** El estructurado cumplió con el límite de palabras y la estructura de 2 párrafos requerida.
3. **Tono:** El prompt estructurado ajustó el tono respetuoso sin sonar melodramático ni exagerar.

---

## FASE 2 — Zero-shot y few-shot

### Prueba 2.1 — Clasificación con zero-shot
**Prompt:**
> Clasifica cada comentario como POSITIVO, NEGATIVO o NEUTRO.
> 1. "La app se cierra cada vez que intento pagar."
> 2. "Llegó el pedido, nada que destacar."
> 3. "Me encantó lo rápido que cargan las pantallas."
> 4. "Está bien, aunque el botón de ayuda es difícil de encontrar."

**Resultado:**
1. NEGATIVO
2. NEUTRO
3. POSITIVO
4. NEUTRO / NEGATIVO

### Prueba 2.2 — Clasificación con few-shot
**Prompt:**
> Clasifica cada comentario siguiendo el formato de los ejemplos.
> 
> Comentario: "Excelente diseño, todo es muy intuitivo."
> Categoría: POSITIVO | Tema: diseño
> 
> Comentario: "Buen precio, pero la entrega tardó una semana."
> Categoría: MIXTO | Tema: entrega
> 
> Comentario: "La app se cierra cada vez que intento pagar."
> Categoría:
> 
> Comentario: "Está bien, aunque el botón de ayuda es difícil de encontrar."
> Categoría:

**Resultado:**
- Comentario 3: Categoría: NEGATIVO | Tema: pago / estabilidad
- Comentario 4: Categoría: MIXTO | Tema: usabilidad / interfaz

**Observaciones:**
El método few-shot permitió que el modelo adaptase exactamente el formato clave-valor deseado e identificase correctamente la nueva categoría MIXTO y el Tema.

---

## FASE 3 — Delimitadores y formato de salida

### Prueba 3.1 — Resumen con delimitadores
**Prompt:**
> Resume el texto delimitado por <texto></texto> en 3 viñetas de máximo 20 palabras cada una. Luego escribe una sola oración con la idea principal.
> 
> <texto>
> El diseño de interfaces de usuario (UI) ha evolucionado significativamente con la integración de herramientas basadas en inteligencia artificial. Estas tecnologías permiten automatizar tareas repetitivas de maquetación, generar componentes dinámicos en tiempo real y adaptar la experiencia visual según las preferencias del usuario. Sin embargo, el rol del diseñador sigue siendo fundamental para garantizar la usabilidad, la accesibilidad y la empatía en la interacción. La combinación de IA y criterio humano optimiza los tiempos de desarrollo sin perder la calidad del producto final.
> </texto>

**Resultado:**
* La IA automatiza maquetaciones y adapta componentes dinámicos en tiempo real.
* El diseñador garantiza usabilidad, accesibilidad y empatía en la interacción.
* La colaboración entre IA y humanos reduce tiempos sin comprometer la calidad.

*Idea principal:* La integración de la IA en el diseño UI acelera el desarrollo, manteniendo el criterio humano como factor clave.

### Prueba 3.2 — Extracción de datos estructurados
**Prompt:**
> Del siguiente mensaje extrae: nombre, curso, fecha y motivo.
> Devuelve primero una tabla Markdown y después el mismo contenido en JSON válido.
> Si algún dato no aparece, escribe "no especificado".
> 
> """
> Hola, soy Lucía Ramos del curso de Base de Datos. Quería avisar que el martes 14 no podré asistir al laboratorio porque tengo una cita médica.
> """

**Resultado:**

| Nombre | Curso | Fecha | Motivo |
| :--- | :--- | :--- | :--- |
| Lucía Ramos | Base de Datos | Martes 14 | Cita médica |

```json
{
  "nombre": "Lucía Ramos",
  "curso": "Base de Datos",
  "fecha": "Martes 14",
  "motivo": "Cita médica"
}


## FASE 2 — Zero-shot y few-shot

### Paso 2.1 — Clasificación con zero-shot
**Herramienta:** ChatGPT / Claude / Gemini
**Prompt:**
> Clasifica cada comentario como POSITIVO, NEGATIVO o NEUTRO.
> 1. "La app se cierra cada vez que intento pagar."
> 2. "Llegó el pedido, nada que destacar."
> 3. "Me encantó lo rápido que cargan las pantallas."
> 4. "Está bien, aunque el botón de ayuda es difícil de encontrar."

**Resultado (resumen):**
1. NEGATIVO
2. NEUTRO
3. POSITIVO
4. NEUTRO (o NEGATIVO)

---

### Paso 2.2 — Clasificación con few-shot
**Herramienta:** ChatGPT / Claude / Gemini
**Prompt:**
> Clasifica cada comentario siguiendo el formato de los ejemplos.
> 
> Comentario: "Excelente diseño, todo es muy intuitivo."
> Categoría: POSITIVO | Tema: diseño
> 
> Comentario: "Buen precio, pero la entrega tardó una semana."
> Categoría: MIXTO | Tema: entrega
> 
> Comentario: "La app se cierra cada vez que intento pagar."
> Categoría:
> 
> Comentario: "Está bien, aunque el botón de ayuda es difícil de encontrar."
> Categoría:

**Resultado (resumen):**
- Comentario 3: Categoría: NEGATIVO | Tema: pago / estabilidad
- Comentario 4: Categoría: MIXTO | Tema: usabilidad / ayuda

**Observaciones:**
- **Respeto del formato:** La IA adoptó exactamente la estructura `Categoría | Tema` definida en los ejemplos.
- **Identificación del tema:** Extrajo de forma precisa el tema principal de cada comentario (pago y ayuda/usabilidad).
- **Uso de la categoría MIXTO:** Utilizó correctamente la categoría `MIXTO` para el comentario 4, entendiendo la lógica gracias a los ejemplos provistos.
 

 ## Rúbrica de evaluación

| Criterio | Descripción | Puntaje (1-5) |
| -------- | --------------------------------------------- | :-----------: |
| Relevancia | Responde exactamente lo que se pidió | 5 |
| Precisión | La información es correcta y sin inventos | 5 |
| Formato | Respeta la estructura y extensión solicitadas | 5 |
| Tono | Es adecuado para el público objetivo | 5 |

---

## Iteraciones — Plan de estudio de Python para principiantes

| Versión | Cambio realizado en el prompt | Puntaje total |
| ------- | --------------------------------------------- | :-----------: |
| v1 | Prompt inicial sin estructura | 11/20 |
| v2 | Se agregó rol y contexto | 16/20 |
| v3 | Se definió formato y restricciones | 19/20 |

### Detalle de las iteraciones

* **v1 (Prompt inicial):** *"Hazme un plan para aprender Python."*  
  * **Evaluación:** Respuesta demasiado genérica, sin división de tiempo ni actividades concretas. (11/20)
* **v2 (Con rol y contexto):** *"Actúa como un tutor de programación. Soy un estudiante principiante que tiene 4 semanas para aprender Python desde cero. Crea un plan de estudio."*  
  * **Evaluación:** Mejoró la adaptación al tiempo y nivel, pero el formato en texto plano resultaba denso. (16/20)
* **v3 (Con formato y restricciones):** *"Actúa como tutor de Python. Crea un plan de 4 semanas en una tabla Markdown con las columnas: Semana, Tema clave y Proyecto práctico. Usa un tono motivador y breve."*  
  * **Evaluación:** Respuesta estructurada, fácil de leer y totalmente alineada con la solicitud. (19/20)
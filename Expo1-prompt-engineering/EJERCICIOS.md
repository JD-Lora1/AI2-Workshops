# Laboratorio Práctico: De Prompt Simple a Prompt Avanzado

Este archivo contiene una serie de ejercicios diseñados para demostrar empíricamente la diferencia entre un prompt simple (ingenuo) y un prompt estructurado (avanzado). La meta es que puedas ejecutar ambos, comparar los resultados y validar la teoría aprendida en la guía principal.

---

## Instrucciones

Para cada ejercicio:
1.  **Copia y pega el "Prompt Simple"** en tu LLM de preferencia (ChatGPT, Claude, Gemini, etc.).
2.  **Guarda la respuesta** generada.
3.  **Copia y pega el "Prompt Avanzado"** en el mismo LLM.
4.  **Guarda la respuesta** generada.
5.  **Compara ambas respuestas** usando los "Criterios de Evaluación" sugeridos. Anota tus observaciones.

---

### Ejercicio 1: Generación de una Función de Código

**Objetivo:** Crear una función en Python que valide si una contraseña cumple con ciertos criterios de seguridad.

#### 1.A: Prompt Simple

```
Haz una función en Python para validar una contraseña.
```

### Respuesta de GEMINI 2.5 Flash 
import re

def validar_contrasena(contrasena: str) -> bool:
    """
    Valida una contraseña según criterios de seguridad específicos.

    Args:
        contrasena (str): La contraseña a validar.

    Returns:
        bool: True si la contraseña es válida, False en caso contrario.
    """
    # 1. Longitud mínima de 8 caracteres.
    if len(contrasena) < 8:
        print("La contraseña debe tener al menos 8 caracteres.")
        return False

    # 2. Al menos una letra mayúscula.
    if not re.search(r"[A-Z]", contrasena):
        print("La contraseña debe contener al menos una letra mayúscula.")
        return False

    # 3. Al menos una letra minúscula.
    if not re.search(r"[a-z]", contrasena):
        print("La contraseña debe contener al menos una letra minúscula.")
        return False

    # 4. Al menos un número.
    if not re.search(r"[0-9]", contrasena):
        print("La contraseña debe contener al menos un número.")
        return False

    # 5. Al menos un carácter especial.
    if not re.search(r"[!@#$%^&*()_+={}\[\]|\\:;\"'<,>.?/`~]", contrasena):
        print("La contraseña debe contener al menos un carácter especial.")
        return False

    # Si pasa todas las validaciones, la contraseña es segura.
    print("¡Contraseña válida y segura!")
    return True

# --- Ejemplos de uso ---
print("--- Probando contraseñas ---")
validar_contrasena("Contrasena123!")  # Debería ser válida
print("-" * 25)
validar_contrasena("corta1!")          # Falla por longitud
print("-" * 25)
validar_contrasena("sinMayuscula1!") # Falla por mayúscula
print("-" * 25)
validar_contrasena("SinEspeciales1")  # Falla por carácter especial

#### 1.B: Prompt Avanzado

```
**Rol:** Eres un desarrollador de software senior especializado en ciberseguridad.

**Tarea:** Genera una función en Python llamada `validar_contrasena`.

**Contexto:** La función recibirá una cadena de texto (la contraseña) y debe retornar `True` si cumple con TODAS las siguientes reglas, o `False` si falla al menos una.

**Reglas de Validación (Criterios):**
1.  Debe tener una longitud mínima de 12 caracteres.
2.  Debe contener al menos una letra mayúscula (A-Z).
3.  Debe contener al menos una letra minúscula (a-z).
4.  Debe contener al menos un número (0-9).
5.  Debe contener al menos un carácter especial (ej: @, #, $, %, &, !).

**Formato de Salida:**
-   El bloque de código de la función en Python.
-   Debe incluir docstrings que expliquen qué hace la función, sus parámetros y qué retorna.
-   Añade 3 ejemplos de uso: uno con una contraseña válida y dos con contraseñas inválidas que demuestren diferentes fallos.

**Restricciones:**
-   No uses librerías externas, solo el core de Python.
-   El código debe ser legible y seguir las convenciones de estilo de PEP 8.
```

### Respuesta de GEMINI 2.5 Flash 
import re

def validar_contrasena(contrasena: str) -> bool:
    """
    Valida si una contraseña cumple con un conjunto de reglas de seguridad.

    La contraseña debe cumplir con los siguientes criterios:
    1. Longitud mínima de 12 caracteres.
    2. Contener al menos una letra mayúscula (A-Z).
    3. Contener al menos una letra minúscula (a-z).
    4. Contener al menos un número (0-9).
    5. Contener al menos un carácter especial (p.ej. @, #, $, %, &).

    Args:
        contrasena: La cadena de texto de la contraseña a validar.

    Returns:
        True si la contraseña es válida, False en caso contrario.
    """
    # 1. Verificar la longitud mínima
    if len(contrasena) < 12:
        return False

    # 2. Verificar la presencia de mayúsculas
    if not re.search(r"[A-Z]", contrasena):
        return False

    # 3. Verificar la presencia de minúsculas
    if not re.search(r"[a-z]", contrasena):
        return False

    # 4. Verificar la presencia de números
    if not re.search(r"[0-9]", contrasena):
        return False

    # 5. Verificar la presencia de caracteres especiales
    if not re.search(r"[@#$%&!]", contrasena):
        return False

    # Si todas las verificaciones pasan, la contraseña es válida
    return True

### Ejemplo 1: Contraseña válida
### Cumple con todas las reglas: longitud >= 12, mayúscula, minúscula, número, especial.
contrasena_valida = "C0ntr@s3ñ@S3gur4!"
print(f"'{contrasena_valida}' es válida: {validar_contrasena(contrasena_valida)}")

### Ejemplo 2 y 3 ...

## Salida esperada
'C0ntr@s3ñ@S3gur4!' es válida: True
'Corta!12' es válida: False
'contrasenasegura123' es válida: False


#### 1.C: Evaluación Comparativa

-   **Completitud:** ¿La función del prompt simple incluyó todas las reglas?
-   **Claridad:** ¿El código está bien documentado? ¿Es fácil de entender?
-   **Utilidad:** ¿El prompt avanzado proporcionó ejemplos de uso que facilitan la prueba y la integración?
-   **Robustez:** ¿La función maneja casos borde que el prompt simple podría haber ignorado?

---

# 🔎 Comparación General entre Código 1 y Código 2

---

## **1. Completitud**
- **Código 1**  
  - Incluye todas las reglas clásicas: longitud (≥8), mayúscula, minúscula, número y carácter especial.  
  - Lista amplia de caracteres especiales (`[!@#$%^&*()_+={}\[\]|\\:;\"'<,>.?/`~]`).  
  - Da mensajes de error específicos cuando falla una regla.  

- **Código 2**  
  - Reglas similares, pero más estrictas (longitud ≥12).  
  - Lista limitada de caracteres especiales (`[@#$%&!]`).  
  - No informa al usuario por qué falló la contraseña, solo devuelve `False`.  

✅ **Conclusión**: Código 1 es más completo en retroalimentación y variedad de caracteres; Código 2 es más estricto pero menos flexible.  

---

## **2. Claridad**
- **Código 1**  
  - Documentación clara y explicativa.  
  - Comentarios paso a paso.  
  - Mensajes impresos ayudan a entender rápidamente los fallos.  

- **Código 2**  
  - Docstring muy bien estructurado con reglas enumeradas.  
  - Comentarios internos breves y concisos.  
  - Sin mensajes intermedios → más limpio pero menos informativo.  

✅ **Conclusión**: Código 2 es más conciso y estructurado, mientras que Código 1 es más amigable y pedagógico.  

---

## **3. Utilidad**
- **Código 1**  
  - Ejemplos básicos de uso mostrando qué falla.  
  - Útil para demostraciones rápidas.  

- **Código 2**  
  - Incluye ejemplos **con salidas esperadas (`True/False`)**.  
  - Facilita pruebas automáticas e integración en proyectos.  

✅ **Conclusión**: Código 2 es más útil para pruebas formales y automatizadas; Código 1 es mejor para retroalimentación en tiempo real.  

---

## **4. Robustez**
- **Código 1**  
  - Cobertura amplia de caracteres especiales.  
  - Mensajes detallados para cada fallo.  
  - No maneja contraseñas vacías o `None`.  

- **Código 2**  
  - Más estricto en seguridad (longitud ≥12).  
  - No explica la causa de fallo → menos claro para el usuario.  
  - Lista reducida de caracteres especiales limita flexibilidad.  

✅ **Conclusión**:  
- **Código 1** es más robusto en cobertura de caracteres.  
- **Código 2** es más robusto en seguridad mínima.  


### Ejercicio 2: Extracción de Información a Formato JSON

**Objetivo:** Extraer datos específicos de un texto no estructurado y presentarlos en formato JSON.

#### 2.A: Prompt Simple

```
Saca los datos importantes de este texto en JSON:

"La reunión de lanzamiento del Proyecto Fénix será el 15 de octubre de 2024 a las 10:30 AM en la Sala Júpiter. Los asistentes confirmados son Ana García (Líder de Proyecto), Carlos Rodríguez (Desarrollador Principal) y Elena Fernández (Diseñadora UX). El presupuesto asignado es de $25,000 USD."
```

## Respuesta de Chat gpt
{
  "proyecto": "Fénix",
  "evento": "Reunión de lanzamiento",
  "fecha": "2024-10-15",
  "hora": "10:30 AM",
  "lugar": "Sala Júpiter",
  "asistentes": [
    { "nombre": "Ana García", "rol": "Líder de Proyecto" },
    { "nombre": "Carlos Rodríguez", "rol": "Desarrollador Principal" },
    { "nombre": "Elena Fernández", "rol": "Diseñadora UX" }
  ],
  "presupuesto": 25000,
  "moneda": "USD"
}


#### 2.B: Prompt Avanzado

```
**Rol:** Eres un asistente de procesamiento de datos altamente preciso.

**Tarea:** Extrae la información clave del siguiente texto y formatéala estrictamente como un objeto JSON.

**Texto de Entrada:**
```
La reunión de lanzamiento del Proyecto Fénix será el 15 de octubre de 2024 a las 10:30 AM en la Sala Júpiter. Los asistentes confirmados son Ana García (Líder de Proyecto), Carlos Rodríguez (Desarrollador Principal) y Elena Fernández (Diseñadora UX). El presupuesto asignado es de $25,000 USD.
```

**Esquema JSON de Salida (Schema):**
Debes seguir esta estructura exacta. Si un campo no se encuentra en el texto, déjalo como `null`.

```json
{
  "proyecto": {
    "nombre": "string",
    "presupuesto": {
      "monto": "number",
      "moneda": "string"
    }
  },
  "reunion": {
    "fecha": "string (formato YYYY-MM-DD)",
    "hora": "string (formato HH:MM)",
    "ubicacion": "string"
  },
  "asistentes": [
    {
      "nombre": "string",
      "rol": "string"
    }
  ]
}
```

**Restricciones:**
-   El `monto` del presupuesto debe ser un número, no un string.
-   La `fecha` y `hora` deben ser normalizadas a los formatos especificados.
-   No incluyas campos que no estén en el esquema.
```

### REspuesta de Chat GPT

```json
{
  "proyecto": {
    "nombre": "Proyecto Fénix",
    "presupuesto": {
      "monto": 25000,
      "moneda": "USD"
    }
  },
  "reunion": {
    "fecha": "2024-10-15",
    "hora": "10:30",
    "ubicacion": "Sala Júpiter"
  },
  "asistentes": [
    {
      "nombre": "Ana García",
      "rol": "Líder de Proyecto"
    },
    {
      "nombre": "Carlos Rodríguez",
      "rol": "Desarrollador Principal"
    },
    {
      "nombre": "Elena Fernández",
      "rol": "Diseñadora UX"
    }
  ]
}
```


#### 2.C: Evaluación Comparativa

-   **Estructura:** ¿El JSON del prompt simple tiene una estructura lógica y predecible?
-   **Precisión:** ¿Los tipos de datos son correctos (números vs. strings)?
-   **Parseabilidad:** ¿El JSON generado por el prompt avanzado es directamente utilizable por una aplicación sin necesidad de limpieza o conversión?
-   **Manejo de Nulos:** ¿Cómo manejaría cada uno un texto donde, por ejemplo, el presupuesto no se menciona?

* **Estructura:**

  * Prompt simple: Menos estructurado, mezcla campos al mismo nivel.
  * Prompt avanzado: Jerárquico y alineado con el esquema, más predecible.

* **Precisión:**

  * Prompt simple: Mezcla strings y números (ej. `"hora": "10:30 AM"`).
  * Prompt avanzado: Normaliza formatos y usa número para presupuesto.

* **Parseabilidad:**

  * Prompt simple: Puede requerir limpieza (ej. quitar `"AM"`).
  * Prompt avanzado: Directamente utilizable en aplicaciones.

* **Manejo de Nulos:**

  * Prompt simple: No contempla nulos explícitos.
  * Prompt avanzado: Sí lo prevé en el esquema (`null` si falta un dato).


---

### Ejercicio 3: Escritura Creativa con Tono y Estilo

**Objetivo:** Escribir un párrafo corto sobre un tema complejo, adaptado a una audiencia específica.

#### 3.A: Prompt Simple

```
Escribe sobre los agujeros negros.
```
### Salida de Google AI Studio (Nano Banana)

Los agujeros negros son regiones del espacio-tiempo donde la gravedad es tan intensa que nada, ni siquiera la luz, puede escapar. Se forman a partir de los restos de estrellas masivas que colapsan al final de su vida.

Existen diferentes tipos de agujeros negros:

    Agujeros negros estelares: Con masas de hasta 20 veces la del Sol.

    Agujeros negros supermasivos: Con masas de millones o miles de millones de veces la del Sol, se encuentran en el centro de las galaxias.

Aquí tienes una imagen de cómo se representaría un agujero negro:
![alt text](image.png)

#### 3.B: Prompt Avanzado

```
**Rol:** Eres un divulgador científico como Carl Sagan, capaz de explicar conceptos complejos con asombro y claridad.

**Tarea:** Escribe un párrafo corto (aproximadamente 100 palabras) sobre los agujeros negros.

**Audiencia:** Niños de 10 a 12 años.

**Tono y Estilo:**
-   Usa un lenguaje sencillo y evocador.
-   Evita la jerga técnica y las fórmulas matemáticas.
-   Utiliza analogías o metáforas fáciles de entender (ej: "un aspirador cósmico del que ni la luz puede escapar").
-   El tono debe ser de misterio y fascinación, no de miedo.

**Formato de Salida:**
-   Un único párrafo de texto.

**Restricción:**
-   No menciones la "singularidad" o la "relatividad general" directamente. Enfócate en el fenómeno observable.
```

### Salida de Google AI Studio (Nano Banana)

Imagina el espacio como una inmensa tela cósmica, estirada y lisa. Ahora, piensa en algo tan increíblemente pesado que, al ponerlo sobre esa tela, ¡la estira y hunde tanto que se forma un agujero profundo! Eso es, más o menos, un agujero negro. Son como aspiradoras gigantes en el universo, tan poderosas que todo lo que se acerca demasiado –estrellas, planetas, ¡incluso la luz!– es engullido para siempre. Es un lugar de no retorno, un misterio cósmico donde las leyes que conocemos se estiran hasta el límite. Pero no te preocupes, están muy, muy lejos, y son una de las maravillas más asombrosas del universo, ¡esperando que las exploremos con nuestra imaginación!

#### 3.C: Evaluación Comparativa

-   **Adecuación a la Audiencia:** ¿Qué respuesta es más apropiada y comprensible para un niño?
-   **Tono:** ¿Logró el prompt simple capturar el tono de asombro solicitado?
-   **Creatividad:** ¿Qué respuesta es más original y memorable?
-   **Cumplimiento de Restricciones:** ¿El prompt avanzado logró evitar la jerga técnica como se le pidió?


```
### Adecuación a la Audiencia (Niños de 10-12 años)

- **Prompt Avanzado:**  
  Es mucho más apropiada y comprensible. La analogía de la "tela cósmica" y la "aspiradora gigante" son muy visuales y fáciles de entender para un niño. El lenguaje es sencillo y las ideas se presentan de forma gradual y amigable, creando una conexión directa con la imaginación infantil.  

- **Prompt Simple:**  
  Es más directa y enciclopédica. Conceptos como "regiones del espacio-tiempo" o "gravedad intensa" son abstractos para un niño de esa edad. La mención de "tipos de agujeros negros" y "masas de millones o miles de millones de veces la del Sol" introduce números grandes que pueden ser difíciles de contextualizar, haciendo la información menos accesible.  

---

### Tono (Asombro)

- **Prompt Avanzado:**  
  Captura muy bien el tono de asombro y misterio. Frases como "increíblemente pesado", "aspiradoras gigantes", "engullido para siempre" y "misterio cósmico" evocan fascinación sin ser aterradoras. El cierre con "maravillas más asombrosas del universo" refuerza este tono, alineándose perfectamente con el rol de un divulgador como Carl Sagan.  

- **Prompt Simple:**  
  Es informativa y objetiva. Presenta hechos, pero carece del tono evocador de asombro y maravilla. Su enfoque es más expositivo que inspirador.  

---

### Creatividad (Original y Memorable)

- **Prompt Avanzado:**  
  Es significativamente más creativa. La analogía de la "tela cósmica" para explicar la curvatura del espacio-tiempo es una metáfora poderosa y bien ejecutada aquí. La "aspiradora gigante" es una imagen vívida y fácil de recordar. Esto la hace muy original y memorable para la audiencia.  

- **Prompt Simple:**  
  Es estándar y directa. No utiliza analogías creativas ni metáforas que la hagan destacar o ser especialmente memorable para un niño. Es un resumen factual más que una descripción imaginativa.  

---

### Cumplimiento de Restricciones (Evitar jerga técnica)

- **Prompt Avanzado:**  
  Cumple excelentemente. Evita completamente la jerga técnica, utilizando analogías en su lugar para explicar los conceptos complejos. No menciona "singularidad" ni "relatividad general".  

- **Prompt Simple:**  
  Aunque no menciona "singularidad" o "relatividad general", sí utiliza "espacio-tiempo", "gravedad intensa" y "colapsan al final de su vida", que pueden ser consideradas jerga o conceptos avanzados para la audiencia solicitada.  
```

---

### Conclusión de los Ejercicios

Al realizar estos laboratorios, deberías notar que los prompts avanzados no solo dan respuestas "mejores", sino que producen resultados:
-   **Más predecibles y consistentes.**
-   **Más fáciles de integrar en flujos de trabajo automatizados.**
-   **Alineados con objetivos de negocio o de producto muy específicos.**
-   **Que requieren menos post-procesamiento manual.**

¡La ingeniería de prompts es el arte de la especificación precisa para obtener resultados de alta calidad!

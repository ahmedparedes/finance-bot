## **Documento de Requisitos del Producto (PRD) para Chatbot de Finanzas**

### **1. Introducción**

#### **1.1 Propósito**
El objetivo de este documento es definir los requisitos para crear un chatbot de finanzas que ayude a los usuarios a resolver dudas financieras. Este chatbot usará **FastAPI** como backend y la **API de OpenAI** para generar respuestas inteligentes y útiles basadas en preguntas de los usuarios.

#### **1.2 Alcance**
El chatbot será una aplicación web simple que permitirá a los usuarios escribir preguntas sobre temas financieros (por ejemplo, inversiones, ahorros o conceptos básicos) y recibir respuestas generadas por inteligencia artificial. En esta primera versión, el chatbot no guardará el historial de las conversaciones, es decir, cada pregunta será independiente. Más adelante, podrías añadirle más funciones según vayas aprendiendo.

---

### **2. Descripción General**

#### **2.1 Perspectiva del Producto**
El chatbot será accesible desde un navegador web. Los usuarios podrán escribir sus preguntas en un cuadro de texto y ver las respuestas en tiempo real. Este proyecto combina tu conocimiento en finanzas con tecnologías modernas como FastAPI (un framework para crear APIs) y la API de OpenAI (que genera respuestas basadas en IA).

#### **2.2 Funciones del Producto**
- Recibir preguntas de los usuarios a través de una página web.
- Enviar esas preguntas a la API de OpenAI para obtener respuestas inteligentes.
- Mostrar las respuestas en la misma página web de forma clara.

#### **2.3 Usuarios Objetivo**
- Personas interesadas en aprender sobre finanzas (principiantes o intermedios).
- Estudiantes o profesionales que buscan respuestas rápidas sobre temas financieros.

---

### **3. Requerimientos Funcionales**
Estos son los "qué" del sistema, es decir, lo que debe hacer.

#### **3.1 Interfaz de Usuario**
- **Cuadro de texto:** 
  - Un campo de entrada donde el usuario escribe su pregunta financiera.
  - Debe tener un placeholder informativo como "Escribe tu pregunta sobre finanzas aquí...".
  - Debe permitir preguntas de al menos 500 caracteres para consultas complejas.
  - Debe tener validación para evitar envíos vacíos.

- **Botón de envío:** 
  - Un botón claramente visible para enviar la pregunta.
  - Debe mostrar un estado de "cargando" mientras se procesa la respuesta.
  - Debe deshabilitarse durante el procesamiento para evitar múltiples envíos.

- **Área de respuesta:** 
  - Un espacio donde se muestra la respuesta generada por el chatbot.
  - Debe formatear correctamente párrafos, listas y otros elementos de texto.
  - Debe incluir un indicador visual cuando se está generando la respuesta.
  - Debe permitir copiar el texto de la respuesta fácilmente.

- **Elementos adicionales:**
  - Un encabezado que identifique claramente el propósito del chatbot.
  - Un pie de página con información sobre el uso de IA para generar respuestas.
  - Un botón para limpiar la conversación actual.

#### **3.2 Comunicación con el Backend**
- **Envío de preguntas:**
  - La interfaz debe recopilar la pregunta del usuario y enviarla al backend mediante una solicitud HTTP POST.
  - La solicitud debe incluir la pregunta como parámetro principal.
  - Se debe implementar un mecanismo de timeout para manejar respuestas lentas (máximo 30 segundos).
  - La comunicación debe ser asíncrona para no bloquear la interfaz de usuario.

- **Recepción de respuestas:**
  - El frontend debe recibir la respuesta del backend y mostrarla en el área designada.
  - Debe manejar correctamente los errores de comunicación y mostrar mensajes apropiados al usuario.
  - Debe procesar y formatear la respuesta para mejorar la legibilidad.

#### **3.3 Procesamiento de Preguntas**
- **Validación de entrada:**
  - El backend debe validar que la pregunta no esté vacía.
  - Debe detectar y rechazar contenido inapropiado o no relacionado con finanzas.
  - Debe limitar la longitud máxima de las preguntas (por ejemplo, 1000 caracteres).

- **Preparación para la API de OpenAI:**
  - El backend debe formatear la pregunta para enviarla a la API de OpenAI.
  - Debe incluir un contexto o prompt inicial que oriente las respuestas hacia temas financieros.
  - Debe configurar parámetros como temperatura y max_tokens para obtener respuestas adecuadas.

#### **3.4 Generación de Respuestas**
- **Integración con OpenAI:**
  - El sistema debe conectarse a la API de OpenAI utilizando una clave de API válida.
  - Debe configurar el modelo (por ejemplo, GPT-3.5-turbo o GPT-4) según las necesidades de calidad y costo.
  - Debe enviar la pregunta con un contexto que indique que las respuestas deben ser sobre finanzas.

- **Procesamiento de respuestas:**
  - El sistema debe recibir la respuesta de la API de OpenAI y procesarla.
  - Debe verificar que la respuesta sea coherente y relevante para la pregunta.
  - Debe formatear la respuesta para mejorar su presentación en el frontend.

- **Manejo de errores:**
  - El sistema debe manejar errores de la API (como límites de tasa, problemas de conexión, etc.).
  - Debe proporcionar mensajes de error amigables al usuario cuando sea necesario.
  - Debe implementar reintentos automáticos en caso de fallos temporales.

#### **3.5 Especialización en Finanzas**
- **Enfoque temático:**
  - El chatbot debe estar especializado en responder preguntas sobre finanzas personales, inversiones, ahorro, presupuestos, etc.
  - Debe proporcionar información educativa y general, no consejos financieros personalizados.
  - Debe aclarar cuando una pregunta requeriría la consulta con un profesional financiero.

- **Calidad de respuestas:**
  - Las respuestas deben ser informativas, precisas y fáciles de entender.
  - Deben incluir explicaciones de términos financieros cuando sea apropiado.
  - Deben ser objetivas y basadas en principios financieros generalmente aceptados.

#### **3.6 Limitaciones Explícitas**
- El chatbot **no** debe:
  - Proporcionar consejos de inversión específicos.
  - Hacer predicciones sobre mercados o instrumentos financieros específicos.
  - Solicitar o almacenar información financiera personal del usuario.
  - Presentarse como un asesor financiero certificado.

#### **3.7 Rendimiento y Escalabilidad**
- **Tiempos de respuesta:**
  - El sistema debe procesar y devolver respuestas en menos de 5 segundos en condiciones normales.
  - Debe manejar múltiples solicitudes simultáneas sin degradación significativa del rendimiento.

- **Disponibilidad:**
  - El sistema debe estar disponible al menos el 99% del tiempo.
  - Debe implementar mecanismos para manejar picos de tráfico.

---

### **4. Requerimientos No Funcionales**
Estos son los "cómo" del sistema, es decir, cómo debe comportarse.

#### **4.1 Rendimiento**
- El chatbot debe responder en menos de **5 segundos** para la mayoría de las preguntas (esto depende de la velocidad de la API de OpenAI y tu conexión).

#### **4.2 Seguridad**
- La clave de la API de OpenAI debe mantenerse secreta y no exponerse en el código público.
- La comunicación entre la página web y el backend debe ser segura (usando HTTPS cuando lo despliegues).

#### **4.3 Usabilidad**
- La interfaz debe ser simple e intuitiva, pensada para personas sin experiencia técnica.

#### **4.4 Mantenibilidad**
- El código debe ser claro y fácil de actualizar en el futuro (por ejemplo, para añadir nuevas funciones).

---

### **5. Diseño y Arquitectura**

#### **5.1 Frontend (Parte Visual)**
- **Tecnologías:** 
  - **HTML** para la estructura básica de la página.
  - **CSS** para los estilos (se puede usar un framework como Bootstrap para simplificar).
  - **HTMX** para manejar las interacciones con el backend sin necesidad de escribir JavaScript complejo.
  - **Alpine.js** para gestionar estados y comportamientos simples en el frontend.

- **Ventajas de usar HTMX y Alpine.js para principiantes:**
  - **HTMX** permite hacer solicitudes AJAX, actualizaciones parciales y más, directamente desde atributos HTML.
  - **Alpine.js** ofrece reactividad y comportamientos dinámicos con una sintaxis sencilla y declarativa.
  - Ambas herramientas son ligeras y no requieren configuración compleja ni bundlers.
  - Reducen drásticamente la cantidad de JavaScript que necesitas escribir.

- **Componentes principales:**
  - **Página principal:** Interfaz simple con un encabezado descriptivo, área de entrada de preguntas y área de respuestas.
  - **Formulario de entrada:** Campo de texto y botón de envío con estados visuales gestionados por Alpine.js.
  - **Área de respuesta:** Contenedor que se actualizará con HTMX al recibir la respuesta del servidor.
  - **Indicadores de estado:** Elementos visuales que muestran cuando se está procesando una pregunta, controlados por Alpine.js.

- **Diseño responsivo:**
  - La interfaz debe adaptarse a diferentes tamaños de pantalla (móvil, tablet, escritorio).
  - Se recomienda usar CSS Grid o Flexbox para layouts simples y responsivos.
  - El texto debe ser legible en todos los dispositivos sin necesidad de zoom.

- **Experiencia de usuario:**
  - Feedback inmediato al enviar una pregunta (indicador de carga gestionado por Alpine.js).
  - Actualizaciones parciales de la página con HTMX sin recargar toda la interfaz.
  - Mensajes claros en caso de error o tiempo de espera excedido.

#### **5.2 Backend (Parte Lógica)**
- **Tecnologías:** FastAPI para crear una API RESTful.
- **Componentes principales:**
  - **Servidor API:** Aplicación FastAPI que expone endpoints para recibir preguntas y devolver respuestas.
  - **Middleware de validación:** Componente que verifica y sanitiza las entradas del usuario.
  - **Servicio de integración con OpenAI:** Módulo que gestiona la comunicación con la API de OpenAI.
  - **Manejador de errores:** Sistema para capturar y procesar errores de forma elegante.
  - **Sistema de logging:** Componente para registrar actividad y errores para diagnóstico.

- **Arquitectura de endpoints:**
  - **/preguntar:** Endpoint principal que recibe preguntas y devuelve respuestas.
  - **/estado:** Endpoint opcional para verificar el estado del servicio.
  - **/info:** Endpoint opcional que proporciona información sobre el chatbot.

- **Flujo de procesamiento:**
  1. Recepción de la pregunta a través del endpoint.
  2. Validación y sanitización de la entrada.
  3. Preparación del contexto para la API de OpenAI.
  4. Envío de la solicitud a OpenAI.
  5. Recepción y procesamiento de la respuesta.
  6. Devolución de la respuesta formateada al cliente.

#### **5.3 Integración con OpenAI**
- **Configuración del modelo:**
  - Selección del modelo adecuado (GPT-3.5-turbo o GPT-4) según requisitos de calidad y presupuesto.
  - Configuración de parámetros como temperatura (0.7 recomendado para balance entre creatividad y precisión).
  - Establecimiento de límites de tokens para controlar la longitud de las respuestas.

- **Diseño del prompt:**
  - Creación de un prompt inicial que establezca el contexto financiero.
  - Inclusión de instrucciones para que el modelo responda como un experto en finanzas.
  - Definición de limitaciones explícitas (no dar consejos de inversión específicos, etc.).

- **Ejemplo de estructura de prompt:**
  - Instrucción de rol: "Eres un asistente especializado en finanzas personales y educación financiera."
  - Contexto: "Proporciona información educativa sobre conceptos financieros, pero no des consejos específicos de inversión."
  - Limitaciones: "Si te preguntan sobre predicciones específicas de mercado o recomendaciones personalizadas, aclara que eso requeriría consultar a un asesor financiero certificado."
  - Pregunta del usuario: [Aquí se inserta la pregunta recibida]

- **Gestión de la API:**
  - Almacenamiento seguro de la clave de API (variables de entorno, no en código).
  - Implementación de mecanismos de retry en caso de errores temporales.
  - Monitoreo de uso para controlar costos y límites de la API.

#### **5.4 Almacenamiento**
- En esta versión inicial, no se implementará almacenamiento persistente de conversaciones.
- **Consideraciones para futuras versiones:**
  - Base de datos para almacenar historial de preguntas y respuestas.
  - Sistema de autenticación para identificar usuarios y mantener sus conversaciones.
  - Análisis de preguntas frecuentes para mejorar el servicio.

---

### **6. Plan de Trabajo**
Aquí te detallo cómo construir el chatbot paso a paso. Como principiante, lo haremos manejable y progresivo.

#### **6.1 Fase 1: Configuración y Aprendizaje Inicial**
- **Tareas:**
  1. Instala **Python** en tu computadora (versión 3.8 o superior).
  2. Instala **uv** siguiendo las instrucciones oficiales:
     - **Para Mac**: 
       ```bash
       curl -LsSf https://astral.sh/uv/install.sh | sh
       ```
     - También puedes usar Homebrew:
       ```bash
       brew install astral-sh/uv/uv
       ```
  3. Inicializa un nuevo proyecto con `uv init --app` para crear la estructura básica del proyecto con `pyproject.toml`.
  4. Añade las dependencias necesarias con `uv add fastapi uvicorn`.
  5. Sincroniza las dependencias con `uv sync` para crear el archivo `uv.lock` y el entorno virtual.
  6. Crea una API simple con FastAPI que devuelva un mensaje como "¡Hola, soy tu chatbot de finanzas!".
  7. Obtén una **clave de API de OpenAI** registrándote en su sitio web.
- **Duración estimada:** 1-2 días.
- **Recursos:** Documentación oficial de FastAPI y uv (https://docs.astral.sh/uv/).

#### **6.2 Fase 2: Integración con la API de OpenAI**
- **Tareas:**
  1. Añade la librería de OpenAI a tu proyecto con `uv add openai`.
  2. Actualiza el archivo `pyproject.toml` si necesitas versiones específicas de las dependencias.
  3. Sincroniza nuevamente con `uv sync` para actualizar el entorno virtual.
  4. Aprende a hacer una llamada simple a la API de OpenAI desde Python (puedes probarlo con un script básico).
  5. Modifica tu API de FastAPI para que reciba una pregunta (por ejemplo, mediante un endpoint `/preguntar`), la envíe a OpenAI y devuelva la respuesta.
- **Duración estimada:** 2-3 días.
- **Ejemplo de código básico:**
  ```python
  from fastapi import FastAPI
  from openai import OpenAI

  app = FastAPI()
  client = OpenAI(api_key="tu-clave-de-api")

  @app.post("/preguntar")
  async def preguntar(pregunta: str):
      response = client.chat.completions.create(
          model="gpt-3.5-turbo",
          messages=[{"role": "user", "content": pregunta}]
      )
      return {"respuesta": response.choices[0].message.content}
  ```

#### **6.3 Fase 3: Desarrollo del Frontend con HTMX y Alpine.js**
- **Tareas:**
  1. Crea un archivo HTML básico para tu aplicación.
  2. Incluye HTMX y Alpine.js desde CDN para simplificar:
     ```html
     <script src="https://unpkg.com/htmx.org@1.9.10"></script>
     <script src="https://unpkg.com/alpinejs@3.13.3/dist/cdn.min.js" defer></script>
     ```
  3. Diseña el formulario utilizando HTMX para manejar la comunicación con el backend:
     ```html
     <!-- Ejemplo conceptual, no código final -->
     <form hx-post="/preguntar" hx-target="#respuesta" hx-indicator="#cargando">
       <input type="text" name="pregunta" placeholder="Escribe tu pregunta sobre finanzas aquí...">
       <button type="submit">Enviar</button>
       <div id="cargando" class="htmx-indicator">Procesando pregunta...</div>
     </form>
     <div id="respuesta"></div>
     ```
  4. Usa Alpine.js para manejar estados simples y comportamientos de la interfaz:
     ```html
     <!-- Ejemplo conceptual, no código final -->
     <div x-data="{ mostrarAyuda: false }">
       <button @click="mostrarAyuda = !mostrarAyuda">Ayuda</button>
       <div x-show="mostrarAyuda">
         Escribe cualquier pregunta sobre finanzas y nuestro chatbot te responderá.
       </div>
     </div>
     ```
  5. Configura el backend para devolver HTML parcial que HTMX pueda insertar directamente en la página.
  6. Para ejecutar la aplicación, usa `uv run uvicorn main:app --reload` que automáticamente utilizará el entorno virtual creado.

- **Duración estimada:** 2-3 días.
- **Recursos adicionales:**
  - Documentación oficial de HTMX: https://htmx.org/docs/
  - Documentación oficial de Alpine.js: https://alpinejs.dev/start-here
  - Tutoriales para principiantes sobre HTMX y FastAPI

#### **6.4 Fase 4: Mejoras y Pruebas**
- **Tareas:**
  1. Añade estilos con CSS para que la página se vea más atractiva.
  2. Prueba el chatbot con preguntas como "¿Cómo ahorrar dinero?" o "¿Qué es una acción?".
  3. Corrige errores (por ejemplo, si la API falla o el frontend no muestra la respuesta).
- **Duración estimada:** 2 días.

#### **6.5 Fase 5: Despliegue**
- **Tareas:**
  1. Prepara tu proyecto para el despliegue asegurándote de que el archivo `pyproject.toml` y `uv.lock` estén correctamente configurados.
  2. Sube tu backend a un servidor gratuito como **Heroku**, **Vercel** o **Render**.
  3. Configura el servidor para que utilice uv para instalar las dependencias con `uv sync`.
  4. Ajusta el frontend para que se conecte a la URL pública de tu API.
  5. Haz que la página web sea accesible para otros (puedes subirla a GitHub Pages o un hosting similar).
- **Duración estimada:** 2-3 días.
- **Recursos:** Tutoriales de despliegue de FastAPI en YouTube o blogs.

---

### **7. Consideraciones Adicionales**
- **Estructura del proyecto:** Tu proyecto debería tener una estructura similar a esta:
  ```
  finance-bot/
  ├── .venv/                  # Entorno virtual (creado automáticamente por uv)
  ├── .python-version         # Versión de Python para el proyecto
  ├── pyproject.toml          # Configuración del proyecto y dependencias
  ├── uv.lock                 # Archivo de bloqueo de dependencias
  ├── app/                    # Código de la aplicación
  │   ├── main.py             # Punto de entrada de FastAPI
  │   ├── static/             # Archivos estáticos (CSS, JS)
  │   │   ├── css/            # Estilos CSS
  │   │   └── js/             # Scripts JS adicionales (si son necesarios)
  │   └── templates/          # Plantillas HTML
  │       ├── index.html      # Página principal con HTMX y Alpine.js
  │       └── partials/       # Fragmentos HTML para actualizaciones parciales con HTMX
  └── README.md               # Documentación del proyecto
  ```

- **Ventajas de HTMX y Alpine.js para principiantes:**
  - **Curva de aprendizaje suave:** Ambas herramientas son fáciles de aprender y usar.
  - **Menos código:** Reducen drásticamente la cantidad de JavaScript que necesitas escribir.
  - **Enfoque en HTML:** HTMX te permite centrarte en HTML, que suele ser más familiar para principiantes.
  - **Sin build steps:** No necesitas configurar bundlers o transpiladores complejos.
  - **Desarrollo rápido:** Permiten crear interfaces interactivas con muy poco código.

- **Configuración en Mac:**
  - En macOS, asegúrate de que uv esté en tu PATH después de la instalación.
  - Si usas zsh (shell predeterminado en Mac moderno), puedes añadir a tu `~/.zshrc`:
    ```bash
    export PATH="$HOME/.cargo/bin:$PATH"
    ```
  - Después de modificar el archivo, ejecuta `source ~/.zshrc` para aplicar los cambios.

- **Futuras mejoras:** Una vez que domines esta versión básica, podrías:
  - Guardar las conversaciones en una base de datos para mantener el contexto.
  - Añadir datos financieros en tiempo real (por ejemplo, usando APIs como Yahoo Finance).
  - Personalizar respuestas según la situación del usuario (ingresos, gastos, etc.).
- **Consejo:** Avanza poco a poco y no te preocupes si algo no sale perfecto al inicio. ¡Es parte del aprendizaje!

---

## **Recomendaciones Finales**
Este PRD te da una base sólida para empezar. Te sugiero:
1. Revisar este documento y ajustar lo que necesites según tus prioridades.
2. Buscar tutoriales básicos de FastAPI, OpenAI y uv (gestor de paquetes) para complementar los pasos.
3. Probar cada fase antes de pasar a la siguiente para no sentirte abrumado.
4. Familiarizarte con el formato `pyproject.toml` y cómo uv gestiona las dependencias.

Si tienes dudas sobre algún paso, como configurar el proyecto con uv, usar la API de OpenAI o crear el frontend, ¡pregúntame! Estoy aquí para ayudarte. ¡Mucho éxito con tu chatbot de finanzas!
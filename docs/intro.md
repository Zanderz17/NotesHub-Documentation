---
sidebar_position: 1
---

# Notas Generales sobre NotesHub

NotesHub, es un bot de Telegram impulsado por GPT-3.5-turbo de OpenAI, diseñado para brindar resúmenes inteligentes de archivos PDF. La funcionalidad principal de NotesHub se centra en simplificar el proceso de obtención de resúmenes de documentos PDF de manera interactiva y eficiente.

## Configuración del Entorno

Antes de ejecutar el script, asegúrate de tener configurado correctamente el entorno. Sigue estos pasos:

1. **Instalación de Dependencias:**

   - Instala las dependencias necesarias ejecutando el siguiente comando:
     ```bash
     pip install -r requirements.txt
     ```

2. **Configuración de Variables de Entorno:**

   - Asegúrate de configurar las variables de entorno necesarias en un archivo `.env`. Consulta el archivo de ejemplo `.env.example` para obtener más información.

3. **Activación del Entorno Virtual:**

   - Activa el entorno virtual con el siguiente comando:
     ```bash
     source myenv/bin/activate
     ```

4. **Iniciar el Bot:**
   - Ejecuta el script principal para iniciar el bot de Telegram:
     ```bash
     python main.py
     ```

## Guía de Uso

1. Inicio de Interacción: Utiliza el comando /start para iniciar la interacción con el bot.
2. Procesamiento de PDF: Sube un documento PDF para recibir un resumen y participar en conversaciones con el bot.
3. Cambiar Modo de Interacción: Emplea el comando /change_mode para alternar entre diferentes modos de interacción.
4. Estimación de Costos: Visualiza la estimación de costos para resumir un documento mediante el comando /calc_summary_cost.
5. Consulta de Límite de Resúmenes: Utiliza /view_summary_limit para conocer el límite de resúmenes disponibles.

## Solución de Problemas Comunes

### El Bot no Responde Después de /start

Si el bot no responde después de enviar el comando `/start`, verifica lo siguiente:

1. **Variables de Entorno:**

   - Asegúrate de haber configurado correctamente las variables de entorno, incluido el token de Telegram.

2. **Logs del Bot:**

   - Revisa los registros del bot para obtener información sobre posibles errores. Puedes encontrar registros en el archivo de registro del bot.

3. **Conexión a Internet:**
   - Confirma que el servidor del bot tiene una conexión a Internet estable y puede acceder a los servicios de OpenAI y Telegram.

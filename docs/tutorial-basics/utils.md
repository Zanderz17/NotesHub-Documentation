---
sidebar_position: 3
---

# Utils.py

## send_to_gpt(chunks)

1. La función toma una lista de fragmentos de texto como entrada.
2. Para cada fragmento, se construye un prompt específico.
3. Utiliza el Chat API de OpenAI para obtener la respuesta del modelo GPT-3.5-turbo.
4. Maneja posibles errores y realiza reintentos en caso de falla en la conexión.
5. Devuelve una lista de respuestas del modelo correspondientes a cada fragmento.

```py
chunks = [...]  # Lista de fragmentos de texto
responses = send_to_gpt(chunks)
```

## dict_to_html_to_pdf(final_chat_response, filename)

1. La función toma un objeto final_chat_response que contiene la estructura del chat, incluyendo título, resumen, sentimiento, etc.
2. Utiliza una plantilla HTML predefinida para renderizar el contenido del chat (archivo template.html)
3. Guarda el HTML renderizado en un archivo temporal.
4. Utiliza WeasyPrint para convertir el HTML en un archivo PDF.
5. Devuelve la ruta del archivo PDF generado.

```py
final_response = {...}  # Objeto final del chat
pdf_path = dict_to_html_to_pdf(final_response, "output")
```

## Notas Adicionales:

Asegúrese de tener instaladas las bibliotecas necesarias (weasyprint, jinja2) para el correcto funcionamiento de esta función.
La plantilla HTML utilizada puede encontrarse en el archivo template.html. Personalícela según sus necesidades.

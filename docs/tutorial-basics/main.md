---
sidebar_position: 1
---

# Main.py

## Configuración e Importación de Bibliotecas

Activación y desactivación del entorno virtual.
Importación de bibliotecas necesarias como nltk, os, openai, etc.
Configuración de token encoding y variables de entorno.

```py
# source myenv/bin/activate
# deactivate
import nltk
nltk.download('punkt')
from dotenv import load_dotenv
import os
import openai
from nltk.tokenize import sent_tokenize
from aiogram.dispatcher.filters import Command, ContentTypeFilter
from aiogram import Bot, Dispatcher, types
from aiogram.types import Message, ContentType
from aiogram.utils import executor
from aiogram.dispatcher import FSMContext
from aiogram.types import InlineKeyboardButton, InlineKeyboardMarkup, InputFile
from utils import *
from utils_db import *
import tempfile
import urllib.request
import ssl
import tiktoken
```

## Configuración del Bot de Telegram

Configuración de variables relacionadas con el modelo GPT-3.5-turbo y el bot de Telegram.
Establecimiento de variables de entorno.

```py
# Token encoding configuration
enc = tiktoken.encoding_for_model("gpt-3.5-turbo")

cost_by_in_token = 0.0000015
cost_by_out_token = 0.000002

# Disable SSL verification
ssl._create_default_https_context = ssl._create_unverified_context

FILE_SIZE_LIMIT = 3 * 1024 * 1024 # 2 MB
gptTurboRate = 0.002
cwd = os.getcwd()

load_dotenv()
openai.api_key = os.getenv("OPENAI_API_KEY")
telegram_username = os.getenv("TELEGRAM_BOT_USERNAME")

bot = Bot(token=os.getenv("TELEGRAM_TOKEN"), parse_mode='HTML')
dp = Dispatcher(bot)
```

## Configuración de Teclados Inline

Definición de botones para teclados inline utilizados en la interacción del usuario en el chat de telegram con el bot

```py
summary_pdf_button = InlineKeyboardButton(text="Subir un PDF", callback_data='summary_pdf')
chatting_button = InlineKeyboardButton(text="Interactuar", callback_data='chatting')
keyboard = InlineKeyboardMarkup(inline_keyboard=[[summary_pdf_button]])
keyboard2 = InlineKeyboardMarkup(inline_keyboard=[[chatting_button]])
```

## Manejo de Callbacks

Manejo de callbacks para cambiar el modo de interacción del usuario.

```py
@dp.callback_query_handler(lambda callback_query: True)
async def button_handler(callback_query: types.CallbackQuery):
    global MODE
    user_id = callback_query.from_user.id
    MODE[user_id] = callback_query.data

    with open('MODE.json', 'w') as file:
        json.dump(MODE, file)

    await bot.answer_callback_query(callback_query.id, text=f"Current mode: {MODE[user_id]}")
```

## Manejo de Comandos

Respuesta al comando /start para iniciar la interacción con el bot.

```py
@dp.message_handler(commands=['start'])
async def cmd_start(msg: types.Message) -> None:
    global MODE
    user_id = msg.from_user.id

    save_user(user_id, msg.from_user.first_name)

    if user_id not in MODE:
        MODE[user_id] = 'chatting'
    if user_id not in USER_STATES:
        USER_STATES[user_id] = 0

    reply_text = f"¡Hola, {msg.from_user.first_name}! ❤️. Soy NotesHub, un chatbot de inteligencia artificial. Recibo tus documentos pdf y luego interactúas sobre ellos conmigo. Anímate a probarme.\nEn el futuro tendré más funcionalidades, pero para seguir mejorando necesito seguir aprendiendo de ti y tus interacciones. Así que ¿Por qué no comenzamos?"
    await bot.send_message(msg.chat.id, reply_text, reply_markup=keyboard)
```

## Funciones de Procesamiento de Texto

Funciones auxiliares para el cálculo de tokens y costos asociados al procesamiento.

```py
# Función para calcular el número de tokens
def calc_n_tokens(text):
    encode = enc.encode(text)
    return len(encode)

# Función para calcular el costo asociado al resumen
def calc_total_cost(n_tokens):
    return float(str(n_tokens * cost_by_in_token + n_tokens * cost_by_out_token))
```

## Manejo de Mensajes de Usuario

```py
@dp.message_handler(content_types=ContentType.TEXT)
async def handle_text(message: types.Message):
    user_input = message.text
    user_id = message.from_user.id

    if MODE[user_id] == "chatting":
        # Lógica para manejar mensajes de texto en el modo "chatting"
    else:
        await message.answer("Por favor, suba un PDF. Si ya lo hizo y desea chatear, cambie de modo utilizando el comando /change_mode.")
```

## Manejo de Documentos PDF

Manejo de documentos PDF y lógica asociada para el resumen.

```py
@dp.message_handler(content_types=ContentType.DOCUMENT)
async def handle_document(message: types.Message):
    document = message.document
    user_id = message.from_user.id
    file_size = document.file_size
    file_name = document.file_name
    sentences_per_group = 4

    if is_summary_limit_positive(user_id):
        # Lógica para manejar documentos PDF
        ...
    else:
        await message.answer("Ha alcanzado el máximo de PDFs procesados de su prueba gratuita 😇. ¿Desearía adquirir la versión de pago de NotesHub?")
```

## Inicialización y Ejecución del Bot

```py
if __name__ == '__main__':
    MODE = {}
    USER_STATES = {}
    QUERY_STATE = {}
    OTHER_MODE = {}

    if os.path.getsize("MODE.json") >

```

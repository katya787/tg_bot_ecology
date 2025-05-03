# tg_bot_ecology
экологичный бот
import telebot
from telebot.types import Message
import random
from random import choice
import os
import requests


bot = telebot.TeleBot('')

citats = [
    "Использовать многоразовые сумки вместо пластиковых.  ",
    "Сортировать отходы для переработки.",
    "Выключать свет и электроприборы, когда они не нужны.",
    " Перемещаться пешком, на велосипеде или общественном транспорте.  ",
    "Сокращать использование одноразовой пластиковой посуды и бутылок.  ",
    "Сажать деревья и ухаживать за растениями.",
    "Использовать энергоэффективные лампочки и приборы.  ",
    "Избегать покупки товаров с излишней упаковкой.",
    "Поддерживать и участвовать в экологических акциях и субботниках.  ",
    "Выбирать натуральные и биоразлагаемые материалы.",
    "Перерабатывать бумагу, стекло и пластик.  ",
    "Использовать солнечные батареи и другие возобновляемые источники энергии.  ",
    "Не выбрасывать мусор в природу, особенно в лесах и у водоёмов.  ",
    "Устанавливать таймеры на полив растений, чтобы не тратить воду зря.  ",
    "Создавать места для птиц и насекомых в саду или на балконе.  ",
    " Обучать детей и близких бережному отношению к природе."
    ]

@bot.message_handler(commands=['start'])
def start_cmd(message: Message):
    bot.send_message(message.chat.id, 'Привет! я бот об охране природы. Напиши /help для дальнейшей инструкции')

@bot.message_handler(commands=['evidence'])
def evidence_cmd(message: Message):
    bot.send_message(message.chat.id, f": {random.choice(citats)}")

@bot.message_handler(commands=['picture'])
def picture_cmd(message: Message): 
    images = os.listdir('meme')
    image = random.choice(images)
    image = 'meme/' + image

    with open(image, 'rb') as file:
        bot.send_photo(message.chat.id, photo=file, caption='вот то, что происходит!')

@bot.message_handler(commands=['help'])
def help_cmd(message: Message):
    text = "<b>Мои команды:</b>\n " \
    "/start - <i>запуск бота</i>\n" \
    "/help - <i>все команды</i>\n " \
    "/evidence - <i>предложения по сохранению природы</i>\n" \
    " /picture - <i>картинки с неким смыслом</i> "
    bot.send_message(message.chat.id, text, parse_mode = 'html')






bot.infinity_polling()

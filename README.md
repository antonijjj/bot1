import telebot  
from random import randint  
from random import choice 
  
game_key_words = ['камень','ножницы','бумага'] 
user_points = 0 
bot_points = 0 
 
bot = telebot.TeleBot("6522215534:AAHuRrXR4_9wlskg7TGEjW7ZUnW2V60ZKZE")  
  
@bot.message_handler(commands=['start', 'help'])  
def send_welcome(message):  
 bot.send_message(message.chat.id, "1000 - 7 ZXC")  
  
@bot.message_handler(func=lambda message: message.text.lower() in game_key_words) 
def game1(message): 
    global user_points, bot_points 
    bot_choice = choice(game_key_words) 
    user_choice = message.text.lower() 
    if bot_choice == user_choice: 
        answer = 'Ничья' 
    elif (user_choice == 'камень' and bot_choice == 'ножницы') or \
            (user_choice == 'ножницы' and bot_choice == 'бумага') or \
            (user_choice == 'бумага' and bot_choice == 'камень'): 
        answer = 'Ты победил' 
        user_points += 1 
    else: 
        answer = 'Ты проиграл' 
        bot_points += 1 
             
    bot.send_message(message.chat.id, answer) 
 
#@bot.message_handler(func=lambda message: True)  
#def echo_all(message):  
# bot.send_message(message.chat.id,'хай') 
 
  
@bot.message_handler(func=lambda message: True)  
def echo_all(message):  
 bot.send_message(message.chat.id, message.text[::-1])  
  
bot.infinity_polling() 
 
 
 
 
 
 
 
 
 
 
#@bot.message_handler(commands=['random'])  
# m = message.text.split()  
 #n = randint(int(m)[1], int(m)[2])  
 #bot.send_message(message.chat.id, f"Рандомное число - {n}")

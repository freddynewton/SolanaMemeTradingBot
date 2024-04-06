import telebot
from tabulate import tabulate

# Verbinden mit dem Telegram-Bot
bot = telebot.TeleBot("DEIN_TELEGRAM_BOT_TOKEN")

# Kauforders
kauforders = [
    ["Wallet1", 3, -2, 5, -4, 2],
    ["Wallet2", 2, -3, 4, -5, 1],
    ["Wallet3", 4, -1, 6, -3, 3],
    ["Wallet4", 1, -4, 3, -6, 2],
    ["Wallet5", 5, -2, 4, -3, 1]
]

# Verkaufsorders und Stop-Loss-Werte
verkaufsorders = [
    ["Wallet1", 10, 8, 12, 6, 15, -8],
    ["Wallet2", 8, 6, 10, 5, 12, -6],
    ["Wallet3", 12, 10, 15, 8, 18, -10],
    ["Wallet4", 9, 7, 11, 6, 14, -7],
    ["Wallet5", 11, 9, 13, 7, 16, -9]
]

# Erstellen der Kauforders-Tabelle
kauf_table = tabulate(kauforders, headers=["Wallet", "Kauf 1", "Kauf 2", "Kauf 3", "Kauf 4", "Kauf 5"])
kauf_text = f"**Kauforders**\n\n{kauf_table}"

# Erstellen der Verkaufsorders-Tabelle
verkauf_table = tabulate(verkaufsorders, headers=["Wallet", "Verkauf 1", "Verkauf 2", "Verkauf 3", "Verkauf 4", "Verkauf 5", "MC%"])
verkauf_text = f"**Verkaufsorders und Stop-Loss-Werte**\n\n{verkauf_table}"

# Senden der Tabellen an den Telegram-Bot
@bot.message_handler(commands=['orders'])
def send_orders(message):
    bot.send_message(message.chat.id, kauf_text)
    bot.send_message(message.chat.id, verkauf_text)

# Starten des Telegram-Bots
bot.polling()

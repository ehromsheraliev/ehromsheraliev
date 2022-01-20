from telegram import ReplyKeyboardMarkup, InlineKeyboardButton, InlineKeyboardMarkup, Update
from telegram.ext import Updater, CommandHandler, CallbackQueryHandler, ConversationHandler, MessageHandler, Filters, CallbackContext
def start(update, context):  
  buttons = [
    [
      InlineKeyboardButton('Bizning kanal 📡', url='https://t.me/LessonsIT'),
      InlineKeyboardButton('Tekshirish ✅', callback_data='1')
    ]
  ]
  update.message.reply_html('Assalomu alaykum <b>{}</b>\n \n \nBizning botdan to`liq foydalanish uchun kanalimizga obuna bo`ling 👇👇👇'.
    format(update.message.from_user.first_name), reply_markup=InlineKeyboardMarkup(buttons))
  return 222
def inline_callback(update, context):
  try:
    query = update.callback_query
    query.message.delete()
    query.message.reply_html(text="<b>Assalomu alaykum</b>\n \n<em><b>Bo'limlardan birini tanlang 👇👇👇</b></em>")
  except Exception as e:
    print('error ', str(e))
updater = Updater('5026033665:AAFUCtBchsRaDcf6_szkQ53neGudI6lSA1w', use_context=True)
conv_handler = ConversationHandler(
  entry_points = [CommandHandler('start', start)],
        states={
            222: [CallbackQueryHandler(inline_callback)]
        },
  fallbacks=[MessageHandler(Filters.text, start)]
  )
updater.dispatcher.add_handler(conv_handler)
updater.start_polling()
updater.idle()

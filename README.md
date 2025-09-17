# Wallet-Hub-from telegram import Update
from telegram.ext import Application, CommandHandler, ContextTypes
import asyncio
import os

# دریافت توکن از Environment Variables
TOKEN = os.getenv('TELEGRAM_BOT_TOKEN')

async def start_command(update: Update, context: ContextTypes.DEFAULT_TYPE):
    loader_message = await update.message.reply_text("⏳ در حال پردازش...\n[----------] 0%")
    
    for progress in range(1, 11):
        await asyncio.sleep(0.5)
        percent = progress * 10
        bars = '█' * progress
        spaces = '░' * (10 - progress)
        await loader_message.edit_text(f"⏳ در حال پردازش...\n[{bars}{spaces}] {percent}%")
    
    await loader_message.edit_text("✅ پردازش کامل شد!")
    await update.message.reply_text("سلام! به ربات من خوش آمدید. 😊")

def main():
    app = Application.builder().token(TOKEN).build()
    app.add_handler(CommandHandler("start", start_command))
    print("✅ ربات فعال شد و در حال گوش دادن است...")
    app.run_polling()

if __name__ == '__main__':
    main()

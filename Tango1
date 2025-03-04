from flask import Flask, request, jsonify
import requests

app = Flask(__name__)

# ЗАМЕНИ {YOUR_TOKEN} на токен SaleBot
SALEBOT_API_URL = "https://chatter.salebot.pro/api/{979cb168ef6c0c76ea539615d72359b1}/message"

@app.route('/webhook', methods=['POST'])
def webhook():
    try:
        data = request.json  # Получаем JSON от Tilda

        # Извлекаем данные
        name = data.get("name", "Неизвестный")
        phone = data.get("phone", "Нет номера")
        email = data.get("email", "Нет email")
        amount = data.get("amount", "0")
        date = data.get("date", "Не указана")

        # Формируем сообщение
        message = f"💰 Новый платеж!\nИмя: {name}\nТелефон: {phone}\nEmail: {email}\nСумма: {amount} руб.\nДата: {date}"

        # Отправляем в SaleBot
        payload = {
            "message": message,
            "phone": phone
        }
        response = requests.post(SALEBOT_API_URL, json=payload)

        return jsonify({"status": "success", "saleBotResponse": response.json()}), 200

    except Exception as e:
        return jsonify({"status": "error", "message": str(e)}), 500

# Запуск сервера
if __name__ == '__main__':
    app.run(host='0.0.0.0', port=10000)

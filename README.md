# learn-rest
this project aims to provide a solid foundation for building REST APIs while remaining simple enough to understand in one sitting. It is well-suited for educational purposes, personal projects, and as a base template for more advanced backend applications.



Project structure
flask-api/
│
├── app.py
├── requirements.txt
└── README.md



app.py
pyton

from flask import Flask, jsonify, request

app = Flask(__name__)

# In-memory "database"
items = []

@app.route("/", methods=["GET"])
def home():
    return jsonify({
        "message": "Welcome to the Flask REST API 🚀"
    })

@app.route("/items", methods=["GET"])
def get_items():
    return jsonify(items)

@app.route("/items", methods=["POST"])
def add_item():
    data = request.get_json()

    if not data or "name" not in data:
        return jsonify({"error": "Item name is required"}), 400

    item = {
        "id": len(items) + 1,
        "name": data["name"]
    }
    items.append(item)
    return jsonify(item), 201

@app.route("/items/<int:item_id>", methods=["DELETE"])
def delete_item(item_id):
    global items
    items = [item for item in items if item["id"] != item_id]
    return jsonify({"message": "Item deleted"}), 200



    requirements.txt
    nginx
    
flask



README.md
# Flask REST API 🚀

A simple REST API built with Flask.

## Features
- Add items
- List items
- Delete items
- Beginner-friendly structure

## Installation
```bash
pip install -r requirements.txt
python app.py



API Endpoints

GET / – Home

GET /items – List items

POST /items – Add item

DELETE /items/<id> – Delete item

if __name__ == "__main__":
    app.run(debug=True)

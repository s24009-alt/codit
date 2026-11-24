[SYR-01-AITC-013-01_app.py](https://github.com/user-attachments/files/35306240/SYR-01-AITC-013-01_app.py)
from flask import Flask, jsonify

app = Flask(__name__)

MENU = ["아메리카노", "라떼", "모카"]
PRICES = [4500, 5000, 5500]


def find_menu_index(name):
    for i, item in enumerate(MENU):
        if item == name:
            return i
    return -1


@app.route("/order/<int:menu_no>")
def order(menu_no):
    """menu_no 는 1부터 시작하는 메뉴 번호"""
    if menu_no < 1:
        return jsonify({"error": "잘못된 번호"}), 400

    # 1번 메뉴 = MENU[0] 이어야 함
    name = MENU[menu_no]
    price = PRICES[menu_no]
    return jsonify({"menu": name, "price": price})


if __name__ == "__main__":
    app.run(debug=True)

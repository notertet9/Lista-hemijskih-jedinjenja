from flask import Flask, request, jsonify
import sqlite3

app = Flask(__name__)

def konekcija():
    conn = sqlite3.connect("database.db")
    conn.row_factory = sqlite3.Row
    return conn

@app.route("/dodaj", methods=["POST"])
def dodaj():
    data = request.json
    naziv = data.get("naziv")
    formula = data.get("formula")
    drugi = data.get("drugi_naziv")

    conn = konekcija()
    cursor = conn.cursor()
    try:
        cursor.execute("INSERT INTO jedinjenja (naziv, formula, drugi_naziv) VALUES (?, ?, ?)", (naziv, formula, drugi))
        conn.commit()
    except sqlite3.IntegrityError:
        return jsonify({"error": "Jedinjenje već postoji"}), 400
    conn.close()
    return jsonify({"status": "uspešno dodato"})

@app.route("/sva-jedinjenja", methods=["GET"])
def sva_jedinjenja():
    conn = konekcija()
    cursor = conn.cursor()
    cursor.execute("SELECT * FROM jedinjenja ORDER BY naziv ASC")
    jedinjenja = [dict(row) for row in cursor.fetchall()]
    conn.close()
    return jsonify(jedinjenja)

if __name__ == "__main__":
    app.run(host="0.0.0.0", port=5000)

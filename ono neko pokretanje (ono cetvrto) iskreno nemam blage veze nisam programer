import sqlite3

conn = sqlite3.connect("database.db")
cursor = conn.cursor()
cursor.execute("""
CREATE TABLE IF NOT EXISTS jedinjenja (
    id INTEGER PRIMARY KEY AUTOINCREMENT,
    naziv TEXT UNIQUE,
    formula TEXT,
    drugi_naziv TEXT
)
""")
conn.commit()
conn.close()

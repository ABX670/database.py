import json, os
from config import DATA_FILE

def load():
    if not os.path.exists(DATA_FILE):
        return {"users":{},"settings":{"bot_enabled":True,"games_locked":False,"group_locked":False,"banned_games":[]},"marriages":[]}
    with open(DATA_FILE, encoding="utf-8") as f:
        return json.load(f)

def save(db):
    with open(DATA_FILE,"w",encoding="utf-8") as f:
        json.dump(db,f,ensure_ascii=False,indent=2)

def get_user(db, num):
    if num not in db["users"]:
        db["users"][num]={"balance":100,"xp":0,"level":1,"wins":0,"bag":[],"gender":None,"banned_game":False,"is_admin":False}
    return db["users"][num]

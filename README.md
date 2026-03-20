from fastapi import FastAPI
from fastapi.middleware.cors import CORSMiddleware
from datetime import datetime
from fastapi.responses import JSONResponse

app = FastAPI()
app.add_middleware(CORSMiddleware, allow_origins=["*"])

@app.get("/")
def root():
    return {"message": "Sports API"}

@app.get("/api/nba")
def nba():
    try:
        from sports_skills import nba
        date = datetime.now().strftime("%Y-%m-%d")
        return nba.get_scoreboard(date=date)
    except Exception as e:
        return {"error": str(e)}

@app.get("/api/nfl")
def nfl():
    try:
        from sports_skills import nfl
        date = datetime.now().strftime("%Y-%m-%d")
        return nfl.get_scoreboard(date=date)
    except Exception as e:
        return {"error": str(e)}
## 🧩 Dependency Injection in FastAPI
FastAPI makes it super easy to manage shared logic or resources using Dependency Injection. This is useful for reusing code, like connecting to a database, checking permissions, or validating data across multiple endpoints.

## 📦 What is Dependency Injection?
Dependency Injection (DI) is a design pattern where dependencies (like a database or a function) are injected into parts of your code that need them, instead of being hardcoded.

In FastAPI, this is done using the Depends function.

🔧 Example

from fastapi import Depends, FastAPI

app = FastAPI()

# Dependency function
def common_parameters(q: str | None = None, skip: int = 0, limit: int = 10):
    return {"q": q, "skip": skip, "limit": limit}

# Injecting dependency
@app.get("/items/")
def read_items(commons: dict = Depends(common_parameters)):
    return commons
    
🗂 Output for /items/?q=books&skip=5

{
  "q": "books",
  "skip": 5,
  "limit": 10
}
🎯 Why use DI?
DRY (Don't Repeat Yourself) code

Centralized logic for parameters, authentication, DB connections, etc.

Cleaner, testable endpoints

## 🛠 Real-world Usage
from fastapi import Depends, HTTPException

def verify_token(token: str):
    if token != "secret":
        raise HTTPException(status_code=403, detail="Invalid token")
    return True

@app.get("/secure-data/")
def secure_data(verified: bool = Depends(verify_token)):
    return {"message": "Access granted"}
    
## ✅ Summary
FastAPI’s Depends makes it easy to:

Share logic across endpoints

Keep code clean and modular

Handle auth, params, or setup once and reuse


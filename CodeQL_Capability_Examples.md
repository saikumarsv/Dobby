## Python CodeQL Capability Examples

### SQL Injection
```python
import sqlite3
conn = sqlite3.connect("users.db")
user_input = input("Enter username:")
conn.execute("SELECT * FROM users WHERE name = '%s'" % user_input)  # Vulnerable
```

### OS Command Injection
```python
import os
filename = input("Enter filename:")
os.system("cat " + filename)  # Vulnerable
```

### XSS (Flask Example)
```python
from flask import Flask, request
app = Flask(__name__)
@app.route("/")
def home():
    name = request.args.get("name")
    return f"<h1>Hello {name}</h1>"  # Vulnerable
```

### Insecure Deserialization
```python
import pickle
data = input("Enter serialized data:")
obj = pickle.loads(data)  # Vulnerable
```

### Improper Crypto Usage
```python
from cryptography.fernet import Fernet
key = Fernet.generate_key()
cipher = Fernet(key)
encrypted = cipher.encrypt(b"secret")  # OK if key is secure, but often misused
```

## C++ CodeQL Capability Examples

### Buffer Overflow
```cpp
#include <cstring>
void vulnerable(char *input) {
    char buffer[10];
    strcpy(buffer, input); // Vulnerable
}
```

### Use-After-Free
```cpp
#include <iostream>
void test() {
    int* ptr = new int(5);
    delete ptr;
    std::cout << *ptr;  // Use-after-free
}
```

### Memory Leak
```cpp
void leak() {
    int* ptr = new int[100];
    // no delete => memory leak
}
```

### Null Pointer Dereference
```cpp
void func(int* ptr) {
    if (!ptr) return;
    *ptr = 42;  // OK
    // if check missing, this could be a vulnerability
}
```

### Command Injection
```cpp
#include <cstdlib>
void runCommand(std::string userInput) {
    std::string cmd = "ls " + userInput;
    system(cmd.c_str());  // Vulnerable
}
```


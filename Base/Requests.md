`requests` — это библиотека на Python для выполнения HTTP-запросов. Она позволяет легко отправлять запросы и получать данные с веб-серверов, обеспечивая удобный интерфейс для работы с HTTP.

## Основные HTTP-методы

### **1. GET — Получение данных**

GET-запрос используется для получения информации с сервера.

```python
import requests

response = requests.get("https://jsonplaceholder.typicode.com/posts/1")
print(response.status_code)  # HTTP-статус
print(response.json())       # JSON-ответ
```

### **2. POST — Отправка данных**

POST-запрос используется для отправки данных на сервер.

```python
data = {"title": "foo", "body": "bar", "userId": 1}
response = requests.post("https://jsonplaceholder.typicode.com/posts", json=data)
print(response.status_code)
print(response.json())
```

### **3. PUT — Обновление данных**

PUT-запрос используется для обновления данных на сервере.

```python
data = {"title": "updated title"}
response = requests.put("https://jsonplaceholder.typicode.com/posts/1", json=data)
print(response.json())
```

### **4. DELETE — Удаление данных**

DELETE-запрос используется для удаления данных с сервера.

```python
response = requests.delete("https://jsonplaceholder.typicode.com/posts/1")
print(response.status_code)  # 200 — успех, 204 — удалено
```

---

## Передача параметров и заголовков

### **1. Передача параметров в URL (GET)**

```python
params = {"userId": 1}
response = requests.get("https://jsonplaceholder.typicode.com/posts", params=params)
print(response.url)  # https://jsonplaceholder.typicode.com/posts?userId=1
```

### **2. Передача заголовков**

```python
headers = {"User-Agent": "my-app"}
response = requests.get("https://jsonplaceholder.typicode.com/posts/1", headers=headers)
print(response.request.headers)
```

### **3. Передача данных в теле запроса (form-data)**

```python
data = {"key": "value"}
response = requests.post("https://httpbin.org/post", data=data)
print(response.json())
```

---

## Работа с JSON

### **1. Отправка JSON**

```python
import json

data = {"name": "Alice"}
response = requests.post("https://httpbin.org/post", json=data)
print(response.json())
```

### **2. Получение JSON**

```python
response = requests.get("https://jsonplaceholder.typicode.com/users/1")
data = response.json()
print(data["name"])  # Вывод имени пользователя
```

---

## Обработка ошибок и исключений

```python
try:
    response = requests.get("https://httpbin.org/status/500", timeout=5)
    response.raise_for_status()  # Вызывает исключение для 4xx и 5xx
except requests.exceptions.RequestException as e:
    print(f"Ошибка: {e}")
```

---

## Работа с сессиями

Сессии позволяют сохранять состояние (например, куки) между запросами. Они полезны при авторизации и повторяющихся запросах к одному серверу.

```python
session = requests.Session()
session.headers.update({"Authorization": "Bearer TOKEN"})

response = session.get("https://httpbin.org/get")
print(response.json())
```

Сессии также позволяют сохранять куки между запросами:

```python
session.get("https://httpbin.org/cookies/set/sessioncookie/123456")
response = session.get("https://httpbin.org/cookies")
print(response.json())
```

---

## Работа с cookies

### **1. Получение cookies**

```python
response = requests.get("https://httpbin.org/cookies/set/sessioncookie/123456")
print(response.cookies.get_dict())
```

### **2. Отправка cookies**

```python
cookies = {"session_id": "123456"}
response = requests.get("https://httpbin.org/cookies", cookies=cookies)
print(response.json())
```

---

## Загрузка файлов

### **1. Сохранение файла**

```python
response = requests.get("https://www.example.com/image.jpg", stream=True)
with open("image.jpg", "wb") as file:
    for chunk in response.iter_content(1024):
        file.write(chunk)
```

### **2. Отправка файлов**

```python
files = {"file": open("test.txt", "rb")}
response = requests.post("https://httpbin.org/post", files=files)
print(response.json())
```

---

## Прокси и таймаут

### **1. Использование прокси**

```python
proxies = {"http": "http://10.10.1.10:3128", "https": "https://10.10.1.10:1080"}
response = requests.get("https://httpbin.org/ip", proxies=proxies)
print(response.json())
```

### **2. Таймаут запроса**

```python
try:
    response = requests.get("https://httpbin.org/delay/5", timeout=3)
except requests.exceptions.Timeout:
    print("Запрос превысил время ожидания")
```

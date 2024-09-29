Строки в Python — это **неизменяемые последовательности символов** (букв, цифр, пробелов, символов и т.д.), которые используются для хранения и манипуляции текстовой информации. Строки создаются с помощью одинарных (`'...'`) или двойных кавычек (`"..."`). Также можно использовать тройные кавычки (`'''...'''` или `"""..."""`) для создания многострочных строк.

Примеры строк:
```Python 
s1 = 'Привет, мир!'
s2 = "Это строка"
s3 = '''Многострочная
строка'''
```

## Неизменяемость строк
Строки в Python являются неизменяемыми, что означает, что после их создания изменить отдельные символы строки нельзя. Если необходимо изменить строку, создается новая строка.
```Python
s = "hello"
s[0] = 'H'  # Это вызовет ошибку, так как строки неизменяемы

```

Как и большинство итерируемых структур данных, строки поддерживают индексации и срезы.
```Python
s = "Hello"
print(s[0])  # 'H'
print(s[-1])  # 'o'

print(s[1:4])  # 'ell'
print(s[:2])   # 'He'
```

## Методы строк в Python

### 1. **`str.lower()` и `str.upper()`**
Эти методы используются для преобразования строки в нижний или верхний регистр соответственно.

**`lower()`**: Преобразует все символы в строке в нижний регистр.
```Python
text = "HELLO"
print(text.lower())  # 'hello'
```

**`upper()`**: Преобразует все символы в верхний регистр.
```Python
text = "hello"
print(text.upper())  # 'HELLO'
```

### 2. **`str.strip()`, `str.lstrip()`, `str.rstrip()`**
Эти методы удаляют пробелы (или указанные символы) с обоих концов строки, с начала или с конца.

**`strip()`**: Убирает пробелы с обоих концов строки.
```Python
text = "  hello  "
print(text.strip())  # 'hello'
```

**`lstrip()`**: Убирает пробелы только с начала строки.
```Python
text = "  hello"
print(text.lstrip())  # 'hello'
```

**`rstrip()`**: Убирает пробелы только с конца строки.
```Python
text = "hello  "
print(text.rstrip())  # 'hello'
```

### 3. **`str.replace()`**
Этот метод заменяет одно значение в строке на другое.

**`replace(old, new[, count])`**: Заменяет все вхождения подстроки `old` на подстроку `new`. Опционально можно указать максимальное количество замен через параметр `count`.
```Python
text = "Hello world"
print(text.replace("world", "Python"))  # 'Hello Python'
```

### 4. **`str.split()` и `str.join()`**
Эти методы используются для разбиения строки на части и для объединения элементов итерируемого объекта в строку.

**`split(sep=None, maxsplit=-1)`**: Разбивает строку на список подстрок по разделителю `sep`. Если `sep` не указан, используется пробел.
```Python
text = "apple,banana,orange"
fruits = text.split(",")
print(fruits)  # ['apple', 'banana', 'orange']
```

**`join(iterable)`**: Объединяет элементы списка или другого итерируемого объекта в строку с указанным разделителем.
```Python
fruits = ['apple', 'banana', 'orange']
result = ", ".join(fruits)
print(result)  # 'apple, banana, orange'
```

### 5. **`str.find()` и `str.rfind()`**
Эти методы используются для поиска подстроки в строке.

**`find(sub[, start[, end]])`**: Возвращает индекс первого вхождения подстроки `sub` в строке. Если подстрока не найдена, возвращает `-1`.
```Python
text = "Hello world"
index = text.find("world")
print(index)  # 6
```

**`rfind(sub[, start[, end]])`**: То же самое, но ищет с конца строки.
```Python
text = "Hello world, world"
index = text.rfind("world")
print(index)  # 13
```

### 6. **`str.startswith()` и `str.endswith()`**
Эти методы проверяют, начинается ли или заканчивается ли строка определённой подстрокой.

**`startswith(prefix[, start[, end]])`**: Проверяет, начинается ли строка с подстроки `prefix`.
```Python
text = "Hello world"
print(text.startswith("Hello"))  # True
```

**`endswith(suffix[, start[, end]])`**: Проверяет, заканчивается ли строка на подстроку `suffix`.
```Python
text = "Hello world"
print(text.endswith("world"))  # True
```

### 7. **`str.isdigit()`, `str.isalpha()`, `str.isalnum()`**
Эти методы проверяют содержимое строки.

**`isdigit()`**: Возвращает `True`, если строка состоит только из цифр.
```Python
text = "12345"
print(text.isdigit())  # True
```

**`isalpha()`**: Возвращает `True`, если строка состоит только из букв.
```Python
text = "Hello"
print(text.isalpha())  # True
```

**`isalnum()`**: Возвращает `True`, если строка состоит только из букв и цифр.
```Python
text = "Hello123"
print(text.isalnum())  # True
```

### 8. **`str.count()`**
Этот метод возвращает количество вхождений подстроки в строке.

**`count(sub[, start[, end]])`**: Подсчитывает количество вхождений подстроки `sub` в строке.
```Python
text = "Hello world, world"
print(text.count("world"))  # 2
```

### 9. **`str.capitalize()` и `str.title()`**
Эти методы изменяют регистр первого символа или каждого слова.

**`capitalize()`**: Преобразует первую букву строки в заглавную.
```Python
text = "hello"
print(text.capitalize())  # 'Hello'
```

**`title()`**: Преобразует первую букву каждого слова в заглавную.
```Python
text = "hello world"
print(text.title())  # 'Hello World'
```

### 10. **`str.format()`**
Этот метод используется для форматирования строк с подстановкой значений.

**`format(*args, **kwargs)`**: Вставляет значения в строку.
```Python
name = "John"
age = 25
print("My name is {} and I am {} years old.".format(name, age))
# 'My name is John and I am 25 years old.'
```
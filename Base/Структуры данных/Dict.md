Словари (англ. **dictionary**) - это изменяемые, неупорядоченные коллекции, которые хранят данные в виде пар "ключ-значение". Они позволяют быстро находить значения по ключам, используя хеширование. Структура данных `dict` реализована как хеш-таблица.
## Создание словаря
Словарь можно создать несколькими способами:
```python
# Пустой словарь
my_dict = {}

# Словарь с начальными значениями
my_dict = {'name': 'Alice', 'age': 25, 'city': 'New York'}

# Использование функции dict()
my_dict = dict(name='Alice', age=25, city='New York')

# Создание словаря с помощью списков пар
pairs = [('name', 'Alice'), ('age', 25), ('city', 'New York')]
my_dict = dict(pairs)
```

## Основные операции со словарями

#### Доступ к значению по ключу
```python
name = my_dict['name']  # 'Alice'
```

#### Изменение значения по ключу
```python
my_dict['age'] = 26
```

#### Добавление новой пары "ключ-значение"
```python
my_dict['email'] = 'alice@example.com'
```

#### Удаление пары "ключ-значение"
```python
del my_dict['city']
```

## Методы для работы со словарями 

#### `dict.get(key, default=None)`
Возвращает значение по ключу, если ключ существует. Если ключ не найден, возвращает значение `default` (по умолчанию `None`).
```python
my_dict = {'name': 'Alice', 'age': 25}
print(my_dict.get('name'))  # Output: Alice
print(my_dict.get('gender', 'Not specified'))  # Output: Not specified
```

#### `dict.keys()`
Возвращает объект представления (view object), содержащий все ключи словаря.
```python
keys = my_dict.keys()
print(keys)  # Output: dict_keys(['name', 'age'])
```

#### `dict.values()`
Возвращает объект представления, содержащий все значения словаря.
```python
values = my_dict.values()
print(values)  # Output: dict_values(['Alice', 25])
```

#### `dict.items()`
Возвращает объект представления, содержащий все пары "ключ-значение" словаря.
```python
items = my_dict.items()
print(items)  # Output: dict_items([('name', 'Alice'), ('age', 25)])
```

#### `dict.update([other])`
Обновляет словарь, добавляя пары "ключ-значение" из `other`, перезаписывая существующие ключи. `other` может быть другим словарем или итерируемым объектом пар "ключ-значение".
```python
my_dict.update({'age': 26, 'city': 'New York'})
print(my_dict)  # Output: {'name': 'Alice', 'age': 26, 'city': 'New York'}
```

#### `dict.pop(key, default=None)`
Удаляет ключ и возвращает его значение. Если ключ не найден, возвращает `default`. Если `default` не указан и ключ не найден, вызывает `KeyError`.
```python
age = my_dict.pop('age')
print(age)  # Output: 26
print(my_dict)  # Output: {'name': 'Alice', 'city': 'New York'}
```

#### `dict.popitem()`
Удаляет и возвращает последнюю добавленную пару "ключ-значение" из словаря. Если словарь пуст, вызывает `KeyError`.
```python
item = my_dict.popitem()
print(item)  # Output: ('city', 'New York')
print(my_dict)  # Output: {'name': 'Alice'}
```

#### `dict.setdefault(key, default=None)`
Если ключ существует, возвращает его значение. Если ключ не найден, добавляет его в словарь с указанным значением `default` и возвращает `default`.
```python
city = my_dict.setdefault('city', 'Unknown')
print(city)  # Output: Unknown
print(my_dict)  # Output: {'name': 'Alice', 'city': 'Unknown'}
```

#### `dict.clear()`
Удаляет все элементы из словаря.
```python
my_dict.clear()
print(my_dict)  # Output: {}
```

#### `dict.copy()`
Возвращает поверхностную копию словаря.
```python
new_dict = my_dict.copy()
print(new_dict)  # Output: {'name': 'Alice', 'city': 'Unknown'}
```

### Методы для работы с итераторами и представлениями

#### `dict.fromkeys(iterable, value=None)`
Создает новый словарь с ключами из `iterable` и значением `value` (по умолчанию `None`).
```python
keys = ['name', 'age', 'city']
new_dict = dict.fromkeys(keys, 'default')
print(new_dict)  # Output: {'name': 'default', 'age': 'default', 'city': 'default'}
```

### Вложенные словари
Словари могут содержать другие словари в качестве значений, что позволяет создавать сложные иерархии данных.
```python
nested_dict = {
    'person1': {'name': 'Alice', 'age': 25},
    'person2': {'name': 'Bob', 'age': 30}
}

# Доступ к вложенным значениям
print(nested_dict['person1']['name'])  # Output: Alice
```

[Memcached](http://danga.com/memcached/) представляет собой огромную хэш-таблицу в оперативной памяти, доступную по сетевому протоколу. Он обеспечивает сервис по хранению значений, ассоциированных с ключами. Доступ к хэшу мы получаем через простой сетевой протокол, клиентом может выступать программа, написанная на произвольном языке программирования (существуют клиенты для C/C++, PHP, Python, Java и т.п.).

## Как скачать и настроить Memcached

### 1. **Установка Memcached на Ubuntu**

1.1. Обновление списка пакетов:

```bash
sudo apt update
```

1.2. Установка Memcached:

```bash
sudo apt install memcached libmemcached-tools
```

1.3. Проверяем, что Memcached установлен и запущен:

```bash
sudo systemctl status memcached
```

1.4. Можно настроить сервер Memcached, отредактировав файл конфигурации:

```bash
sudo nano /etc/memcached.conf
```

Основные параметры:

- `-m` — объём памяти, выделяемый для Memcached (например, `-m 64` — 64 МБ).
- `-l` — IP-адрес, на котором будет работать Memcached (по умолчанию `127.0.0.1`).
- `-p` — порт (по умолчанию 11211).
- `-c` — максимальное количество одновременных подключений.

После внесения изменений, Memcached нужно перезапустить:

```bash
sudo systemctl restart memcached
```

### 2. **Проверка производительности**

После настройки и запуска приложения можно использовать утилиты, такие как `memcached-tool` или `stats` через Telnet, для проверки загрузки Memcached.

Для проверки статистики:

```bash
echo "stats" | nc 127.0.0.1 11211
```

## Базовые операции в Memcached

### **1. `set(key, value, exptime=0)`**

- **`key`** _(bytes)_ — ключ для хранения данных.
- **`value`** _(bytes)_ — значение, которое сохраняется.
- **`exptime`** _(int, по умолчанию 0)_ — время жизни ключа в секундах (0 = бесконечно).

### **2. `get(key)`**

- **`key`** _(bytes)_ — ключ, значение которого нужно получить.
- Возвращает значение (если ключ есть) или `None`.

### **3. `delete(key)`**

- **`key`** _(bytes)_ — ключ, который нужно удалить.

### **4. `add(key, value, exptime=0)`**

- Добавляет данные **только если ключа ещё нет**.
- Если ключ уже существует, ничего не делает.

### **5. `replace(key, value, exptime=0)`**

- Обновляет значение **только если ключ уже существует**.
- Если ключа нет, операция не выполнится.

### **6. `append(key, value)`**

- Добавляет `value` в конец текущего значения `key`.
- Работает только с уже существующими ключами.

### **7. `prepend(key, value)`**

- Добавляет `value` в начало текущего значения `key`.
- Работает только с уже существующими ключами.

### **8. `incr(key, delta)`**

- Увеличивает числовое значение ключа на `delta`.
- Ключ должен содержать **число** (иначе произойдёт ошибка).

### **9. `decr(key, delta)`**

- Уменьшает числовое значение ключа на `delta`.
- Если значение станет отрицательным, Memcached установит его в `0`.

### **10. `flush_all()`**

- Полностью очищает кэш.
- Удаляет **все ключи** сразу.

### Пример кода для каждой операции 

В примере я использую библиотеку `aiomcache` для Python3. Код, написанный на асинхронной библиотеке не сильно отличается от стандартной синхронной.

```Python
import asyncio
import aiomcache

async def main():
    client = aiomcache.Client("127.0.0.1", 11211)

    # 1. set - сохранение значения
    await client.set(b"username", b"john_doe", exptime=60)
    print("set: username = john_doe (на 60 секунд)")

    # 2. get - получение значения
    username = await client.get(b"username")
    print(f"get: username = {username.decode() if username else 'None'}")

    # 3. delete - удаление значения
    await client.delete(b"username")
    print("delete: username удалён")

    # 4. add - добавляет значение, но только если ключ НЕ существует
    success = await client.add(b"username", b"new_user", exptime=30)
    print(f"add: username добавлен: {success}")

    # 5. replace - заменяет значение, но только если ключ уже существует
    success = await client.replace(b"username", b"updated_user", exptime=30)
    print(f"replace: username заменён: {success}")

    # 6. append - добавляет данные в конец существующего значения
    await client.append(b"username", b"_appended")
    updated_value = await client.get(b"username")
    print(f"append: username = {updated_value.decode()}")

    # 7. prepend - добавляет данные в начало существующего значения
    await client.prepend(b"username", b"prepended_")
    updated_value = await client.get(b"username")
    print(f"prepend: username = {updated_value.decode()}")

    # 8. incr - увеличение числового значения
    await client.set(b"counter", b"10")  # Устанавливаем начальное значение
    await client.incr(b"counter", 5)
    counter = await client.get(b"counter")
    print(f"incr: counter = {counter.decode()}")

    # 9. decr - уменьшение числового значения
    await client.decr(b"counter", 3)
    counter = await client.get(b"counter")
    print(f"decr: counter = {counter.decode()}")

    # 10. flush_all - очистка всего кэша
    await client.flush_all()
    print("flush_all: кэш очищен")

    await client.close()

asyncio.run(main())

```
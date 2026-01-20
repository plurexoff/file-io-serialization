# Задание №3: Работа с файлами и потоками ввода-вывода

Получение навыков работы с файлами и сериализацией данных.

## 📋 Цель

1. Изучить методы открытия файлов и чтения/записи данных
2. Создать приложение, которое записывает двоичные данные в файл и читает их обратно
3. Применить сериализацию и десериализацию собственных объектов (Python `pickle`, Java `ObjectOutputStream`)

## 📁 Структура проекта

```
file-io-serialization/
├── README.md
├── python/
│   ├── binary_io.py           # Работа с двоичными данными
│   ├── pickle_serialization.py # Сериализация объектов pickle
│   ├── csv_handler.py          # Работа с CSV файлами
│   └── examples.py             # Примеры использования
├── java/
│   ├── BinaryIO.java           # Работа с двоичными данными
│   ├── ObjectSerialization.java # Сериализация объектов Java
│   └── CSVHandler.java         # Работа с CSV файлами
└── data/                       # Директория для тестовых данных
    ├── .gitkeep
```

## 🐍 Python примеры

### 1. Двоичный ввод-вывод

```python
# Запись двоичных данных
with open('data.bin', 'wb') as f:
    data = bytes([1, 2, 3, 4, 5])
    f.write(data)

# Чтение двоичных данных
with open('data.bin', 'rb') as f:
    data = f.read()
    print(data)
```

### 2. Сериализация объектов (Pickle)

```python
import pickle

class Person:
    def __init__(self, name, age):
        self.name = name
        self.age = age

# Сериализация
person = Person("Иван", 30)
with open('person.pkl', 'wb') as f:
    pickle.dump(person, f)

# Десериализация
with open('person.pkl', 'rb') as f:
    loaded_person = pickle.load(f)
    print(f"{loaded_person.name}, {loaded_person.age}")
```

## ☕ Java примеры

### 1. Двоичный ввод-вывод

```java
// Запись двоичных данных
FileOutputStream fos = new FileOutputStream("data.bin");
byte[] data = {1, 2, 3, 4, 5};
fos.write(data);
fos.close();

// Чтение двоичных данных
FileInputStream fis = new FileInputStream("data.bin");
byte[] buffer = new byte[5];
fis.read(buffer);
fis.close();
```

### 2. Сериализация объектов (ObjectOutputStream)

```java
class Person implements Serializable {
    private String name;
    private int age;
    
    public Person(String name, int age) {
        this.name = name;
        this.age = age;
    }
}

// Сериализация
Person person = new Person("Иван", 30);
FileOutputStream fos = new FileOutputStream("person.dat");
ObjectOutputStream oos = new ObjectOutputStream(fos);
oos.writeObject(person);
oos.close();

// Десериализация
FileInputStream fis = new FileInputStream("person.dat");
ObjectInputStream ois = new ObjectInputStream(fis);
Person loaded = (Person) ois.readObject();
ois.close();
```

## 🔑 Ключевые концепции

### Потоки ввода-вывода (Streams)

| Тип потока | Назначение | Пример |
|-----------|-----------|--------|
| **FileInputStream/FileOutputStream** | Работа с файлами в двоичном режиме | Читать/писать байты |
| **FileReader/FileWriter** | Работа с текстовыми файлами | Читать/писать текст |
| **ObjectInputStream/ObjectOutputStream** | Сериализация объектов | Сохранять сложные объекты |
| **BufferedInputStream/BufferedOutputStream** | Буферизированный ввод-вывод | Оптимизация производительности |

### Сериализация

**Определение:** Процесс преобразования объекта в последовательность байтов для сохранения или передачи.

**Преимущества:**
- Сохранение состояния объекта
- Передача по сети
- Кэширование данных

**Типы:**
- **Python**: `pickle` (встроенный модуль)
- **Java**: `Serializable` интерфейс

### Обработка исключений

```python
# Python
try:
    with open('file.txt', 'r') as f:
        data = f.read()
except FileNotFoundError:
    print("Файл не найден")
except IOError as e:
    print(f"Ошибка ввода-вывода: {e}")
```

```java
// Java
try {
    FileInputStream fis = new FileInputStream("file.txt");
    // работа с файлом
} catch (FileNotFoundException e) {
    System.out.println("Файл не найден");
} catch (IOException e) {
    System.out.println("Ошибка ввода-вывода: " + e.getMessage());
} finally {
    // очистка ресурсов
}
```

## 🚀 Запуск примеров

### Python

```bash
# Установка зависимостей (если требуется)
pip install -r requirements.txt

# Запуск примеров
python python/examples.py
```

### Java

```bash
# Компиляция
javac java/*.java

# Запуск
java -cp java/ BinaryIO
java -cp java/ ObjectSerialization
```

## 📚 Что изучим

- ✅ Открытие и закрытие файлов
- ✅ Чтение и запись двоичных данных
- ✅ Работа с текстовыми файлами
- ✅ Сериализация объектов
- ✅ Десериализация объектов
- ✅ Обработка исключений при работе с файлами
- ✅ Буферизация для оптимизации производительности
- ✅ Работа с потоками ввода-вывода

## 💡 Полезные ресурсы

- [Python File I/O](https://docs.python.org/3/tutorial/inputoutput.html#reading-and-writing-files)
- [Python pickle](https://docs.python.org/3/library/pickle.html)
- [Java File I/O](https://docs.oracle.com/javase/tutorial/i18n/resbundle/propfile.html)
- [Java Serialization](https://docs.oracle.com/javase/tutorial/jndi/objects/ser.html)

## 📝 Лицензия

MIT

---

**Дата создания:** 2026-01-20
**Статус:** В разработке

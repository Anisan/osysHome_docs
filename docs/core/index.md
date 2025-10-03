---
title: Архитектура
layout: home
nav_order: 4
---

# Архитектура системы объектов
Система osysHome построена на компонентах управления объектами:

## Классы (Classes)
Классы определяют структуру объектов и поддерживают наследование через parent_id.

Создание класса с наследованием:
```
addClass("ChildClass", "Description", parentId=parent_class_id)
```
## Объекты (Objects)
Объекты создаются на основе классов и управляются через ObjectManager

## Свойства (Properties)

### Типы свойств
Система поддерживает следующие типы данных с автоматическим преобразованием:

|Тип|Преобразование|Формат хранения
|-------|-----|-------|
int|	int(value)|	Строковое представление
float|	float(value)|	Строковое представление
str|	Прямое присвоение|	Исходная строка
datetime|	parser.parse() с UTC|	ISO формат
dict|	json.loads()|	JSON строка
list|	json.loads()|	JSON строка
bool|	Парсинг строк (true/false)|	Строковое представление

### Наследование свойств
Система загружает свойства рекурсивно по иерархии классов

## Методы (Methods)
Создание методов
Методы содержат Python код и поддерживают наследование: object.py:108-136

### Выполнение методов
Методы выполняются в контролируемой среде с предопределенными переменными

Доступные переменные в методах:

* self - ссылка на ObjectManager
* params - параметры метода
* logger - экземпляр логгера
* source - источник вызова

### Наследование методов
Методы загружаются рекурсивно по иерархии классов

## Шаблоны (Templates)

### Наследование шаблонов
Шаблоны наследуются от родительских классов и используются для рендеринга объектов

### Рендеринг шаблонов
Система использует Jinja2 для рендеринга с поддержкой наследования

## Связывание с модулями
Свойства могут быть связаны с внешними плагинами для двунаправленной синхронизации

Примеры использования
Создание класса с наследованием
```python
# Создание родительского класса  
parent_class = addClass("Device", "Base device class")  
  
# Создание дочернего класса  
child_class = addClass("Sensor", "Sensor device", parent_class['id'])  
  
# Добавление свойства к классу  
addClassProperty("temperature", "Sensor", "Temperature value",   
                history=7, type=PropertyType.Float, method_name="onTempChange")
Работа с объектами и свойствами
# Создание объекта  
sensor = addObject("LivingRoomSensor", "Sensor", "Temperature sensor in living room")  
  
# Установка значения свойства  
setProperty("LivingRoomSensor.temperature", 23.5, "sensor_module")  
  
# Получение значения  
temp = getProperty("LivingRoomSensor.temperature")  
  
# Связывание с модулем  
setLinkToObject("LivingRoomSensor", "temperature", "mqtt_plugin")
```
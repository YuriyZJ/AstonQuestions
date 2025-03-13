# Patterns

+ [1. Фабричный метод (Factory Method)](#1-фабричный-метод-factory-method)
+ [2. Абстрактная фабрика (Abstract Factory)](#2-абстрактная-фабрика-abstract-factory)
+ [3. Строитель (Builder)](#3-строитель-builder)
+ [4. Прототип (Prototype)](#4-прототип-prototype)
+ [5. Одиночка (Singleton)](#5-одиночка-singleton)
+ [6. Адаптер (Adapter)](#6-адаптер-adapter)
+ [7. Мост (Bridge)](#7-мост-bridge)
+ [8. Компоновщик (Composite)](#8-компоновщик-composite)
+ [9. Декоратор (Decorator)](#9-декоратор-decorator)
+ [10. Фасад (Facade)](#10-фасад-facade)
+ [11. Легковес (Lightweight)](#11-легковес-lightweight)
+ [12. Заместитель (Proxy)](#12-заместитель-proxy)
+ [13. Цепочка обязанностей (Chain of responsibility)](#13-цепочка-обязанностей-chain-of-responsibility)
+ [14. Команда (Command)](#14-команда-command)
+ [15. Итератор (Iterator)](#15-итератор-iterator)
+ [16. Посредник (Mediator)](#16-посредник-mediator)
+ [17. Снимок (Memento)](#17-снимок-memento)
+ [18. Наблюдатель (Observer)](#18-наблюдатель-observer)
+ [19. Состояние (State)](#19-состояние-state)
+ [20. Стратегия (Strategy)](#20-стратегия-strategy)
+ [21. Шаблонный Метод (Template Method)](#21-шаблонный-метод-template-method)
+ [22. Посетитель (Visitor)](#22-посетитель-visitor)

---

## Порождающие (Creational) (1-5)
Используются для управления созданием объектов, скрывая при этом логику его создания.
Шаблоны фокусируются на процессе создания объектов при разработке программного обеспечения. Эти шаблоны гарантируют, что мы создаем вещи не только простым, но и гибким способом, поэтому мы можем изменить их позже, если нам тоже понадобится. Они скрывают сложные детали того, как мы соединяем их вместе.

### 1. Фабричный метод (Factory Method)
[к оглавлению](#patterns)

### 2. Абстрактная фабрика (Abstract Factory)
[к оглавлению](#patterns)

---

### 3. Строитель (Builder)
Паттерн Builder (Строитель) позволяет пошагово создавать сложные объекты. Используется, когда объект имеет много параметров и его создание может быть сложным. Вместо длинного конструктора с кучей аргументов, пошагово настраиваем объект с помощью методов билдера.
Когда использовать?
- Когда объект сложный (много обязательных и опциональных параметров).
- Когда нужно сделать код читабельным и понятным.
- Когда нужно избежать длинного конструктора (telescoping constructor).

__Пример без Builder (Как не надо)__

    class Car {
        private String engine;
        private int wheels;
        private boolean airConditioning;
    
        public Car(String engine, int wheels, boolean airConditioning) {
            this.engine = engine;
            this.wheels = wheels;
            this.airConditioning = airConditioning;
        }
    }
        Car car = new Car("V8", 4, true); // Непонятно, что за параметры!
__Минусы:__
- Сложно читать, особенно если у конструктора много аргументов.
- Проблемы с изменением параметров – придется менять конструктор.

__Используем паттерн Builder (Как правильно)__

    class Car {
        private String engine;
        private int wheels;
        private boolean airConditioning;

        private Car(CarBuilder builder) {
            this.engine = builder.engine;
            this.wheels = builder.wheels;
            this.airConditioning = builder.airConditioning;
        }
    
        public static class CarBuilder {
            private String engine;
            private int wheels;
            private boolean airConditioning;
    
            public CarBuilder(String engine, int wheels) { // Обязательные параметры
                this.engine = engine;
                this.wheels = wheels;
            }
    
            public CarBuilder setAirConditioning(boolean airConditioning) { // Опциональный параметр
                this.airConditioning = airConditioning;
                return this;
            }
    
            public Car build() { // Финальный метод для сборки объекта
                return new Car(this);
            }
        }
    
        @Override
        public String toString() {
            return "Car{" + "engine='" + engine + '\'' + ", wheels=" + wheels + ", airConditioning=" + airConditioning + '}';
        }
    }

Используем:

    Car car = new Car.CarBuilder("V8", 4)
                .setAirConditioning(true)
                .build();

    System.out.println(car);

__Как здесь применены принципы SOLID?__
1. S (Single Responsibility) - Принцип единственной ответственности
   Класс Car только хранит данные, а создание объекта вынесено в CarBuilder.
2. O (Open/Closed) - Принцип открытости/закрытости
   Car закрыт для модификации, но можно легко добавлять новые параметры в CarBuilder.
3. L (Liskov Substitution) - Принцип подстановки Барбары Лисков
   Здесь не используются наследование и подтипы, но объекты Car ведут себя предсказуемо.
4. I (Interface Segregation) - Принцип разделения интерфейсов
   У CarBuilder нет ненужных методов – он предоставляет только нужные методы для сборки.
5. D (Dependency Inversion) - Принцип инверсии зависимостей
   Car не зависит от конкретных реализаций, а взаимодействует с CarBuilder.

[к оглавлению](#patterns)

---

### 4. Прототип (Prototype)
[к оглавлению](#patterns)

### 5. Одиночка (Singleton)
[к оглавлению](#patterns)

---

## Структурные (Structural) (6-12)
Определяют, как классы и объекты могут быть объединены.
Шаблон подобен рецепту объединения различных объектов и классов для создания более крупной структуры. Это немного похоже на следование чертежу при строительстве дома. Эти шаблоны учат нас объединять уникальные части системы таким образом, чтобы их было легко изменять и расширять, не затрагивая всю систему.

### 6. Адаптер (Adapter)
[к оглавлению](#patterns)

### 7. Мост (Bridge)
[к оглавлению](#patterns)

### 8. Компоновщик (Composite)
[к оглавлению](#patterns)

### 9. Декоратор (Decorator)
[к оглавлению](#patterns)

### 10. Фасад (Facade)
[к оглавлению](#patterns)

### 11. Легковес (Lightweight)
[к оглавлению](#patterns)

### 12. Заместитель (Proxy)
[к оглавлению](#patterns)

---

## Поведенческие (Behavioural) (13-22)
Определяют способы взаимодействия объектов.
Шаблоны помогают решать распространенные проблемы, связанные с тем, как фрагменты кода разделяют задачи, скрывают, что они делают, и остаются организованными. Когда разработчики используют эти шаблоны, это похоже на сборку головоломки, где части легко складываются вместе, что делает программное обеспечение более организованным, его легко менять и с меньшей вероятностью сломается, когда нам нужно что-то добавить или изменить. Таким образом, это похоже на руководство по обеспечению бесперебойной работы всех частей вашего программного обеспечения.

### 13. Цепочка обязанностей (Chain of responsibility)
[к оглавлению](#patterns)

### 14. Команда (Command)
[к оглавлению](#patterns)

### 15. Итератор (Iterator)
[к оглавлению](#patterns)

### 16. Посредник (Mediator)
[к оглавлению](#patterns)

### 17. Снимок (Memento)
[к оглавлению](#patterns)

### 18. Наблюдатель (Observer)
[к оглавлению](#patterns)

### 19. Состояние (State)
[к оглавлению](#patterns)

### 20. Стратегия (Strategy)
[к оглавлению](#patterns)

### 21. Шаблонный Метод (Template Method)
[к оглавлению](#patterns)

### 22. Посетитель (Visitor)
[к оглавлению](#patterns)

---

[← Вернуться к вопросам](README.md)
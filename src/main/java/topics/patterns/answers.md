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

**Фабричный метод** — это **порождающий** паттерн проектирования, который определяет **общий интерфейс** для создания 
объектов в суперклассе, позволяя подклассам изменять тип создаваемых объектов.

**Проблемы, которые решает Фабричный метод:**

- Отделение кода создания объектов от их использования.
- Упрощение добавления новых типов продуктов без изменения существующего кода, который их использует.

**Шаги реализации**
1. Приведите все создаваемые продукты к **общему интерфейсу**.
2. В классе, который производит продукты, создайте пустой **фабричный метод**. В качестве возвращаемого типа укажите 
**общий интерфейс продукта**.
3. Затем пройдитесь по коду класса и найдите все участки, **создающие продукты**. Поочерёдно замените эти участки вызовами
**фабричного метода**, перенося в него код создания различных продуктов.
- В фабричный метод, возможно, придётся добавить несколько параметров, **контролирующих**, какой из продуктов нужно создать.
На этом этапе фабричный метод, скорее всего, будет выглядеть удручающе. В нём будет жить большой условный оператор, 
выбирающий класс создаваемого продукта.
4. Для каждого типа продуктов заведите **подкласс** и переопределите в нём фабричный метод. Переместите туда код создания 
соответствующего продукта из суперкласса.
5. Если создаваемых продуктов слишком много для существующих подклассов создателя, вы можете подумать о введении
параметров в фабричный метод, которые позволят возвращать различные продукты в пределах одного подкласса.
- Например, у вас есть класс **Почта** с подклассами **АвиаПочта** и **НаземнаяПочта**, а также классы продуктов 
**Самолёт**, **Грузовик** и **Поезд**. **Авиа** соответствует **Самолётам**, но для **НаземнойПочты** есть сразу два 
продукта. Вы могли бы создать новый подкласс почты для поездов, но проблему можно решить и по-другому. Клиентский код
может передавать в фабричный метод **НаземнойПочты** аргумент, контролирующий тип создаваемого продукта.
6. Если после всех перемещений фабричный метод стал пустым, можете сделать его абстрактным. Если в нём что-то осталось —
не беда, это будет его реализацией по умолчанию.

**Преимущества**
- Избавляет класс от привязки к конкретным классам продуктов.
- Выделяет код производства продуктов в одно место, упрощая поддержку кода.
- Упрощает добавление новых продуктов в программу.
- Реализует принцип открытости/закрытости.

**Недостатки**
- Может привести к созданию больших параллельных **иерархий классов**, так как для каждого 
класса продукта надо создать свой подкласс создателя.

**РЕАЛИЗАЦИЯ**
``` java
// Паттерн Фабричный метод применим тогда, когда в программе
// есть иерархия классов продуктов.
interface Button is
method render()
method onClick(f)

class WindowsButton implements Button is
method render(a, b) is
// Отрисовать кнопку в стиле Windows.
method onClick(f) is
// Навесить на кнопку обработчик событий Windows.

class HTMLButton implements Button is
method render(a, b) is
// Вернуть HTML-код кнопки.
method onClick(f) is
// Навесить на кнопку обработчик события браузера.


// Базовый класс фабрики. Заметьте, что "фабрика" — это всего
// лишь дополнительная роль для класса. Скорее всего, он уже
// имеет какую-то бизнес-логику, в которой требуется создание
// разнообразных продуктов.
class Dialog is
method render() is
// Чтобы использовать фабричный метод, вы должны
// убедиться в том, что эта бизнес-логика не зависит от
// конкретных классов продуктов. Button — это общий
// интерфейс кнопок, поэтому все хорошо.
Button okButton = createButton()
okButton.onClick(closeDialog)
okButton.render()

    // Мы выносим весь код создания продуктов в особый метод,
    // который назвают "фабричным".
    abstract method createButton():Button


// Конкретные фабрики переопределяют фабричный метод и
// возвращают из него собственные продукты.
class WindowsDialog extends Dialog is
method createButton():Button is
return new WindowsButton()

class WebDialog extends Dialog is
method createButton():Button is
return new HTMLButton()


class Application is
field dialog: Dialog

    // Приложение создаёт определённую фабрику в зависимости от
    // конфигурации или окружения.
    method initialize() is
        config = readApplicationConfigFile()

        if (config.OS == "Windows") then
            dialog = new WindowsDialog()
        else if (config.OS == "Web") then
            dialog = new WebDialog()
        else
            throw new Exception("Error! Unknown operating system.")

    // Если весь остальной клиентский код работает с фабриками и
    // продуктами только через общий интерфейс, то для него
    // будет не важно, какая фабрика была создана изначально.
    method main() is
        this.initialize()
        dialog.render()
```

[к оглавлению](#patterns)

---

### 2. Абстрактная фабрика (Abstract Factory)
Паттерн “Абстрактная фабрика” (Abstract Factory)
Абстрактная фабрика — это порождающий паттерн проектирования, который предоставляет интерфейс для создания семейств взаимосвязанных объектов без привязки к конкретным классам.
Когда использовать этот паттерн?
- Когда система должна быть независимой от способа создания и компоновки продуктов.
- Когда нужно предоставить пользователям интерфейс для создания семейств связанных объектов.
- Когда конкретные классы должны быть скрыты от клиента.

__Пример без Abstract Factory (Как не надо)__. Здесь клиентский код жестко привязан к конкретным классам, что нарушает OCP (Open-Closed Principle).

``` java
// Классы продуктов (конкретные реализации)
class WindowsButton {
      void render() {
         System.out.println("Рисуем кнопку для Windows");
      }
}

class MacOSButton {
      void render() {
         System.out.println("Рисуем кнопку для MacOS");
      }
}

// Клиентский код жёстко зависит от конкретных классов
public class Application {
    private WindowsButton button;

    public Application() {
        button = new WindowsButton(); // Жесткая привязка к реализации
    }

    public void renderUI() {
        button.render();
    }

    public static void main(String[] args) {
        Application app = new Application();
        app.renderUI(); // Работает только с WindowsButton
    }
}
```
Что тут не так?
- Нарушение OCP – если захотим добавить поддержку MacOS, придется менять клиентский код.
- Проблемы с тестированием – код жестко зависит от конкретных классов.
- Слабая расширяемость – для новых платформ придется модифицировать классы.

__Пример с Abstract Factory__
``` java
// 1. Абстрактный интерфейс для кнопок
interface Button {
      void render();
}

// 2. Конкретные реализации кнопок
class WindowsButton implements Button {
      @Override
      public void render() {
         System.out.println("Рисуем кнопку для Windows");
      }
}

class MacOSButton implements Button {
      @Override
      public void render() {
         System.out.println("Рисуем кнопку для MacOS");
      }
}

// 3. Абстрактная фабрика, определяющая создание элементов интерфейса
interface GUIFactory {
      Button createButton();
}

// 4. Конкретные фабрики для каждой ОС
class WindowsFactory implements GUIFactory {
      @Override
      public Button createButton() {
         return new WindowsButton();
      }
}

class MacOSFactory implements GUIFactory {
   @Override
   public Button createButton() {
      return new MacOSButton();
   }
}

// 5. Клиентский код, который теперь НЕ зависит от конкретных классов
class Application {
   private final Button button;

    // Конструктор принимает фабрику, а не конкретный класс
    public Application(GUIFactory factory) {
        this.button = factory.createButton();
    }

    public void renderUI() {
        button.render();
    }
}

// 6. Создаем правильную фабрику и запускаем приложение
public class Main {
   public static void main(String[] args) {
        GUIFactory factory;

        // Определяем, какую фабрику использовать (можно заменить на чтение из конфига)
        String osType = "Windows"; // MacOS

        if (osType.equals("Windows")) {
            factory = new WindowsFactory();
        } else {
            factory = new MacOSFactory();
        }

        // Передаем фабрику в приложение
        Application app = new Application(factory);
        app.renderUI();
    }
}
```
Как здесь применены принципы SOLID?
1. S (Single Responsibility Principle, Принцип единственной ответственности). Каждый класс отвечает только за свою зону ответственности (фабрика создает объекты, кнопки отрисовываются).
2. O (Open-Closed Principle, Принцип открытости-закрытости). Теперь можно добавлять новые типы кнопок и фабрик без изменения существующего кода.
3. L (Liskov Substitution Principle, Принцип подстановки Барбары Лисков). Объекты WindowsButton и MacOSButton заменяют Button без изменений в клиентском коде.
4. I (Interface Segregation Principle, Принцип разделения интерфейсов). Интерфейс Button не перегружен ненужными методами.
5. D (Dependency Inversion Principle, Принцип инверсии зависимостей). Клиентский код зависит от абстракции (GUIFactory), а не от конкретных классов (WindowsButton, MacOSButton).


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
**Prototype** — это **порождающий** паттерн, который позволяет создавать новые объекты путём копирования существующего
объекта. Он используется в случаях, когда приложению нужно создать несколько экземпляров класса, которые имеют почти
одинаковое состояние или очень мало отличаются.

Паттерн Прототип реализован в базовой библиотеке Java посредством интерфейса Cloneable. Любой класс может реализовать этот
интерфейс, чтобы позволить собственное клонирование.

**Компоненты паттерна:**
1. Интерфейс или абстрактный класс, который объявляет метод клонирования. Используется как шаблон для создания новых объектов.
2. Класс, который реализует интерфейс прототипа или расширяет абстрактный класс. Представляет конкретный тип объекта,
   который нужно клонировать. Определяет детали процесса клонирования для экземпляров этого класса.
3. Код или модуль, который запрашивает создание новых объектов путём взаимодействия с прототипом.

#### **Реализация:**

```java
// Определяем интерфейс, который служит прототипом для наших объектов.
public interface Sheep {
   Sheep clone();  //Метод clone для создания копий объектов.
   String getName();
   void setName(String name);
}

/* Создаем конкретные классы объекта, реализующие интерфейс Sheep. Эти конкретные классы представляют определенные типы 
объектов и предоставляют свои собственные реализации clone. */
public class BlackSheep implements Sheep {
   private String name;
   public BlackSheep(String name) {
      this.name = name;
   }
   public Sheep clone() {
      return new BlackSheep(this.name);
   }
   public String getName() {
      return name;
   }
   public void setName(String name) {
      this.name = name;
   }
}
public class WhiteSheep implements Sheep {
   private String name;
   public WhiteSheep(String name) {
      this.name = name;
   }
   public Sheep clone() {
      return new WhiteSheep(this.name);
   }
   public String getName() {
      return name;
   }
   public void setName(String name) {
      this.name = name;
   }
}

// Создаем прототипы объектов, клонируем их и настраиваем клонированные объекты по мере необходимости.
public class SheepFarm {
   public static void main(String[] args) {
      // Создаем прототип объектов
      Sheep blackPrototype = new BlackSheep("Baa Baa");
      Sheep whitePrototype = new WhiteSheep("Fleecy");
      // Клонируем объекты по мере необходимости
      Sheep clonedBlackSheep = blackPrototype.clone();
      Sheep clonedWhiteSheep = whitePrototype.clone();
      // Настройка клонированных объектов
      clonedBlackSheep.setName("Midnight");
      clonedWhiteSheep.setName("Snowball");
      // Выводим информацию измененных объектов
      System.out.println("Black sheep: " + clonedBlackSheep.getName());
      System.out.println("White sheep: " + clonedWhiteSheep.getName());
   }
}
```
#### **Плюсы и минусы шаблона Прототип.**

**Плюсы:**
1. Простое клонирование объектов: шаблон позволяет создавать новые объекты путем копирования существующих, что
   способствует повторному использованию кода. Это очень полезно, если объекты имеют сложные или ресурсоемкие процессы
   инициализации.
2. Сокращение накладных расходов на инициализацию. Поскольку объекты клонируются, а не создаются с нуля, это может
   значительно снизить накладные расходы, связанные с дорогостоящей инициализацией объектов.
3. Индивидуальная настройка: клонированные объекты можно легко настроить в соответствии с конкретными требованиями,
   сохраняя при этом общие характеристики прототипа. Это обеспечивает гибкость при создании объектов.
4. Оптимизированное создание объектов: шаблон обеспечивает структурированный и последовательный способ создания
   объектов, что делает базу кода более организованной и простой в обслуживании.
5. Минимизированная логика создания сложных объектов. Шаблон Прототип абстрагирует логику создания сложных объектов от
   клиентского кода, что приводит к более чистому и удобочитаемому коду.

**Минусы:**
1. Поверхностное и глубокое копирование. В сценариях, где объекты содержат ссылки на другие объекты (например, вложенные
   объекты), клонирование по умолчанию может привести к созданию неглубоких копий. Это означает, что изменения вложенных
   объектов в клонированном объекте могут повлиять на исходный объект и наоборот. Может потребоваться глубокое копирование,
   которое иногда сложно реализовать.
2. Управление состоянием объекта. Если объект имеет внутреннее состояние, которое не должно использоваться несколькими
   клонами, необходимо тщательное управление состоянием объекта, чтобы гарантировать, что каждый клон сохраняет свою
   целостность.
3. Создание конкретных прототипов. Реализация шаблона прототипа часто включает в себя создание конкретных
   классов-прототипов и настройку их методов clone. Это может привести к появлению дополнительных классов и лишней сложности.
4. Ограниченная применимость: шаблон Прототип наиболее подходит, когда стоимость создания объектов с нуля высока. В тех
   случаях, когда создание объекта является относительно простым и недорогим, использование шаблона может привести к
   ненужной сложности.
5. Совместимость с сериализацией. Если вам нужно клонировать сериализуемые объекты, вы можете столкнуться с проблемами,
   связанными с сериализацией и десериализацией объектов.

**Как здесь применены принципы SOLID?**
1. S (Single Responsibility) - Интерфейс прототипа отвечает только за клонирование объектов.
2. O (Open/Closed) - При необходимости все изменения при клонировании можно добавить
   в реализацию метода clone в дочерних класах.
3. L (Liskov Substitution) - Все клонируемые объекты реализуют единый интерфейс и должны реализовывать все его методы.
   В противном случае следует использовать другой интерфейс прототипа.
4. I (Interface Segregation) - Интерфейс прототипа можно ограничить единственным методом clone (т.к. вся логика заключена в нем).
5. D (Dependency Inversion) - В паттерне Prototype мы программируем на уровне интерфейсов.

[к оглавлению](#patterns)

### 5. Одиночка (Singleton)
Одиночка (Singleton) — это порождающий паттерн, который гарантирует, что у класса есть только один экземпляр, и предоставляет глобальную точку доступа к этому экземпляру.

Когда использовать?
- Для управления ресурсами (например, логирование, кэширование, конфигурационные файлы).
- Когда нужно создать объект только один раз и переиспользовать его в разных частях приложения.

__Пример без Singleton (Как не надо)__. В этом примере создается несколько объектов конфигурации, что приводит к ненужному расходу памяти и потенциальным проблемам с синхронизацией.

```java
class Configuration {
    private String configData;

    public Configuration() {
        configData = "Настройки приложения";
    }

    public String getConfigData() {
        return configData;
    }
}

public class Main {
    public static void main(String[] args) {
        Configuration config1 = new Configuration();
        Configuration config2 = new Configuration();

        System.out.println(config1.getConfigData());
        System.out.println(config2.getConfigData());

        // config1 и config2 — это два разных объекта!
        System.out.println(config1 == config2); // false
    }
}
```

Что тут не так?
- Нарушение принципа экономии ресурсов – создаются дубликаты объекта, хотя настройки могут быть едиными для всего приложения.
- Проблемы с согласованностью данных – если один объект изменит настройки, другие объекты этого не увидят.
- Сложность в управлении – трудно гарантировать, что в программе существует только один экземпляр.

__Пример с правильным использованием паттерна Singleton__.
Используем паттерн Singleton для того, чтобы обеспечить один экземпляр объекта.

```java
// 1. Класс Singleton
class Configuration {
    // Приватное статическое поле для единственного экземпляра
    private static Configuration instance;

    private String configData;

    // 2. Приватный конструктор запрещает создание объекта извне
    private Configuration() {
        configData = "Настройки приложения";
    }

    // 3. Метод для получения единственного экземпляра
    public static Configuration getInstance() {
        if (instance == null) {
            instance = new Configuration();
        }
        return instance;
    }

    public String getConfigData() {
        return configData;
    }
}

// 4. Клиентский код
public class Main {
    public static void main(String[] args) {
        Configuration config1 = Configuration.getInstance();
        Configuration config2 = Configuration.getInstance();

        System.out.println(config1.getConfigData());
        System.out.println(config2.getConfigData());

        // config1 и config2 теперь ссылаются на один и тот же объект!
        System.out.println(config1 == config2); // true
    }
}
```

__Улучшенная версия Singleton (потокобезопасная)__.
В многопоточной среде лучше использовать Lazy Initialization с двойной проверкой:

```java
class Configuration {
private static volatile Configuration instance;
private String configData;

    private Configuration() {
        configData = "Настройки приложения";
    }

    public static Configuration getInstance() {
        if (instance == null) { // Первая проверка
            synchronized (Configuration.class) {
                if (instance == null) { // Вторая проверка
                    instance = new Configuration();
                }
            }
        }
        return instance;
    }

    public String getConfigData() {
        return configData;
    }
}
```

__Как здесь применены принципы SOLID?__
1. S (Single Responsibility Principle, Принцип единственной ответственности). Класс Configuration отвечает только за управление единственным экземпляром настроек.
2. O (Open-Closed Principle, Принцип открытости-закрытости). Добавлять новые поля в Configuration можно без изменения клиентского кода.
3. L (Liskov Substitution Principle, Принцип подстановки Барбары Лисков). Этот принцип не особо применим в Singleton, так как не предполагается наследование от этого класса.
4. I (Interface Segregation Principle, Принцип разделения интерфейсов). Класс Configuration предоставляет только нужные методы без перегрузки интерфейса.
5. D (Dependency Inversion Principle, Принцип инверсии зависимостей). Если в коде использовать Configuration через интерфейс, то зависимости можно инвертировать, но Singleton обычно сам по себе не предполагает работу через интерфейсы.

[к оглавлению](#patterns)

---

## Структурные (Structural) (6-12)
Определяют, как классы и объекты могут быть объединены.
Шаблон подобен рецепту объединения различных объектов и классов для создания более крупной структуры. Это немного похоже на следование чертежу при строительстве дома. Эти шаблоны учат нас объединять уникальные части системы таким образом, чтобы их было легко изменять и расширять, не затрагивая всю систему.

### 6. Адаптер (Adapter)
Паттерн программирования "Адаптер" (Adapter) — это структурный шаблон проектирования, который позволяет объектам с
несовместимыми интерфейсами работать вместе. Он выступает в качестве прослойки между двумя объектами, преобразуя вызовы
одного объекта в вызовы, понятные другому.

```java
public interface Animal {
   void makeSound();
}

public class Dog implements Animal {
   @Override
   public void makeSound() {
      System.out.println("Гав-гав!");
   }
}

public interface Flyable {
   void fly();
   void chirp();
}

public class Bird implements Flyable {
   @Override
   public void fly() {
      System.out.println("Лечу!");
   }

   @Override
   public void chirp() {
      System.out.println("Чирик!");
   }
}


public class Main {
   public static void main(String[] args) {
   Animal dog = new Dog();
   Flyable bird = new Bird();


   Animal adaptedBird = new BirdToAnimalAdapter(bird);
   dog.makeSound(); 
   adaptedBird.makeSound();
   }
}
```
[к оглавлению](#patterns)

---

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
Наблюдатель — это поведенческий паттерн проектирования, который создает механизм подписки, позволяющий одним объектам
отслеживать изменения состояния другого объекта и автоматически реагировать на них.

Основные компоненты:
- **Субъект (Subject)**: Объект, за которым наблюдают. Управляет списком наблюдателей и уведомляет их об изменениях.
- **Наблюдатель (Observer)**: Интерфейс, определяющий метод update(), который вызывается при изменении состояния субъекта.

***Пример кода без паттерна Observer(Как не следует делать)***

Описан код, где элемент (логгер Logger) должен обновляться при изменении данных в объекте класса Data.
```java
class Data {
    private int value;
    private Logger logger;

    public Data(Logger logger) {
        this.logger = logger;
    }

    public void setValue(int value) {
        this.value = value;
        logger.log("New value: " + value);  // При изменении значения вручную обновляем все зависимые компоненты
    }
}

class Logger {
    public void log(String message) {
        System.out.println("[LOG] " + message);
    }
}

public class Main {
    public static void main(String[] args) {
        Logger logger = new Logger();
        Data data = new Data(logger);

        data.setValue(10); 
        // Вывод:
        // [LOG] New value: 10
    }
}
```
Минусы:
- **Жесткая связь**: Класс Data напрямую зависит от конкретного класса Logger.
- **Нарушение Open/Closed(SOLID)**: Добавление нового компонента(ещё одного логгера) требует изменения кода Data.
- **Сложность масштабирования**: Каждое новое изменение влечет правки в классе Data.

***Пример кода c паттерном Observer(Как следует делать)***

Решить вышеописанную проблему можно с помощью написания отдельных интерфейсов Observer и Subject:
```java
interface Observer {
    void update(int value);
}
interface Subject {
   void addObserver(Observer observer);
   void removeObserver(Observer observer);
   void notifyObservers();
   
}
// Субъект (наблюдаемый объект)
class Data implements Subject{
    private int value;
    private List<Observer> observers = new ArrayList<>(); // Список всех наблюдателей

    // Методы для управления подписчиками
    @Override
    public void addObserver(Observer observer) {
        observers.add(observer);
    }
   @Override
    public void removeObserver(Observer observer) {
        observers.remove(observer);
    }

    // Уведомление всех наблюдателей
    @Override
    private void notifyObservers() {
        for (Observer observer : observers) {
            observer.update(value);
        }
    }

    public void setValue(int value) {
        this.value = value;
        notifyObservers(); // Автоматическое уведомление
    }
}

class Logger implements Observer {
    @Override
    public void update(int value) {
        System.out.println("[LOG] New value: " + value);
    }
}

public class Main {
    public static void main(String[] args) {
        Data data = new Data();
        Logger logger = new Logger();
        data.addObserver(logger);   // Подписка на изменения
        data.setValue(10);
        // Вывод:
        // [LOG] New value: 10
        Logger logger2 = new Loger();
        data.removeObserver(logger); // Удаление ненужного наблюдателя
        data.addObserver(logger2); // Добавление нового наблюдателя без изменения кода Data
    }
}
```
Преимущества:
- **Слабая связь**: Субъект не зависит от конкретных классов наблюдателей.
- **Гибкость:** Новые наблюдатели добавляются без изменения кода субъекта.

Применение SOLID в паттерне Observer
1. **Single Responsibility Principle (SRP)**:Субъект отвечает только за управление наблюдателями и уведомление.
   Наблюдатели отвечают только за реакцию на изменения.
2. **Open/Closed Principle (OCP)** Добавление нового наблюдателя не требует изменений в классе Data.
3. **Liskov Substitution Principle (LSP)** Все наблюдатели реализуют интерфейс Observer и не сужают его исходное поведение.
4. **Interface Segregation Principle (ISP)** Все методы интерфейсов Observer и Subject реализованы.
5. **Dependency Inversion Principle (DIP)** Субъект зависит от абстракции Observer, а не от конкретных реализаций.


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
### 1. Назовите основные принципы ООП. Расскажите подробно о каждом.

**Инкапсуляция**
Инкапсуляция в программировании является объединением данных и кода, работающего с этими данными,
в большинстве случае это сводится к тому, чтобы не давать доступа к важным данным напрямую.
Вместо этого мы создаем ограниченный набор методов, с помощью которых можно работать с нашими данными.
Очевидные примеры инкапсуляции, - это модификаторы доступа (private, public и т.д.),
то есть реализация такой логики что внутри объекта или класса хранятся все данные этого объекта
или класса с разным уровнем доступа. Таким образом, разработчик не может их редактировать при помощи других классов.
Окружающие элементы могут лишь запрашивать «публичные» методы и атрибуты через геттеры - и изменять их через сеттеры.

**Наследование**
Наследование является одним из важнейших принципов объектно-ориентированного программирования,
поскольку оно позволяет создавать иерархические структуры объектов.
Используя наследование, можно создать общий класс, который будет определять характеристики и поведение,
свойственные какому-то набору связанных объектов. В дальнейшем этот класс может быть унаследован другими,
более частными классами, каждый из которых будет добавлять уникальные, свойственные только ему характеристики
и дополнять или изменять поведение базового класса. В терминах Java которые можно услышать или встретить
такой общий класс называется _суперклассом (superclass)_, или _базовым классом (base class)_,
или _классом-родителем (parent class)_, а класс, его расширяющий наследником, - _подклассом (subclass)_,
или _дочерним классом (child class)_, или _классом-потомком (derived class)_.

**Полиморфизм**
Это один из принципов ООП, позволяющий вызовом переопределённого метода через переменную класса-родителя
получить поведение, которое будет соответствовать реальному классу-потомку, на который ссылается эта переменная.
Возьмем для примера абстрактный класс _«Автомобиль»_, который наследуют два конкретных класса
– _«Спортивный автомобиль»_ и _«Грузовой автомобиль»_. И спортивные, и грузовые автомобили будут обладать общими
характеристиками и будут иметь возможность выполнять общие для всех автомобилей действия, которые указаны в
абстрактном классе -родителе, но конкретная реализация этих действий может быть разной.
Например, общее для всех автомобилей действие «завестись» у спортивного автомобиля может быть реализовано
путем нажатия кнопки, а у грузового - с помощью ключа. Один результат – разные решения. В этом и состоит полиморфизм.

**Абстракция**
Отделение частного от общего, это прием исследования, позволяющий отвлечься от некоторых несущественных
в определенном отношении свойств изучаемых явлений и выделить свойства существенные и определяющие.
Фокусировка разработчика на конкретных свойствах объекта зависит от тех задач, которые призван решать объект.
Следствием такого подхода является то, что, если в императивных языках разработчику необходимо думать в терминах
компьютерной логики, в объектно-ориентированных языках разработчик думает в терминах проблемной области,
в которой он разрабатывает приложения.

### 2.Расскажите про иерархию наследования. Подробно про методы класса object.
Все классы неявно наследуются от типа Object. Все методы которые есть у Object, есть вообще у всех классов.
Т.е. разработчики Java отобрали несколько методов, которые, по их мнению, должны быть у всех классов
и добавили их в класс Object:
**toString()** - Возвращает строковое представление объекта.
**hashCode()**
**equals(Object obj)** - Пара методов, которые используются для сравнения объектов.
**getClass()** - 	Возвращает специальный объект, который описывает текущий класс
**notify()**
**notifyAll()**
**wait()**  Методы для контроля доступа к объекту из различных потоков. Управление синхронизацией потоков. Многопоточность.
**finalize()** - Методы для контроля доступа к объекту из различных нитей. Управление синхронизацией нитей.
**clone()** - Метод позволяет клонировать объект: создает дубликат объекта.

### 3.Что такое интерфейс, что такое абстрактный класс +
### 4.Может ли интерфейс \ абстрактный класс иметь конструктор, поля, статические статические \ дефолтные методы.
**Интерфейс** — это контракт, который должен быть реализован конкретным классом. У интерфейса _не может быть состояния_,
поэтому в нем нельзя использовать изменяемые поля экземпляра. В интерфейсе могут быть только неизменяемые final-поля
(они таковые неявно). Методы интерфейса неявно абстрактны и обязаны быть реализованы в классе,
реализующем этот интерфейс.

**Абстрактный класс** -  похож на обычный, но отличается тем, что может содержать абстрактные
методы — методы без реализации, и нельзя создать экземпляр абстрактного класса. Абстрактные методы в абстрактных
классах должны быть явно объявлены как _абстрактные_ (слово abstract). Рекомендуется использовать абстрактный класс,
когда вам нужно изменяемое состояние. У него _может быть конструктор_ (у интерфейса нет).

С точки зрения объектно-ориентированного программирования основное различие между интерфейсом и абстрактным классом
заключается в том, что интерфейс _не может иметь состояния_, тогда как абстрактный класс может(в виде полей экземпляра).
Другое ключевое различие заключается в том, что классы могут реализовывать более одного интерфейса,
но расширять только один абстрактный класс.

Множественное наследование может привести к тупиковым ситуациям в коде,
поэтому авторы Java решили этого избежать, отказавшись от него. В Java 8 у интерфейсов добавили default методы.
В качестве примера default-метода из JDK можно привести метод _forEach()_ из интерфейса Iterable.
Любая реализация Iterable может использовать метод _forEach()_ без необходимости реализации этого нового метода.

### 5.Что такое Enum , в чем отличие от класса, может ли иметь методы ,
### конструкторы , наследоваться реализовывать интерфейсы.
**Enum** — тоже класс. Но он специально «заточен» на решение задачи - создание некоторого ограниченного круга значений.
Этот список значений фиксирован и хорошо известен, что делает код более предсказуемым и понятным.
Использование Enum помогает избежать ошибок, связанных с применением недопустимых значений, и способствует созданию
более надежного и эффективного кода. Enum  можно рассматривать как особый вид класса Java.

Enum может:
- Реализовывать интерфейсы;
- Неявно реализует интерфейсы _Serializable_ и _Comparable_;
- В неявном виде класс реализует интерфейс java.lang.Enum и не может быть расширен от другого класса;
- Для сравнения значений Enum можно использовать операторы == и _equals()_.

Перечисления (enum) в Java представляют собой набор констант, которые обычно используются для определения некоторого
ограниченного набора значений. В Java enum-классы имеют свои собственные конструкторы,
которые объявляются с модификатором доступа private. Когда все конструкторы перечисления объявлены как private,
это означает, что их можно вызывать только из самого перечисления, но не извне.

Таким образом, применение оператора new для создания новых экземпляров перечислений невозможно. вы можете определить
несколько конструкторов для изменения значений каждого элемента перечисления.

### 6. Расскажите про модификаторы доступа, к чему они применяются.
Модификаторы — это специальные слова языка Java, которые вы можете использовать для изменения элементов (классов, методов, переменных). В Java есть две категории модификаторов: модификаторы доступа и другие модификаторы.
Модификаторы доступа определяют область видимости и доступность классов, методов, полей и конструкторов. В Java есть четыре уровня доступа:
* public - открытый элемент. Доступ к нему можно получить из класса, снаружи класса, внутри и снаружи пакета, в пределах одного проекта (Java файл может иметь только один public класс и множество подклассов). Используется, если класс или его члены должны быть доступны в любой точке программы;

        public class Example {
            public int value;
        
            public void show() {
                System.out.println("Public method");
            }
        }

* private — доступ только внутри того же класса. Применяется для инкапсуляции данных, чтобы ограничить прямой доступ к полям и методам;

        class Example {
          private int value; // доступен только внутри Example
        
          private void show() {
              System.out.println("Private method");
          }
        }
* default — элементу с модификатором по умолчанию, есть доступ только внутри пакета. Устанавливается ко всем полям и методам, в которых не подставлены другие модификаторы. Применяется, когда нет необходимости предоставлять доступ извне пакета;

        class Example {
           int value; // доступен внутри пакета
        }
* protected — можно получить доступ внутри и снаружи пакета через дочерний класс и только в классе наследника (дочерний). Применяется в основном только к методам и довольно редко, нужно основание. Чаще всего используется для наследования;
  
        class Parent {
          protected void show() {
              System.out.println("Protected method");
          }
        }
        
        class Child extends Parent {
          void display() {
              show(); // доступно через наследование
          }
        }
Для чего же следует использовать модификаторы доступа? При разработке ООП-кода классы проектируются с целью моделирования сущностей предметной области. Описывая класс разработчик выделяет внешнюю и внутреннюю реализации типа. Модификаторы доступа позволяют при проектировании класса указать что есть интерфейс (внешняя реализация) и открыть ее для использования, а что есть внутренняя реализация.

Применение модификаторов:
- Классы могут быть только public или default (вложенные классы могут быть private или protected).
- Поля, методы и конструкторы могут иметь любой модификатор.
- Лучшая практика – ограничивать доступ по принципу “минимально необходимый уровень”, чаще всего используя private и protected для инкапсуляции.


### 7. Расскажите про конструкторы, с какими модификаторами они применяются, могут ли они наследоваться \ переопреляться ?
Конструктор – это специальный метод, имя конструктора совпадает с именем класса, конструктор не имеет возвращаемого значения. Он инициализирует поля и устанавливает начальное состояние объекта. Конструкторов в классе может быть сколько угодно, различаться они должны количеством и/или типом параметров (это называется перегрузка конструкторов). Вызываться конструктор может только при создании объекта после оператора new.
“Зачем нужен конструктор?”, можно сказать: для того, чтобы объекты всегда находились в правильном состоянии. Когда ты используешь конструкторы, все твои переменные будут корректно проинициализированы, и в программе не будет машин со скоростью 0 и прочих “неправильных” объектов.

    class Example {
        private Example() {
        System.out.println("Private constructor");
    }

    public static Example getInstance() {
        return new Example(); // можно создавать объект внутри класса
        }
    }
Если ты будешь инициализировать поля самостоятельно, велик риск что-нибудь пропустить и ошибиться. А с конструктором такого не будет: если ты передал в него не все требуемые аргументы или перепутал их типы, компилятор сразу же выдаст ошибку.
Отдельно стоит сказать о том, что внутрь конструктора не стоит помещать логику твоей программы. Для этого в твоем распоряжении есть методы, в которых ты можешь описать весь

Рассмотрим все особенности конструктора.
- Конструктор – это метод, имя которого совпадает с именем класса.
- Конструктор не имеет типа возвращаемого значения.
- При объявлении конструктора можно использовать любой их четырех модификаторов доступа.
- Количество конструкторов в классе не ограничено так как конструкторы можно перегружать (т.е. создавать конструкторы с различным количеством и/или типом параметров).
- С помощью ключевого слова this([параметры]) можно вызвать один конструктор из конструктора как обыкновенный метод. Этот оператор используется только в первой строке конструктора (до него в теле конструктора могут быть только комментарии).
- Конструкторы применяются для начальной инициализации полей создаваемого объекта. Реализовывать какую-либо логику в коде конструктора считается плохи стилем программирвоания.
- Конструкторы не наследуются.
- Не бывает классов без конструкторов. Если в классе явно не определить ни одного конструктора, тогда компилятор добавляет конструктор по умолчанию – это конструктор без параметров, с пустым телом, и с таким же атрибутом доступа, как и у класса.
- Если же в классе определить хоть один конструктор, то конструктор по умолчанию добавлен не будет. При необходимости же создавать объекты, не передавая в конструктор параметры, подходящий конструктор придется также определить явно.
- Какие именно конструкторы нужно определить в классе и сколько их должно быть определяет разработчик (правила языка программирования этого определить не могут). Необходимо проанализировать предметную область и определить все возможные варианты создания объекта, которые могут понадобиться в дальнейшем
- static конструкторов в java нет;
- Используется для синглтонов (Singleton) или статических фабрик (Factory Method).

Краткий ответ на собеседовании:
Конструктор – это специальный метод, вызываемый при создании объекта. Он не наследуется и не переопределяется, потому что конструкторы не являются обычными методами и не участвуют в полиморфизме, но может быть вызван через super(). Конструкторы могут быть public, protected, default и private. Также в Java возможна перегрузка конструкторов (overloading).

### 8. Можно ли в классе заимплементить 2 интерфейса? А если в них один и тот же метод doSmth? Как он реализуется?
Да, в Java класс может реализовывать несколько интерфейсов с помощью ключевого слова implements.

    interface A {
        void doSmth();
    }
    
    interface B {
        void doSmth();
    }
    
    class MyClass implements A, B {
        @Override
        public void doSmth() {
            System.out.println("Implemented doSmth()");
        }
    }
Ответ: Код компилируется без ошибок, и метод doSmth() должен быть реализован один раз в MyClass, так как интерфейсы не содержат реализацию методов.

А если в интерфейсах есть default-методы?
Если оба интерфейса имеют default-метод с одинаковой сигнатурой, то при компиляции возникнет конфликт. Java не знает, какой именно метод использовать, и потребует явного разрешения конфликта.

    interface A {
        default void doSmth() {
            System.out.println("A's default doSmth");
        }
    }
    interface B {
        default void doSmth() {
            System.out.println("B's default doSmth");
        }
    }
    class MyClass implements A, B {
        @Override
        public void doSmth() {
            // Разрешаем конфликт явно
            B.super.doSmth(); // Или A.super.doSmth();
        }
    }
Ответ: Если в интерфейсах A и B есть default-методы с одинаковой сигнатурой, то класс обязан переопределить метод и явно указать, чей метод он использует (A.super.doSmth(); или B.super.doSmth();).

Краткий ответ на собеседовании:
Да, класс может реализовывать несколько интерфейсов. Если в интерфейсах объявлен один и тот же метод без реализации, он просто реализуется один раз в классе. Если же в интерфейсах есть default-методы с одинаковыми сигнатурами, Java требует явного разрешения конфликта через A.super.methodName() или B.super.methodName().

### 9. Статический\динамический полиморфизм.
1. **Статический полиморфизм** также называется перегрузкой методов (method overloading). Он происходит на этапе компиляции (compile-time), поэтому его называют "статическим".
   Особенности:
    * Методы с одинаковым именем, но разными параметрами (типами, количеством или порядком).
    * Какой метод будет вызван, определяется на этапе компиляции на основе сигнатуры метода (имени и параметров).
```java
class Calculator {
    // Перегрузка метода add
    public int add(int a, int b) {
        return a + b;
    }

    public double add(double a, double b) {
        return a + b;
    }

    public int add(int a, int b, int c) {
        return a + b + c;
    }
}

public class Main {
    public static void main(String[] args) {
        Calculator calc = new Calculator();
        System.out.println(calc.add(2, 3));           // Вызов add(int, int)
        System.out.println(calc.add(2.5, 3.5));       // Вызов add(double, double)
        System.out.println(calc.add(2, 3, 4));        // Вызов add(int, int, int)
    }
}
```

2. **Динамический полиморфизм** также называется переопределением методов (method overriding). Он происходит во время выполнения программы (runtime), поэтому его называют "динамическим".
   Особенности:
    * Метод в подклассе переопределяет метод суперкласса.
    * Какой метод будет вызван, определяется на этапе выполнения программы на основе типа объекта, а не типа ссылки.
```java
class Animal {
    public void sound() {
        System.out.println("Animal makes a sound");
    }
}

class Dog extends Animal {
    @Override
    public void sound() {
        System.out.println("Dog barks");
    }
}

class Cat extends Animal {
    @Override
    public void sound() {
        System.out.println("Cat meows");
    }
}

public class Main {
    public static void main(String[] args) {
        Animal myAnimal = new Animal();  // Создание объекта Animal
        Animal myDog = new Dog();        // Создание объекта Dog, но ссылка типа Animal
        Animal myCat = new Cat();        // Создание объекта Cat, но ссылка типа Animal

        myAnimal.sound();  // Вызов метода sound() из класса Animal
        myDog.sound();     // Вызов метода sound() из класса Dog (динамический полиморфизм)
        myCat.sound();     // Вызов метода sound() из класса Cat (динамический полиморфизм)
    }
}
```
### 10. Что является членами класса.

**Члены класса** в Java — это элементы, объявленные внутри тела класса. Они определяют структуру, состояние и поведение объектов или самого класса. К ним относятся:

**1. Поля (Fields)**
- Переменные экземпляра: Хранят состояние объекта (например, `private int age;`).
- Статические переменные: Общие для всех экземпляров класса (например, `public static int count;`).
- Константы: Объявляются с модификаторами `static final` (например, `public static final String NAME = "Test";`).

**2. Методы (Methods)**
- Методы экземпляра: Определяют поведение объекта (например, `public void calculate() { ... }`).
- Статические методы: Принадлежат классу, а не объекту (например, `public static void log(String message) { ... }`).

**3. Конструкторы (Constructors)**
- Используются для инициализации объектов.
- Имя совпадает с именем класса, нет возвращаемого типа (например, `public MyClass() { ... }`).

**4. Вложенные классы и интерфейсы**
- Вложенные классы:
    - Обычные (не статические) — `class Outer { class Inner { ... } }`.
    - Статические — `class Outer { static class Nested { ... } }`.
- Локальные классы: Объявляются внутри методов.
- Aнонимные классы: Объявляются и используются в одном выражении.

**5. Блоки инициализации**
- Блоки экземпляра: Выполняются при создании объекта (например, `{ System.out.println("Init"); }`).
- Статические блоки: Выполняются при загрузке класса (например, `static { System.out.println("Static init"); }`).

**6. Перечисления (Enums)**
- Объявляются внутри класса (например, `enum Status { ACTIVE, INACTIVE }`).

**7. Аннотации (Annotations)**
- Применяются к элементам класса (например, `@Override`, `@Deprecated`).

**8. Модификаторы доступа**
- Контролируют видимость элементов:
    - `public`, `private`, `protected`, а также *упрощённый модификатор* (отсутствие ключевого слова).

---

**Не являются членами класса**:
- Локальные переменные (объявлены внутри методов).
- Параметры методов.
- Элементы анонимных классов.

Пример:
```java
public class Example {
    // Поля
    private int instanceVar;
    public static final String CONSTANT = "Value";

    // Конструктор
    public Example() {
        instanceVar = 10;
    }

    // Метод экземпляра
    public void display() {
        System.out.println("Instance method");
    }

    // Статический метод
    public static void staticMethod() {
        System.out.println("Static method");
    }

    // Вложенный класс
    public class NestedClass { }

    // Статический инициализатор
    static {
        System.out.println("Static initializer");
    }

    // Инициализатор экземпляра
    {
        System.out.println("Instance initializer");
    }
}
```

### 11. Расскажите подробно как переопределяются\ перегружаются методы классов наследников.
В Java **переопределение** (overriding) и **перегрузка** (overloading) методов — это два разных механизма, которые позволяют управлять поведением методов в классах-наследниках.

**1. Переопределение методов (Overriding).**
Переопределение позволяет подклассу предоставить свою реализацию метода, уже объявленного в родительском классе. Это ключевой аспект полиморфизма.
**Переопределение** используется для изменения реализации унаследованного метода.

**Правила переопределения:**
- **Сигнатура метода** (имя и параметры) должна **полностью совпадать** с методом в родительском классе.
- **Возвращаемый тип** должен быть совместимым.
- **Модификатор доступа** не может быть более строгим, чем в родительском классе (например, если метод в родителе `protected`, в потомке можно сделать его `public`, но не `private`).
- Методы, помеченные как `final` или `static`, **не могут быть переопределены**.
- Аннотация `@Override` используется для явного указания, что метод переопределяет родительский.
```java
class Animal {
    public void makeSound() {
        System.out.println("Animal sound");
    }
}

class Dog extends Animal {
    @Override
    public void makeSound() { // Переопределение
        System.out.println("Bark!");
    }
}
```

**2. Перегрузка методов (Overloading).**
Перегрузка позволяет иметь в одном классе несколько методов с **одинаковым именем**, но **разными параметрами** (по количеству, типу или порядку). Возвращаемый тип не влияет на перегрузку.
**Перегрузка** позволяет создавать методы с одинаковым именем, но разными параметрами.

**Правила перегрузки:**
- **Сигнатура метода** (имя + параметры) должна **отличаться**.
- **Возвращаемый тип** может быть любым.
- **Модификаторы доступа** и объявленные исключения не влияют на перегрузку.
```java
class Calculator {
    int add(int a, int b) {
        return a + b;
    }

    double add(double a, double b) { // Перегрузка по типу параметров
        return a + b;
    }

    int add(int a, int b, int c) { // Перегрузка по количеству параметров
        return a + b + c;
    }
}
```

**3. Важные нюансы:**
- **Конструкторы** можно перегружать, но нельзя переопределять.
- **Статические методы** не переопределяются (они скрываются в подклассе).
- **Абстрактные методы** должны быть переопределены в неабстрактном подклассе.

### 12. Jvm, Jre, Jdk.
**JVM (Java Virtual Machine) — виртуальная машина Java**, которая исполняет Java-программы. Она берет байт-код (.class файлы, которые получаются после компиляции Java-кода) и выполняет его на конкретной операционной системе. JVM — это платформо-независимый компонент, но у каждой операционной системы своя реализация JVM.  

**JRE (Java Runtime Environment) — среда выполнения Java**, это комплект, необходимый для запуска Java-приложений. В него входит:
- JVM (виртуальная машина)
- Стандартные библиотеки Java (например, java.lang, java.util)
- Различные конфигурационные файлы

**JDK (Java Development Kit) — набор разработчика Java**. В него входит:
- JRE (а значит, и JVM)
- Компилятор javac
- Отладчики, инструменты профилирования
- Библиотеки и документация для разработки

### 13. Расскажите что такое classpath java, общее правило именования пакетов java.
**CLASSPATH** – это путь, по которому Java ищет классы и пакеты во время выполнения программы.
используется:
- при компиляции (javac) – чтобы найти зависимости
- при запуске (java) – чтобы загрузить классы
- в IDE для управления зависимостями

**Пакеты (packages)** в Java нужны для организации кода и предотвращения конфликтов имен.

Структура именования пакетов обычно имеет такой вид:  
**доменное имя компании в обратном порядке** + **название проекта/модуля**  
Примеры:
- com.example.project → Компания example.com, проект project.
- org.apache.commons → Организация Apache, библиотека Commons.

Основные правила именования пакетов:
1. Используйте только строчные буквы (com.example.app).
2. Не начинайте с цифры и специальных символов.
3. Не используйте зарезервированные слова Java (int, class, package).
4. Название пакета должно отражать его содержимое.


### 14. Расскажите про интерфейсы Comparator, Comparable и их применение.
В Java интерфейсы Comparable и Comparator используются для сортировки объектов. Они помогают определить, как сравнивать экземпляры класса, чтобы можно было, например, отсортировать список.  

**Comparable – встроенный порядок сортировки**  
Интерфейс Comparable используется, когда у объекта есть естественный порядок (например, числа – по возрастанию, строки – в алфавитном порядке).  
`int compareTo(T o);`

Возвращает:
- 0, если объекты равны
- Отрицательное число, если текущий объект меньше переданного
- Положительное число, если текущий объект больше переданного

```java
class Person implements Comparable<Person> {
    String name;
    int age;

    public Person(String name, int age) {
        this.name = name;
        this.age = age;
    }

    @Override
    public int compareTo(Person other) {
        return Integer.compare(this.age, other.age); // Сортировка по возрасту
    }
}
public class Main {
    public static void main(String[] args) {
        List<Person> people = new ArrayList<>();
        people.add(new Person("Alice", 30));
        people.add(new Person("Bob", 25));
        people.add(new Person("Charlie", 35));

        Collections.sort(people); // Использует compareTo()
    }
}
```
Если нужно сортировать по разным критериям (например, по имени), придется менять compareTo(), что не всегда удобно.  

**Comparator** – для разных вариантов сортировки  
Если объект можно сортировать по разным критериям, то лучше использовать Comparator.  
`int compare(T o1, T o2);`  
Возвращает аналогично compareTo()  
```java
class NameComparator implements Comparator<Person> {
    @Override
    public int compare(Person p1, Person p2) {
        return p1.name.compareTo(p2.name);
    }
}

public class Main {
    public static void main(String[] args) {
        List<Person> people = Arrays.asList(
            new Person("Alice", 30),
            new Person("Bob", 25),
            new Person("Charlie", 35)
        );

        Collections.sort(people, new NameComparator()); // Сортировка по имени
        System.out.println(people); // [Alice (30), Bob (25), Charlie (35)]
    }
}
```
Можно легко добавлять новые критерии сортировки без изменения класса Person.

### 15. Расскажите про класс String, пул строк.
Для работы со строками в Java определен класс String. Для сложения двух строк можно воспользоваться оператором +.
Преобразование объектов других классов к строковому представлению выполняется через неявный вызов метода `toString()` у объекта.

Имеется возможность перевод числа в строке в числовой тип. Для перевода необходимо использовать соответствующий класс-обёртку.
Все эти методы начинаются со слова parse:
```java
Integer i = Integer.parseInt("4"); 
Double d = Double.parseDouble("23.34D");
```
Основные особенности класса:
1. Неизменяемость (Immutable) - После создания строку нельзя изменить. Любые операции (например, `concat()`, `replace()`)
   возвращают новый объект строки.
2. Для сравнения содержимого строк используется `equals()`, а не "=="
3. Создание строк может быть выполнено несколькими способами:
    1. Через конструктор - Объект создается в heap'е: `String str1 = new String("Hello")`
    2. Через литерал - Объект создаётся в String Pool'е: `String str2 = "Hello"`

**String Pool** - специальная область в heap'е, где хранятся уникальные строковые литералы с целью
экономия памяти за счет повторного использования одинаковых строк.
При создании строки через литерал (`String str2 = "Hello"`), JVM проверяет наличие такой строки в пуле.
- Если есть — возвращает ссылку на существующий объект.
- Если нет — создает новый объект в пуле.

Строки, созданные через new String(), не попадают в пул автоматически, но благодаря методу `intern()` можно вручную
добавить данную строку в пул.

### 16. Расскажите про варианты использования зарезервированных слов таких как super, this, class, instance of.
1. super - ссылается на родительский класс (суперкласс). Используется для вызова конструктора родительского класса, методов, полей:
```java
public class Animal {
    public Animal(String name) {
        System.out.println("Animal: " + name);
    }
    public makeSound(){}
}

public class Dog extends Animal {
    public Dog() {
        super("Toto"); // Вызов конструктора Animal
        super.makesound(); //Вызов метода родительского класса
    }
}
```
2. this - ссылка на текущий экземпляр объекта. Используется для разрешения конфликта между полями класса и метода,
   вызова конструкта, передачи объекта в методе. Примеры использования:
```java
public class Person {
    private String name;

    public Person(String name) { 
        this.name = name; // this указывает на поле класса
    }
    public Person(){
        this("John"); // Вызов конструктора с параметром
    }
    public void show(){
        System.out.println(this); // Вызов toString() текущего объекта
    }
}
```
3. class - предоставляет метаданные о классе. Часто используется в рефлексии.
```java
if (listEx.getClass() == ArrayList.class) { // Проверка на принадлежность объекта listEx к классу ArrayList
        System.out.println("Это ArrayList");
}
```
4. instance of - проверяет, является ли объект экземпляром указанного класса или интерфейса. Часто используется при работе
   с полиморфизмом.
```java
Object obj = "Hello";
if (obj instanceof String) { // Проверка obj на принадлежность к классу String
    //Блок кода
}
```
### 17. java массивы, к какому типу относится, какие есть особенности можно ли создать 0 длинны, могут ли расширяться.
Массив в Java - это структура данных, в которой хранятся элементы одного типа. Его можно представить, как набор
пронумерованных ячеек, в каждую из которых можно поместить какие-то данные (один элемент данных в одну ячейку).
Доступ к конкретной ячейке осуществляется через её индекс. Элементы нумеруются с нуля. Массивы в Java являются объектами,
даже если хранят примитивные типы. Java поддерживает создание многомерных(2,3 и т.д) массивов.
Пример объявления массива, в котором может храниться 10 целых чисел:

`int[] myArray = new int[10];`

Также можно объявлять массивы с уже занесёнными значениями:

`int[] myArray2 = {1, 2, 3, 4, 5}`

Двумерный массив выглядит следующим образом:

`int[][] myArray3 = new int [3][3];`

Имеется встроенная поддержка сортировки и поиска содержимого массива: ` Arrays.sort()` и `Arrays.binarySearch()` соответственно

Особенности:
- **Быстрый доступ к данным**: элементы доступны за O(1) благодаря использованию индексов через array[index].
- **В Java можно создать массив нулевой длины**:
```java
int[] emptyIntArray = new int[0];
String[] emptyStringsArray = {}; // При возврате значения будет показан пустой результат вместо null
```
- **Размер массива фиксирован после создания**. Для решения данной проблемы можно воспользоваться
  ArrayList из Java Collections, который имеет возможность динамически расширяться.
  
### 18. Назовите этапы создания \запуска блоков\конструкторов класса при наследовании.

Создание и запуск блоков и конструкторов класса при наследовании включает несколько этапов, которые обеспечивают корректную инициализацию объектов. Вот основные этапы:

* Инициализация супер-класса:

При создании экземпляра подкласса сначала вызывается конструктор супер-класса. Это обеспечивается автоматическим вызовом конструктора супер-класса, который производится с помощью super(). Если в подклассе не указано явно какое-либо другое значение для вызова конструктора супер-класса, будет вызван конструктор по умолчанию.

* Выбор конструктора:

Конструктор супер-класса выбирается на основе переданных параметров в super() в конструкторах подкласса. Если в супер-классе есть несколько конструкторов (перегрузка), Java выбирает соответствующий в зависимости от предоставленных аргументов.

* Инициализация полей супер-класса:

Все поля инициализируются в порядке объявления в классе супер-класса, прежде чем будет выполнен любой код в конструкторе подкласса.

* Выполнение статических блоков:

Если в супер-классе есть статические блоки инициализации, они выполняются перед конструктором, инициализируя любые статические переменные. Это происходит один раз при загрузке класса.

* Инициализация подкласса:

После того как конструктор супер-класса завершил свою работу, управление передается конструктору подкласса. Здесь выполняется код, определенный в его конструкторе.

* Инициализация полей подкласса:

Поля подкласса инициализируются в порядке их объявления. Это происходит после выполнения конструктора супер-класса, но перед выполнением тела конструктора подкласса.

* Выполнение статических блоков подкласса:

Если в подклассе есть статические блоки инициализации, они выполняются также один раз при загрузке подкласса.

* Завершение создания объекта:

После выполнения всех вышеуказанных этапов, объект считается полностью инициализированным и готовым к использованию.

### 19. Расскажите какое будет поведение если внутри цикла вызвать оператор break\continue.

В Java операторы break и continue используются для управления выполнением циклов. Рассмотрим их поведение подробнее.

* Оператор break

Оператор break используется для немедленного выхода из цикла. Когда break вызывается, управление передается на первую строку кода после завершения цикла. Рассмотрим пример:

  for (int i = 0; i < 10; i++) {
    if (i == 5) {
      break; // Прерывает цикл, если i равно 5
    }
    System.out.println(i);
  }

В этом примере, когда i достигает значения 5, оператор break вызывается, и цикл прерывается. В результате в консоль будут выведены числа от 0 до 4.

* Оператор continue

Оператор continue пропускает текущую итерацию цикла и переходит к следующей. В зависимости от типа цикла, управление передается к проверке условия для продолжения выполнения цикла. Пример:

  for (int i = 0; i < 10; i++) {
      if (i == 5) {
        continue; // Пропускает текущую итерацию, если i равно 5
      }
      System.out.println(i);
  }

В этом примере, когда i равно 5, оператор continue вызывается, и текущее значение i не будет выведено. Цикл продолжит свою работу, и в результате будут выведены числа от 0 до 9, за исключением 5.

* Вложенные циклы

Важно знать, что в случае вложенных циклов оператор break и continue будут действовать только на текущий цикл, в котором они находятся.

  for (int i = 0; i < 3; i++) {
    for (int j = 0; j < 3; j++) {
      if (j == 1) {
        break; // Прерывает внутренний цикл
      }
      System.out.println("i: " + i + ", j: " + j);
    }
  }

В этом примере, когда j равно 1, внутренний цикл прерывается, и управление переходит к следующей итерации внешнего цикла. Результат будет:

i: 0, j: 0
i: 1, j: 0
i: 2, j: 0

Если бы мы использовали continue, то внутренний цикл пропустил бы текущую итерацию, и j продолжил бы свою работу, печатая все значения:

  for (int i = 0; i < 3; i++) {
    for (int j = 0; j < 3; j++) {
      if (j == 1) {
        continue; // Пропускает текущую итерацию внутреннего цикла
      }
      System.out.println("i: " + i + ", j: " + j);
    }
  }

В этом случае вывод будет:

i: 0, j: 0
i: 0, j: 2
i: 1, j: 0
i: 1, j: 2
i: 2, j: 0
i: 2, j: 2

### 20. Что такое Generic.

Generics (обобщения) в Java — это мощный механизм, который позволяет создавать классы, интерфейсы и методы, работающие с типами данных, которые будут определены только при их использовании. Это позволяет использовать один и тот же код для разных типов данных, обеспечивая при этом безопасность типов и избавляясь от необходимости использования объектов класса Object.
Вот основные моменты, которые нужно знать о Generics в Java:

1. Основы Generics
   
Объявление обобщенного класса:

  class Box<T> { 
    private T object;

    public void set(T object) {
        this.object = object;
    }

    public T get() {
        return object;
    }
}

В этом примере класс Box является обобщенным. Он принимает параметр типа T, который можно использовать в других методах класса.
Использование обобщенного класса:

Box<String> stringBox = new Box<>();
stringBox.set("Hello, Generics!");
String value = stringBox.get();

Здесь T заменяется на String, и теперь Box может хранить только строки.

2. Параметризованные Типы

Можно создавать обобщенные интерфейсы и методы. Пример параметризованного метода:

public static <T> void printArray(T[] array) {
  for (T element : array) {
    System.out.println(element);
  }
}

Метод printArray может принимать массив любого типа, поскольку T является параметром типа.

3. Безопасность типов

Одним из основных преимуществ Generics является безопасность типов. Использование Generics позволяет избежать ошибок времени выполнения, связанных с приведением типов. Например, если бы мы использовали обычный класс, тип данных преобразуется в Object, и приведение типов может привести к ошибкам:

Box box = new Box();
box.set("Hello");
String value = (String) box.get(); // Здесь может произойти ошибка ClassCastException, если был установлен другой тип.

С Generics это невозможно:

Box<String> box = new Box<>();
box.set("Hello");
String value = box.get(); // Безопасно, нет необходимости в приведении типов.

4. Ограничения Generics
   
Java поддерживает несколько ограничений Generics, которые могут быть применены к параметрам типа:

  class NumberBox<T extends Number> {
    private T number;

    public void set(T number) {
        this.number = number;
    }

    public T get() {
        return number;
    }
}

Здесь T может быть только Number или его подклассами (например, Integer, Double и т. д.).

5. Стирательность (Type Erasure)

При компиляции Java удаляет информацию о типах, чтобы обеспечить обратную совместимость с версиями Java, которые не поддерживают Generics. Это называется стирательностью типов. Это означает, что в байт-коде не сохраняется информация о типах, и обобщенные классы фактически используются как их ограничивающие параметры.


[← Вернуться к вопросам](README.md)
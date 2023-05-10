[Вопросы для собеседования](README.md)

# Spring

+ [Spring Core](#Spring-Core) [Junior]
+ [Spring MVC](#Spring-MVC) [Junior]
+ [Spring Validator](#Spring-Validator) [Junior]
+ [Spring Boot](#Spring-Boot) [Junior]
+ [Spring Security](#Spring-Security) [Junior]
+ [Spring REST](#Spring-REST) [Junior]
+ [JWT](#JWT) [Junior]

## Spring Core

__Framework__ - Платформа, которая определяет структуру системы (приложения) и облегчает разработку системы и их интеграцию.
Фреймворк - это больше, чем просто библиотека (определяет структуру системы, предоставляет определенные паттерны разработки).

__Востребованность Spring__:
+ Один из самых популярных web-фреймворков в мире.
+ Самый популярный Java-фреймворк.
+ Java - один из самых популярных ЯП в мире. Spring обычно используется везде, где используется Java.
+ Очень востребован работодателями по всему миру.

Spring Framework сщстоит из множества компонентов => облегчает множество аспектов разработки приложений на Java.
Компоненты:
+ Контекст приложения (Application Context) и Внедрение зависимостей (Dependency Injection).
+ Удобный и эффективный доступ к БД (замена JDBC).
+ Компонент для разработки web-приложений на Java (Spring MVC)/
+ Множество других полезных компонентов (spring.io).

__Application Context & Dependency Injection__

Типичное Java приложение - это набор Java объектов, которые взаимодействуют друг с другом и ссылаются друг на друга.

![image](https://user-images.githubusercontent.com/116163780/236843731-63d77f43-3282-47bc-bed6-8c6b45f0dfc1.png)

Кргда Java приложение запускается, все необходимые Java объекты создаются и помещаются в оперативную память. В ходе работы приложения, объекты могут добавляться / удаляться. Также могут изменяться связи между объектами.
Большое количество объектов и связей между ними встречается в любом более-менее сложном Java приложении. Spring помогает нам в работе с множеством объектов.

Существуют некоторые проблемы при создании приложений, например, нужно что бы конкретный объект создавался только один раз (пример Database). Можно решить это без Spring с помощью паттерна Singleton. но для этого требуется дополнительный код. Еще одна проблема, что нужно внедрять ссылку на этот единственный объект (Database) во все остальные классы, выстроить иерархию. Можно сделать вручную, но это очень сложно и запутанно.

![image](https://user-images.githubusercontent.com/116163780/236846479-0ff13f4b-d6c6-4174-8d16-828ff6c7a490.png)

![image](https://user-images.githubusercontent.com/116163780/236848438-38ff8c7c-f143-4fcd-83f3-62bd231b815d.png)

Spring Framework дает возможность удобного и эффективного доступа к БД, предоставляет для этого множество инструментов для взаимодействия с БД.
JDBC - примитивный и неудобный способ взаимодествия с БД. Он не подходит для сложных приложений, слишком низкоуровневый.

__Spring MVC__ - компонент Spring Framework, который позволяет создавать Web - приложения.
Огромное количество Web - приложений в интернете работают на Spring MVC.
Помимо этого, Spring MVC часто используется в качестве backend - API для мобильных приложений.

## Наполнение конфигурационного файла Spring 
Конфигурационный файл Spring должен называться __applicationContext.xml__

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans  xmlns="http://www.springframework.org/schema/beans"
        xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
        xmlns:context="http://www.springframework.org/schema/context"
        xsi:schemaLocation="http://www.springframework.org/schema/beans
        http://www.springframework.org/schema/beans/spring-beans.xsd
        http://www.springframework.org/schema/context
        http://www.springframework.org/schema/context/spring-context.xsd">

    <bean id="testBean"
        class="ru.kirillova.springcourse.TestBean">
        <constructor-arg value="Neil"/>
    </bean>
</beans>
```

Это стандартная конфигурация, которая позволяет использовать Spring Framework.
В теге `<bean>` создается новый бин, у него есть `id` - уникальный идентификатор объекта, `class`- путь к классу, бин которого мы хотим создать, `TestBean` - название класса, бин которого мы хотим создать, `"ru.kirillova.springcourse.TestBean"` - соответственно сам путь до класса, ` <constructor-arg>` -  передаем параметры для конструктора для создания бина.

## Inversion of Control (IoC)
__Инверсия управления__

![image](https://user-images.githubusercontent.com/116163780/237034903-2a9d2e96-d5e7-442c-97fb-ca87a6ed1655.png)

![image](https://user-images.githubusercontent.com/116163780/237035316-c8af838e-5975-4fc8-b514-107f95413f0e.png)

![image](https://user-images.githubusercontent.com/116163780/237035955-ccc47398-0419-42b7-801b-f827a805a8a8.png)


__Что такое Bean?__

Это просто Java объект. Когда Java объекты создаются с помощью Spring'а они называются бинами (beans).
Бины создаются из Java классов (так же, как и обычные объекты).

```xml
<bean id="testBean"
        class="ru.kirillova.springcourse.TestBean">
        <constructor-arg value="Neil"/>
</bean>
```

![image](https://user-images.githubusercontent.com/116163780/237036918-4454190c-26e3-4a75-a466-43ba8da743d7.png)

`MusicPlayer` слабо зависит от интерфейса `Music`. В методе `playMusic()` видим, что `MusicPlayer` сам создает свои зависимости, даже если будем использовать Spring Framework, мы будем сами обращаться к application context'у и будем сами извлекать из него созданный бин.

![image](https://user-images.githubusercontent.com/116163780/237039107-8ec81f02-9819-4e60-a5c9-ac149ebb7d22.png)

__Inversion of Control__ - это такой архитектурный подход, когда сущность не сама создает свои зависимости, а когда зависимости для этой сущности поставляются извне.

![image](https://user-images.githubusercontent.com/116163780/237040068-24a936a8-f8c2-4318-a804-abe094fd2e32.png)

![image](https://user-images.githubusercontent.com/116163780/237040271-ecc4e3e0-ee8d-450e-af6d-7541e0ae2536.png)

![image](https://user-images.githubusercontent.com/116163780/237040521-49e6c6dd-748b-43d1-b544-0a8417eb5442.png)

Решние этой проблемы с помощью внедрения зависимостей (Dependency Injection) с помощью Spring Framework будет рассмотрена далее.


__Смотри код в папке `spring-app1` или уроки №5,6, показано на практике внедрение зависимостей и создание бинов на примере `MusicPlayer`__


## Какие есть способы конфигурации Spring Framework?
+ XML файл когфигурации (старый способ, но многие существующие приложения до сих пор его используют, будут рассмотрены несколько примеров далее с его использованием).
+ Java аннотации и немного XML (современный способ).
+ Вся конфигурация на Java коде (современный способ).

## Типичные шаги в работе со Spring
+ Создаем Java классы (будущие бины)
+ Создаем и связываем бины с помощью Spring (аннотации, XML или Java код)
+ При использовании, все объекты (бины) берутся из контейнера Spring

## Dependency Ijection
__Способы внедрения зависимостей:__
+ Через конструктор
+ Через setter
+ Можно внедрять ссылки или простые значения
+ Можно внедрять значения из внешнего файла
+ Есть множество конфигураций того, как внедрять (scope, init-method, destroy-method, factory method и т.д.)
+ Можно внедрять через XML, Java-аннотации или Java код
+ Процесс внедрения можно автоматизировать (Autowiring)

![image](https://user-images.githubusercontent.com/116163780/237057848-fd98f103-372d-4c97-97d7-7f1ac870c59d.png)

![image](https://user-images.githubusercontent.com/116163780/237058647-aa66855d-9e79-4d5d-bace-ca69530b75d3.png)

![image](https://user-images.githubusercontent.com/116163780/237059674-d64108fd-306a-4e25-9efb-9a726126303d.png)

__Что такое scope?__

Scope задает то, как Spring будет создавать ваши бины.
Есть такой scope, который называется __Singleton__, он используется по умолчанию.
Singleton - это паттерн программирования.

Если не указывать scope, то по умолчанию Singleton:

```xml
<bean id="musicBean"
	class="ru.kirillova.springcourse.ClassicalMusic">
</bean>
```

+ По умолчанию создается один объект (он создается до вызова метода `getBean()`).
+ При всех вызовах `getBean()` возвращается ссылка на один и тот же единственный объект.

Scope Singleton чаще всего используется тогда, когда у нашего бина нет изменяемых состояний (stateless).
Потому что если будем изменять состояние у Singleton бина, столкнемся с проблемой.

![image](https://github.com/Slimercorp/java-interview/assets/116163780/ba2e9681-33c3-46b0-a28a-eec7a8349d14)

Здесь видим, что среда разработки говорит, что Singleton используется по умолчанию, и указывать его явно нет смысла.

Еще один scope, который называется __Prototype__, каждый раз создает новый объект при вызове `getBean()`. Используется, когда у бина есть изменяемые состояния (stateful).

Другие scope'ы , такие как request, session, flobal-session, будут изучены в разделе Spring MVC.

## Жизненный цикл бина (Bean Lifecycle)
смотри код в папке C:\IntelliJ IDEA workspace\SpringCourse\Lesson8.InitDestroyAndFactory

__Специальные методы бинов__
init-method, destroy-method, factory method

![image](https://github.com/Slimercorp/java-interview/assets/116163780/31f09c3b-504c-4b64-bf56-7bb96a459243)

__init-method__
Это метод, который запускается в ходе инициализации бина. Используется для инициализации ресурсов, обращения к внешним файлам, запуска БД.

__destroy-method__
Этот метод, который запускается в ходе уничтожения бина (при завершении приложения). В этом методе обычно происходит очищение ресурсов, закрытие потоков ввода-выводы, закрытие доступа к БД.

![image](https://github.com/Slimercorp/java-interview/assets/116163780/08046928-642f-4c1b-8d9d-1311e034e79c)

```java
public class ClassicalMusic implements Music {
    private ClassicalMusic() {}

    public static ClassicalMusic getClassicalMusic() {
        return new ClassicalMusic();
    }

    public void doMyInit() {
        System.out.println("Doing my initialization");
    }

    public void doMyDestroy() {
        System.out.println("Doing my destruction");
    }

    @Override
    public String getSong() {
        return "Hungarian Rhapsody";
    }
}
```

__Тонкости init и destroy методов:__
+ Модификатор доступа - может быть любой у обоих методов (public, protected, private).
+ Тип возвращаемого значения - может быть любой, но чаще всего используется void, т.к. нет возможности получить возвращаемое значение.
+ Название метода - может быть любое.
+ Аргументы метода - эти методы не должны принимать на вход какие-либо аргументы.

Для бинов со scope "prototype" Spring не вызывает destroy мотод.
Spring не берет на себя полный жизненный цикл бинов со scope "prototype". Spring отдает prototype бины клиенту и больше о них не заботится (в отличие от singleton бинов).

__factory method__
Фабричный метод (англ. Factory Method) - это паттерн программирования.
Если объекты класса создаются фабричным методом, то можно определить factory method.

![image](https://github.com/Slimercorp/java-interview/assets/116163780/0719c747-c9d8-408e-80c7-b51d9ef039bc)

## Что такое Java аннотация?
__Java аннотация__ - это специальный тип комментариев в вашем коде с помощью которых можно:
+ Передавать какие-либо инструкции для Java компилятора (пример: @Override).
+ Передавать какие-либо инструкции для анализаторов исходного кода.
+ Передавать метаданные, которые могут быть использованы либо вашим Java приложением(с помощью рефлексии), либо другими приложениями или фреймворками (привет: Spring Framework).

![image](https://github.com/Slimercorp/java-interview/assets/116163780/fcb9649a-e134-4ba7-badd-969eda6fbbd2)

## Аннотация @Component
+ Помечаем ей класс, если хотим, чтобы Spring создал бин из этого класса.
+ Именно эту аннотацию Spring ищет, когда сканирует все ваши классы.
+ Можно указать `id` для создаваемого бина, можно не указывать (тогда будет название `название_класса_с_маленькой_буквы`).

При использовании аннотаций, ручное создание бинов в xml файле уже не актуально, нужно всего лишь сказать Spring чтобы он отсканировал все компоненты, включает эту операцию следующуя строка:

```xml
<context:component-scan base-package="ru.kirillova.springcourse" />
```

Теперь при запуске приложения Spring отсканирует все классы в пакете `springcourse` и создаст бины классов, помеченных аннотацией `@Component`.

## Аннотация @Autowired
Эта аннотация осущществляет внедрение зависимостей.

![image](https://github.com/Slimercorp/java-interview/assets/116163780/17b78544-93fc-415d-979d-a8c6b64a5685)

![image](https://github.com/Slimercorp/java-interview/assets/116163780/e8872f97-ef79-408a-a318-2521628a10c1)

Мы можем внедрять бины указывая конкретный класс, или какой-то интерфейс:

![image](https://github.com/Slimercorp/java-interview/assets/116163780/6b42a6e2-a034-409c-ae79-39eee193dcc9)

![image](https://github.com/Slimercorp/java-interview/assets/116163780/81dc0195-cbe8-40af-9325-d877c0df8e45)

![image](https://github.com/Slimercorp/java-interview/assets/116163780/df84209f-2f15-4814-9757-0600fb776e62)

## Аннотация @Qualifier
Решает проблему неоднозначности, когда для внедрения подходят несколько бинов.

![image](https://github.com/Slimercorp/java-interview/assets/116163780/c552d69e-dbcf-4094-9640-6f8e21411cf2)

Эту аннотацию можно использовать на :
+ Конструкторах
+ Сеттерах
+ Полях

![image](https://github.com/Slimercorp/java-interview/assets/116163780/63d80334-b6e6-4e47-8279-4218283e9175)

![image](https://github.com/Slimercorp/java-interview/assets/116163780/f2b55a1e-7488-4bf3-ac30-0a057e42fddb)

![image](https://github.com/Slimercorp/java-interview/assets/116163780/99751ac7-a986-4c53-8603-aba18ab3ff03)


## Аннотация @Value

![image](https://github.com/Slimercorp/java-interview/assets/116163780/65b54e68-418e-408d-8388-c5bc72b2da3c)

Тоже самое можно делать с помощью `@Value`.

![image](https://github.com/Slimercorp/java-interview/assets/116163780/22f1be1d-5f90-40a5-906b-09ffb07e75ed)

Первые два шага идентичны, но внедрение осуществляем с помощью `@Value`. Аннотируем (помечаем) поля, в аргументы посталяем название ключа. Значение, которое лежит по этому ключу будет внедрено в соответствующее поле.

## Аннотация @Scope

![image](https://github.com/Slimercorp/java-interview/assets/116163780/01867ddd-13f6-4341-8fd3-6e202a5c3aa4)

Конфигурацию области видимости мы тоже можем настроить с помощью аннотаций - для этого и существует @Scope.

![image](https://github.com/Slimercorp/java-interview/assets/116163780/8b00b9bb-e08f-4695-a07b-a955c6d220fb)

## Аннотации @PostConstruct и @PreDestroy
Есть два метода из жизненного цикла бина - init-method и destroy-method. В Spring аннотации `@PostConstruct` и `@PreDestroy` делают тоже самое. 

![image](https://github.com/Slimercorp/java-interview/assets/116163780/104d665f-253b-4a54-a976-203b708abf85)

![image](https://github.com/Slimercorp/java-interview/assets/116163780/6681706a-1572-46bb-9b61-bc88abe10684)

![image](https://github.com/Slimercorp/java-interview/assets/116163780/d0e885b7-4750-4cd3-a92e-8888f0eae294)

## Spring конфигурация с помощью Java кода

![image](https://github.com/Slimercorp/java-interview/assets/116163780/93c651f8-ddaf-4f67-b938-ebc50453be8a)

__Аннотация @Configuration__

![image](https://github.com/Slimercorp/java-interview/assets/116163780/ce103b2c-a692-48d3-a24e-59c22c15631d)

![image](https://github.com/Slimercorp/java-interview/assets/116163780/e7e92b79-ac21-4fde-b271-ff5970e33e8d)

![image](https://github.com/Slimercorp/java-interview/assets/116163780/690bbbd5-10cb-468d-ac04-147f0446a734)

![image](https://github.com/Slimercorp/java-interview/assets/116163780/7360c04f-3668-4678-ae75-61e4463c1546)

Раньше использовали  класс `ClassPathXmlApplicationContext` и указывали ему путь до конфигурационного xml файла. Теперь используем другой класс `AnnotationConfigApplicationContext`, ему на вход передаем конфигурационный класс и получаем доступ к контесту, из которого впоследствии можем получать бины.

![image](https://github.com/Slimercorp/java-interview/assets/116163780/13ab6db6-8a8d-4db8-a9de-e0888b222ba0)

__@Bean__
![image](https://github.com/Slimercorp/java-interview/assets/116163780/45adc3af-2b19-46c5-b213-2ab548e4fb49)

![image](https://github.com/Slimercorp/java-interview/assets/116163780/d7656935-1399-40d3-bb1e-231daec8bc77)

![image](https://github.com/Slimercorp/java-interview/assets/116163780/36ac88d1-7c79-46f2-97b0-b4620bd26b40)

@PropertySource указывает путь до файла с нашими входными значениями.









## Spring MVC

## Spring Validator

## Spring Boot

## Spring Security

## Spring REST

## JWT













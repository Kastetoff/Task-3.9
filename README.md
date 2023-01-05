# JvmComprehension

### В данном файле описывается исполнение кода в части **Java Virtual Machine**
 
## Исходный код:

```java
public class JvmComprehension {

    public static void main(String[] args) {
        int i = 1;                      // 1
        Object o = new Object();        // 2
        Integer ii = 2;                 // 3
        printAll(o, i, ii);             // 4
        System.out.println("finished"); // 7
    }

    private static void printAll(Object o, int i, Integer ii) {
        Integer uselessVar = 700;                   // 5
        System.out.println(o.toString() + i + ii);  // 6
    }
}
```
## Class Loader
Bootstrap ClassLoader подгружает следующие классы: *Object, Integer, String*

Application ClassLoader подгружает следующие классы: *JvmComprehension*

Подгруженные классы размещаются в области памяти **Metaspace**

## Stack, Heap, Metaspace areas in memory
1. Создается новый фрэйм основного метода **main()**. В этом фрэйме инициализируется переменная *int i = 1*
2. В фрэйме метода **main()** инициализируется переменная *o* и появлется ссылка на объект **Object**, созданный в ***Куче***
3. В фрэйме метода **main()** инициализируется переменная *ii = 2* и появлется ссылка на объект **Integer**, созданный в ***Куче***
4. Создается новый фрэйм метода **printAll()**. В этом фрэйме инициализируются переменные *(o, i, ii)*, переданные в аргументах. 
при этом Переменная *"o"* имеет сслыку на объект **Object** (п.2), а переменная *"ii"* имеет сслыку на объект **Integer** (п.3)
5. В этом же фрэйме инициализируется переменная *uselessVar = 700* со сслыкой на объект **Integer**, из ***Кучи***
6. Создается новый фрэйм метода **out.println()**. В этом фрэйме появляются ссылки на переменные *(o, ii)* и инициализируется переменная *i* 
7. В фрэйме метода **main()** инициализируется переменная со значением *"finished"* и появлется ссылка на объект **String**, созданный в ***Куче***

## Garbage Collector
В сборщик мусора больше всего шансов попасть у переменной *uselessVar = 700*, т.к. присвоенное ей значение никогда не используется
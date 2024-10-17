# Lab1
## Отчет по лабораторной работе № 1

#### № группы: `ПМ-2403`

#### Выполнила: `Соколова Анастасия Павловна`

#### Вариант: `25`

### Cодержание:

- [Постановка задачи](#1-постановка-задачи)
- [Входные и выходные данные](#2-входные-и-выходные-данные)
- [Выбор структуры данных](#3-выбор-структуры-данных)
- [Алгоритм](#4-алгоритм)
- [Программа](#5-программа)
- [Анализ правильности решения](#6-анализ-правильности-решения)

### 1. Постановка задачи

> Набор бусинок диаметрами A, B, C, D, надетый на нить, пытаются
протащить в указанном порядке через отверстие диаметром X. Какое
количество бусинок удастся протащить через отверстие? На вход программы
подаются натуральные числа X, A, B, C, D
> 
Программа получает на вход 5 натуральных чисел X, A, B, C, D. Нужно сравнить последние четыре числа с первым и посчитать количество тех, что последовательно не превышают значение числа Х.

Данную задачу можно разделить на 2 подзадачи: сравнение чисел и поиск их количества.

### 2. Входные и выходные данные

#### Данные на вход

На вход программа должна получать 5 натуральных чисел. Этим задается нижняя граница (число >=1), но верхней не существует (до бесконечности).

|             | Тип               | min значение | max значение |
|-------------|-------------------|--------------|--------------|
| X (Число 1) | Натуральное число |      1       |     +∞       |
| A (Число 2) | Натуральное число |      1       |     +∞       |
| B (Число 3) | Натуральное число |      1       |     +∞       |
| C (Число 4) | Натуральное число |      1       |     +∞       |
| D (Число 5) | Натуральное число |      1       |     +∞       |


#### Данные на выход

Т.к. программа должна вывести число возможных успехов выполнения сравнения, то на выход мы получим
единственное натуральное число, не превышающее 4 (максимальное число всех возможных успехов), или 0.

|         | Тип                         | min значение | max значение   |
|---------|---------------------------- |--------------|----------------|
| Число 6 | Целое неотрицательное число |      0       |      4         |

### 3. Выбор структуры данных

Программа получает 5 натуральных чисел, которые больше или равны 1, но не ограничины в своем максимальном значении. Поэтому для их хранения
можно выделить 5 переменных (`x`, `a`,`b`,`c`,`d`,) и использовать наиболее объемный целочисленный тип данных - long. 

|             | название переменной | Тип (в Java) | 
|-------------|---------------------|--------------|
| X (Число 1) | `x`                 | `long`     |
| A (Число 2) | `a`                 | `long`     | 
| B (Число 3) | `b`                 | `long`     |
| C (Число 4) | `c`                 | `long`     | 
| D (Число 5) | `d`                 | `long`     |


Результат представлен в виде целого неотрицательного числа в промежутке от 0 до 4 включительно. 
Для этого можно использовать более простой тип данных int.

|             | название переменной | Тип (в Java) | 
|-------------|---------------------|--------------|
| K (Число 6) | `k`                 | `int`        | 


### 4. Алгоритм

#### Алгоритм выполнения программы:

1. **Ввод данных:**  
   Программа считывает 5 натуральных чисел, обозначенные как `x`, `a`, `b`, `c`, `d`.

2. **Сравнение чисел и счетчик:**  
   - Программа сравнивает значения `x` и `a`. Если `a` меньше или равно `x`, программа увеличивает значение переменной-счетчика `k` на 1.
   - Затем по тому же условию сравниваются `x` и `b` и в случае успеха к переменной `k` прибавлется  единица.
   - Затем по тому же условию сравниваются `x` и `b` и в случае успеха к переменной `k` прибавлется  единица.
   - По той же схеме последовательно происходит сравнение `x` и `c` и `x` и `d`. Счетчик `k` при этом увеличивается на 1 только в случае успеха.

5. **Вывод результата:**  
   Результат подсчета всех удовлетворительных неравенств, хранящийся в переменной-счетчике `k`, выводится на экран.

#### Блок-схема

```mermaid
graph TD
    A([Начало]) --> B[/Ввести: x, a, b, c, d.
k=0/]
    B --> C{a <= x}
    C -- Да --> E((k+1))
    C -- Нет --> D((k=k))
    E --> F[/b <= x/]
    D --> F[/b <= x/]
    F -- Да --> G((k+1))
    F -- Нет --> H((k=k))
    G --> I[/c <= x/]
    H --> I[/c <= x/]
    I -- Да --> J((k+1))
    I -- Нет --> K((k=k))
    J --> L[/d <= x/]
    K --> L[/d <= x/]
    L -- Да --> M((k+1))
    L -- Нет --> N((k=k))
    M --> O[/Вывод k/]
    N --> O
    O --> Z([Конец])


```

### 5. Программа

```java
import java.util.Scanner;
public class Main {
    // Объявляем объект класса Scanner для ввода данных
    public static Scanner in = new Scanner(System.in);
    public static void main(String[] args) { {
    // Считывание пяти натуральных чисел x,a,b,c,d
        long x = in.nextLong();
        long a = in.nextLong();
        long b = in.nextLong();
        long c = in.nextLong();
        long d = in.nextLong();
    // Обнуление счетчика `k` до его минимального возможнонго значения `0`
        int k = 0;
    // Сравнение эталонного числа с первым элементом 
        if (a<=x)
        {
            // Добавление к `k=0` единицы в случае удовлетворительного значения `a` относительно `x`
            k=k+1;
            // Последующее сравнение элемента `b` с шаблонным числом `x`
            if (b<=x)
            {
                // Добавление к `k` единицы в случае удовлетворительного значения `b` относительно `x`
                k=k+1;
                // Последующее сравнение элемента `c` с шаблонным числом `x`
                if (c<=x)
                {
                    // Добавление к `k` единицы в случае удовлетворительного значения `c` относительно `x`
                    k=k+1;
                    // Последующее сравнение элемента `d` с шаблонным числом `x`
                    if (d<=x)
                    {
                        // Добавление к `k` единицы в случае удовлетворительного значения `d` относительно `x`
                        k=k+1;
                    }
                }
            }
        }
        // Вывод значения `k` 
        System.out.print(k);
    }
    }
}
```

### 6. Анализ правильности решения

Программа работает корректно на всем множестве решений с учетом ограничений.

1. Тест на `X > A > B > C > D`:

    - **Input**:
        ```
        10
        4
        3
        2
        1
        ```

    - **Output**:
        ```
        4
        ```

2. Тест на `X > D > C > B > A`:

    - **Input**:
        ```
        15
        5
        6
        7
        10
        ```

    - **Output**:
        ```
        4
        ```

3. Тест на `X > C > D > A > B`:

    - **Input**:
        ```
        20
        6
        3
        18
        14
        ```

    - **Output**:
        ```
        4
        ```

4. Тест на `B > X > A > C > D`:

    - **Input**:
        ```
        80
        70
        100
        21
        14
        
        ```

    - **Output**:
        ```
        1
        ```

5. Тест на `A > B > C > D > X`:

    - **Input**:
        ```
        1654
        1963254
        995422
        874562
        2154
        ```

    - **Output**:
        ```
        0
        ```
 6. Тест на `C > D > X > A > B`:

    - **Input**:
        ```
        305
        300
        51
        5010
        501
        ```

    - **Output**:
        ```
        2
        ```

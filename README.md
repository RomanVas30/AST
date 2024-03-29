# Отчет по домашнему заданию

## (Алгоритмы и структуры данных)

### Условие задачи:

`Напишите программу, которая строит абстрактное синтаксическое дерево по исходному коду. Вход — исходный код программы на выбранном студентом языке общего назначения.`

## Теоретическая часть:
#### Список определений:
* ***Абстрактное синтаксическое дерево (AST)*** - дерево представление абстрактной синтаксической структуры исходного кода, написанного на языке программирования. Каждый узел дерева обозначает конструкцию, встречающуюся в исходном коде.
* ***Взаимная рекурсия*** - форма рекурсии, где математические или вычислительные объекты, такие как функции или типы данных, определены в терминах друг друга.
* ***Грамматика*** - набор правил для преобразования строк.
* ***Контекстно-свободная грамматика*** - определенный тип формальной грамматики: набор правил производства, которые описывают все возможные строки в данном формальном языке. Правила производства - простые замены.
* ***Терминальные символы*** - элементарные символы языка, определенные формальной грамматикой.
* ***Нетерминальные символы*** - сторонние символы, заменяющиеся группами терминальных символов в соответствии с правилами производства.

#### Основные подходы к решению:
##### 1. Метод рекурсивного спуска.
Метод рекурсивного спуска - алгоритм нисходящего синтаксического анализа, реализуемый путём взаимного вызова процедур, где каждая процедура соответствует одному из правил контекстно-свободной грамматики. Применения правил последовательно, слева-направо поглощают токены, полученные от лексического анализатора. \
Данный метод имеет два варианта реализации: 

__Предсказывающий парсер__ 

Для парсеров этого типа нужна `LL(k)` грамматика, позволяющая по очередному токену или токенам однозначно выбрать один из альтернативных вариантов раскрытия каждого нетерминала

Основные шаги алгоритма: 
1. Анализатор считывает следующий доступный символ из входного потока и самый верхний символ из стека;  
2. Если символы совпадают, отбрасываем их и возвращаемся на Шаг 1; 
3. Обращаемся к таблице синтаксического анализа, выясняем, какое правило из грамматики необходимо применить и переходим на Шаг 1.

_Сложность: __O(n)___

__Парсер с возвратом__

Вместо предсказания парсер просто пытается применить все альтернативные варианты правил по порядку, пока одна из попыток не увенчается успехом

Основные шаги алгоритма:
1. Последовательный просмотр входной строки слева-направо;  
2. Очередной символ входной строки является основанием для выбора одной из правых частей правил группы при замене текущего нетерминала; 
3. Терминальные символы входной строки и правой части правила «взаимно уничтожаются»;  
4. Обнаружение нетерминала в правой части рекурсивно повторяет этот же процесс.
 
_Сложность: до __O(<nobr>*2*^n</nobr>)___

##### 2. Синтаксический анализатор приоритетов.
Реализация похожа на метод рекурсивного спуска наоборот. \
Этот синтаксический анализатор опирается на следующие три отношения: <, >, = 
* `a < b` - означает, что а «уступает приоритет» b. 
* `a > b` - означает, что а «имеет приоритет над» b. 
* `a = b` - означает, что а «имеет приоритет как» b. 

По ним строится таблица отношений приоритета оператора для данной грамматики. Недостатком этой таблицы также то, что если у нас есть n операторов, то размер таблицы будет ***nxn***, а сложность  по памяти - ***O(<nobr>*n*^2</nobr>)***.

Алгоритм:
1) Считать символ из входной строки и добавить его в стек.
2) Сравнить следующий символ из входной строки с первым символом стека: если отношение `<` или `=`, то добавить текущий символ в стек. В противном случае переместить символ из начала стека в массив.
3) Сравнить начальный символ из стека и крайний левый символ массива. Если отношение `>`, то переместить символ из начала стека в массив и повторить Шаг 3.
4) Пройти по сформированному массиву и заменить все вхождения левой части правил на правую. Если входная строка еще не пуста, то перейти на Шаг 2.

Сложность: ***O(<nobr>*n*^2</nobr>)***

#### Выбор алгоритма и примерный план решения:
Для начала будет реализован `Lexer`, который токенизирует входную строку с исходным кодом.


Для построения самого AST будет использоваться __Метод рекурсивного спуска__, потому что данный метод не только является основой реализации большинства компиляторов, в которых строится AST, но и имеет относительно небольшую сложность.
#### Форматы входных и выходных данных
##### Входные данные: 
Файл с корректным исходным кодом программы на языке С++.
##### Выходные данные:
Файл с AST по исходному коду.

##### Пример:
Входной файл:
```cpp 
int main(){
    int a = 5;
    std::cout << a;
}
```
Выходной файл:
```
(Pr) -> (func: main) -> (type: int)
	             -> (body) -> (decl: a) -> (type: int)
			       		    -> (value: 5)
		               -> (op: <<) -> (stream: std::cout)
					   -> (value: a)
```

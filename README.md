Принцып параллельного решета Эратосфена. В классическом алгоритме, если мы ищем простые числа
среди первых $N$ чисел, то перебирать достаточно до $\sqrt{N}$, после этой границы уникальных простых
делителей не будет. Остается только проверять делимость на те числа, которые мы нашли до $\sqrt{N}$.

Разделим весь диапазон от 0 до $N$ на батчи длинной $batch size = \sqrt{N}$. Заметим, что количество
таких батчей будет в точности равно $batch size$. Перенумеруем батчи от 0 до $batch size - 1$. 
В нулевом батче найдем все простые числа классическим решетом, назовем эти числа уникальными
простыми делителями. 

Заметим, что если мы имеем простое число $prime$ и число $x$, которое делится на $prime$, то любые 
числа $x + n \cdot prime$ так же делятся на $prime$.

Возмем первый уникальный простой делитель в нулевом батче (это будет число 3). Для каждого батча от 1
до $batch size - 1$ надем первое в этом батче число, которое кратно 3, пусть это будет число $x$.
Далее нам остается только вычеркнуть все числа, начиная с числа $x$ с шагом 3 в рамках этого батча.

Проделываем эти действия для каждого уникального простого делителя и для каждого батча.

В параллельной реализации зоны ответственности каждого потока -- батчи.
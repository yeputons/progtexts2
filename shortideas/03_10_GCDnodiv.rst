НОД без деления
---------------

Я надеюсь, вы все представляете, как считать НОД двух чисел алгоритмом
Евклида. На всякий случай напомню: пусть вам надо посчитать
:math:`{{НОД}}(a,b)`. Если :math:`b=0`, но :math:`{{НОД}}(a,b)=a`, иначе
:math:`{{НОД}}(a,b)={{НОД}}(b, a \bmod b)`. Получаем следующий алгоритм:

::

    function gcd(a,b:integer):integer;
    begin
    if b=0 then
       gcd:=a
    else gcd:=gcd(b,a mod b);
    end;

Можно показать, что этот алгоритм работает за
:math:`O(\max(\log a,\log b))`. В частности, поэтому имеет смысл
поставить задачу поиска НОД *длинных* чисел. Но, как только вы глянете
на приведённый выше код, сразу поймёте, что написать такое будет весьма
нетривиально и неприятно. Действительно, кому охота реализовывать
деление длинного на длинное (для mod)?

Но есть способ посчитать НОД без деления. Точнее, без деления длинного
на длинное. А именно, применим ту же идею, что применяли для быстрого
возведения в степень. Посмотрим на остатки :math:`a` и :math:`b` по
модулю 2. Возможны четыре случая:

-  :math:`a \bmod 2=b\bmod 2=0`. Тогда очевидно, что
   :math:`{{НОД}}(a,b)=2\cdot{{НОД}}(a/2,b/2)`.

-  :math:`a\bmod 2=0`, но :math:`b\bmod 2=1`. Тогда
   :math:`{{НОД}}(a,b)={{НОД}}(a/2,b)`.

-  :math:`a\bmod 2=1`, и :math:`b\bmod 2=0`. Догадайтесь сами :)

-  :math:`a\bmod 2=b\bmod 2=1`. Тогда
   :math:`{{НОД}}(a,b)={{НОД}}(|a-b|,b)` типа того (модуль для того,
   чтобы числа оставались положительными; может быть, можно и без него.
   Можно обойти эту проблему и как-нибудь по-другому...).



.. task::

    Докажите все эти утверждения.
    |
    |
    |

Этот алгоритм тоже работает за :math:`O(\max(\log a,\log b))`, т.к.
каждый вариант, кроме последнего, уменьшает хотя бы одно из чисел в 2
раза, и не бывает так, чтобы два раза подряд получился последний вариант
(почему? :)), поэтому как минимум каждая вторая итерация будет уменьшать
хотя бы одно из чисел в два раза.

Но главное — здесь надо уметь делить только на два. Надеюсь, написать
длинное деление на два и вычисление остатка по модулю два для вас элементарно
:).

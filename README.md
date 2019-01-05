#### @BroNaz

# 1. Контейнеры STL,основные функции работы с контейнерами.
что такое ? 

Библиотека [контейнеров](https://ru.cppreference.com/w/cpp/container) является универсальной коллекцией шаблонов классов и алгоритмов, позволяющих программистам легко реализовывать общие структуры данных, такие как очереди, списки и стеки. Существует три вида контейнеров: последовательные контейнеры, ассоциативные контейнеры, и неупорядоченные ассоциативные контейнеры, каждый из которых предназначен для поддержки различных наборов операций.

Контейнер управляет выделяемой для его элементов памятью и предоставляет функции-члены для доступа к ним, либо непосредственного, либо через итераторы (объекты, обладающие схожими с указателями свойствами).

Большинство контейнеров обладают по крайней мере несколькими общими функциями-членами и общей функциональностью. Выбор оптимального контейнера для конкретного случая зависит не только от предоставляемой функциональности, но и от его эффективности при различных рабочих нагрузках. 
> следующее разделение взято [microsoft.com](https://docs.microsoft.com/en-us/cpp/standard-library/stl-containers?view=vs-2017)

+ Контейнеры последовательности
+ Ассоциативные Контейнеры

#### Контейнеры последовательности

Контейнеры последовательности поддерживают порядок вставки указанных вами элементов.
подробное описание классов: 

[std::vector](https://docs.microsoft.com/en-us/cpp/standard-library/vector-class?view=vs-2017) 

[std::array](https://docs.microsoft.com/en-us/cpp/standard-library/array-class-stl?view=vs-2017)

[std::deque](https://docs.microsoft.com/en-us/cpp/standard-library/deque-class?view=vs-2017)

[std::list](https://docs.microsoft.com/en-us/cpp/standard-library/list-class?view=vs-2017)

[std::forward_list](https://docs.microsoft.com/en-us/cpp/standard-library/forward-list-class?view=vs-2017)


#### Ассоциативные Контейнеры

В ассоциативных контейнерах элементы вставляются в заранее определенном порядке, например, по возрастанию. Неупорядоченные ассоциативные контейнеры также доступны. Ассоциативные контейнеры можно сгруппировать в два подмножества

[std::map](https://docs.microsoft.com/en-us/cpp/standard-library/map-class?view=vs-2017), иногда называемый словарем, состоит из пары ключ / значение. Ключ используется для упорядочения последовательности, и значение связано с этим ключом.
Неупорядоченная версия mapесть [unordered_map](https://docs.microsoft.com/en-us/cpp/standard-library/unordered-map-class?view=vs-2017)

[std::set](https://docs.microsoft.com/en-us/cpp/standard-library/set-class?view=vs-2017) -  это просто восходящий контейнер уникальных элементов - значение также является ключом. Неупорядоченная версия set есть [unordered_set](https://docs.microsoft.com/en-us/cpp/standard-library/unordered-set-class?view=vs-2017)

Упорядоченные карты и наборы поддерживают двунаправленные итераторы, а их неупорядоченные аналоги поддерживают прямые итераторы




> следующее разделение взято из книги [С++17 STL](https://vk.com/doc44301783_470643658?hash=7fa27aef42121f5313&dl=c61cb4e22b67ea12bc)

Все контейнеры, предоставляемые STL, можно разделить на такие категории:
+ непрерывные хранилища
+ списки
+ деревья поиска
+ хеш-таблицы
+ адаптеры контейнеров

#### Непрерывные хранилища
Самый простой способ хранения объектов — поместить их рядом друг с другом в одном большом фрагменте памяти. Произвольный доступ к такому фрагменту выполняется за время O(1).
Это проще всего сделать так: воспользоваться контейнером __std::array__. Массивы STL имеют фиксированный размер, определяемый при создании. Контейнер __std::vector__ вступает в дело, когда вам нужно хранилище, похожее на массив, но с изменяемой длиной. Он использует память из кучи для хранения объектов.


#### Хранение списков 
Контейнер __std::list__ представляет собой классический двухсвязный список.Ни больше ни меньше. Если вам нужно выполнять обход списка только в одном направлении, то больше подойдет контейнер __std::forward_list__ — он быстрее работает и занимает меньше места, поскольку в нем хранятся лишь указатели на следующий элемент. Пройти список можно только последовательно, за время O(n).  Вставку и удаление элементов в заданную позицию можно выполнить за время O(1). 


#### Деревья поиска 
Если для объектов характерен естественный порядок, такой, что их можно отсортировать с использованием математического отношения <, то их можно поддерживать в этом же порядке с помощью деревьев поиска. Из названия следует: конкретный элемент дерева легко находится благодаря ключу поиска, что дает возможность выполнять эту операцию за время O(log(n)). В STL есть несколько видов таких деревьев, самым простым является __std::set__ — в нем хранятся уникальные сортируемые объекты.Контейнер __std::map__ отличается тем, что данные в нем хранятся парами. Пара состоит из ключа и значения. Дерево поиска использует ключ для сортировки элементов, таким образом можно задействовать __std::map__ в качестве ассоциативного контейнера. Как и в случае с контейнером __std::set__, ключи в дереве должны быть в единственном экземпляре. Контейнеры __std::multiset__ и __std::multimap__ являются частными случаями контейнеров, показанных выше, для которых отсутствует требование уникальности ключей.


#### Хеш - таблицы 
В хеш - таблицах элементы можно найти за время O(1), но они игнорируют естественный порядок элементов, поэтому не так просто пройти по упорядоченному списку. Контейнеры __std::unordered_set__ и __std::unordered_map__ весьма похожи на __std::set__ и __std::map__, что можно утверждать на основании их взаимозаменяемости. Как и реализации поисковых деревьев,у обоих контейнеров есть 
«коллеги» __std::unordered_multiset__ и __std::unordered_multimap__, которые не имеют ограничения на уникальность объектов, ключей,  поэтому можно хранить несколько элементов для одного ключа


#### Адаптеры контейнеров 
Массивы, списки, деревья и хеш-таблицы не единственный способ хранения данных и получения к ним доступа. Еще есть стеки, очереди и т.д. Аналогично тому, как более сложные структуры могут быть реализованы с использованием более примитивных, в STL такие структуры создаются благодаря следующим классам адаптерам контейнеров : __std::stack__, __std::queue__ и __std::priority_queue__. 

### основные функции(Операции ??) 
подробная таблица [тут](https://vk.com/doc182687495_486181627?hash=c0e733e1da504d26cd&dl=5f7b94af6d86fab217) стр 284-286

| Описание      | Требование         | Действие |
| ------------- |:------------------:| -----:|
| ContType c     | ДА    | Конструктор по умолчанию. Создает пустой контейнер, не содержащий ни одного элемента|
| ContType c(с2)     | ДА    | Копирующий конструктор |
| ContType c = с2     | ДА    | Копирующий конструктор|
| ContType c(rv)     | ДА    | Перемещающий конструктор|
| ContType c = rv     | ДА    | Перемещающий конструктор|
| ContType c(beg, end)     | -    |Создает и инициализирует его копиями всех элем. интервалов [beg, end)|
| ContType c(initlist)     | -    | Создает и инициализирует его копиями значений из списка initlist|
| ContType c = initlist     | -    | Создает и инициализирует его копиями значений из списка initlist|
| c.~ContType()     | ДА    | Удаляет и освобождает память, если это возможно|
| c.empty()     | ДА    | Возвращает признак того, что контейнер пуст  |
| c.size()     | ДА    |Возвращает текущее кол-во элементов |
| c.max_size()     | ДА    |Возвращает максимально возможное кол-во элементов |
| c1 == с2     | ДА    |Возвращает признак того, что контейнер с1 равен с2|
| c1 != с2     | ДА    |Возвращает признак того, что контейнер с1 не равен с2|
| c1 < с2     | -    |Возвращает признак того, что контейнер с1 меньше с2|
| c1 > с2     | -    |Возвращает признак того, что контейнер с1 больше с2|
| c1 <= с2     | -    |Возвращает признак того, что контейнер с1 меньше или равен с2|
| c1 >= с2     | -    |Возвращает признак того, что контейнер с1 больше или равен с2|
| c1.swap(c2)    | ДА  |Обменивает данные контенеров|
| swap(с1 , c2)    | ДА  |Обменивает данные контенеров|
| c1.begin()    | ДА  |Возвращает итератор, установленный на первый элемент|
| c1.end()    | ДА  |Возвращает итератор, установленный на позицию следующую за послед. элементом|
| c1.сbegin()    | ДА  |Возвращает константный итератор, установленный на первый элемент|
| c1.сend()    | ДА  |Возвращает константный итератор, установленный на позицию следующую за послед. элементом|
| с.clear()    | -  |Опустошает контенер|


# 2. Итераторы.
что такое ? 

Итератор — структура данных, которая «указывает» на некоторый элемент контейнера, и (для некоторых контейнеров) умеет переходить к предыдущему/следующему элементу.

зачем нужно ? 

Пускай у вас есть контейнер. Неважно какой: _map_ , _vector_ , _set_ и тд . Он содержит набор элементов. И вы хотите сослаться не на весь контейнер, а на какое-то место в этом наборе элементов. Так чтобы от этого места можно было перейти вперёд/назад, и что-то в этом месте сделать: изменить элемент, вставить элемент, удалить элемент.

----------------------------------------------------------------------------------------------------------------------------------------
Если вы хотите реализовать итератор, помните, что существуют разные типы итераторов, в зависимости от операций, которые они предоставляют. Вот [список](https://en.cppreference.com/w/cpp/iterator) возможных типов.

Если вы, например, хотите реализовать RandomAccessIterator, вам придётся определить конструктор копирования, оператор присваивания, деструктор, операции ==, !=, *, ->, конструктор без аргументов, ++, --, +=, + (2 шт.), -=, - (2 шт.), <, >, <=, >=. (Другие типы итераторов попроще.)

Кроме того, вам придётся специфицировать std::iterator_traits<<It>It> [(тут подробнее)](https://en.cppreference.com/w/cpp/iterator/iterator_traits), где It — тип вашего итератора.
  
Итераторы обычно используются парами, один из которых используется для указания текущей итерации, а второй служит для обозначения конца коллекции. Итераторы создаются при помощи соответствующих классов контейнеров, используя такие стандартные методы как begin() и end(). Функция begin() возвращает указатель на первый элемент, а end() — на воображаемый несуществующий элемент, следующий за последним.

Когда итератор выходит за последний элемент, то по определению это равно специальному конечному значению итератора. Нижеследующий пример демонстрирует типичное использование итератора:

```c++
std::list<int> C; // Вместо std::list можно использовать любой стандартный контейнер STL
for (std::list<int>::iterator it = C.begin(),end = C.end(); it != end; ++it) { //для изменяемого итератора
    *it = 8; // элемент, на который указывает итератор, можно изменить
}
for (std::list<int>::const_iterator it = C.begin(),end = C.end(); it != end; ++it) { //если вам не нужно изменять элементы
    std::cout << *it << std::endl;
}
```


### информацию брал тут 
[stackoverflow](https://is.gd/SV6l6N)

[вики](https://is.gd/j9WPS8)

### подробнее 
[Стандартная библиотека языка C++](https://vk.com/doc182687495_486181627?hash=c0e733e1da504d26cd&dl=5f7b94af6d86fab217) стр 219 - 225


# 3. Обработка исключений.RAII

Получение ресурса есть инициализация (англ. Resource Acquisition Is Initialization (RAII)) — программная идиома объектно-ориентированного программирования, смысл которой заключается в том, что с помощью тех или иных программных механизмов получение некоторого ресурса неразрывно совмещается с инициализацией, а освобождение — с уничтожением объекта.

Типичным (хотя и не единственным) способом реализации является организация получения доступа к ресурсу в конструкторе, а освобождения — в деструкторе соответствующего класса. Поскольку деструктор автоматической переменной вызывается при выходе её из области видимости, то ресурс гарантированно освобождается при уничтожении переменной. Это справедливо и в ситуациях, в которых возникают исключения. Это делает RAII ключевой концепцией для написания безопасного при исключениях кода в языках программирования, где конструкторы и деструкторы автоматических объектов вызываются автоматически, прежде всего — в C++.

#### подробнее 

[qa.ru](http://qaru.site/questions/7289/why-is-exception-handling-bad)

очень подробно об [обработке ошибок](http://itnotesblog.ru/note.php?id=163)

#### @WhiteRabbitRo

# 4  "Умные указатели"

1) Лекция 2 от Бородина (Все что нужно описано)
2) Джосаттис, глава 5, раздел 2 "Интеллектуальные указатели" (Тут все подробно, даже слишком подробно, но даже разобраны подводные камни)
+ http://alenacpp.blogspot.com/2016/02/c.html в копилку

```

Несколько интересных свойств умных указателей в C++
Об этом полезно знать при использовании умных указателей в С++:

У shared_ptr есть конструктор, который позволяет создавать зависимости между shared_ptr'ами. (std::shared_ptr's secret constructor  by Anthony Williams) 
Допустим, я хочу создать указатель на объект типа Y, py, который является членом экземпляра класса X, px. Мне нужно, 
чтобы px не удалялся, пока я не закончу работать с py.



void bar(){
    std::shared_ptr<X> px(std::make_shared<X>());
    std::shared_ptr<Y> py(px,&px->y);
    store_for_later(py);
} // our X object is kept alive



unique_ptr не такой уж и уникальный. (unique_ptr–How Unique is it? by Bartosz Milewski)

void f(Foo * pf) {
    globalFoo = pf; // creates a global alias
}

unique_ptr<Foo> pFoo(new Foo());
f(pFoo.get()); // leaks an alias


Передача shared_ptr по значению - дорогое удовольствие. (The Real Price of Shared Pointers in C++ by Nico Josuttis)
При передаче по значению происходит его копирование и к его внутреннему счетчику прибавляется единица, это нужно сделать атомарно, что влияет на производительность. Передавайте его по ссылке, где возможно.


Зачем нужен scoped_ptr, если есть shared_ptr. (shared_ptr vs scoped_ptr)
shared_ptr "тяжелее" чем scoped_ptr, потому что он гарантирует корректную работу  в многопоточных программах. Поэтому, 
если вы работаете с одним указателем, и вам просто нужно автоматически освободить память из-под него, лучше использовать 
scoped_ptr.


Чтобы корректно возвращать shared_ptr на this надо использовать enable_shared_from_this. (std::enable_shared_from_this на 
cppreference.com)
Пример с  cppreference.com демонстрирует что случится, если вы не используете enable_shared_from_this.


#include <memory>
#include <iostream>

struct Good: std::enable_shared_from_this<Good>
{
    std::shared_ptr<Good> getptr() {
        return shared_from_this();
    }
};
 
struct Bad
{
    std::shared_ptr<Bad> getptr() {
        return std::shared_ptr<Bad>(this);
    }
    ~Bad() { std::cout << "Bad::~Bad() called\n"; }
};
 
int main()
{
    // Good: the two shared_ptr's share the same object
    std::shared_ptr<Good> gp1(new Good);
    std::shared_ptr<Good> gp2 = gp1->getptr();
    std::cout << "gp2.use_count() = " << gp2.use_count() << '\n';
 
    // Bad, each shared_ptr thinks it's the only owner of the object
    std::shared_ptr<Bad> bp1(new Bad);
    std::shared_ptr<Bad> bp2 = bp1->getptr();
    std::cout << "bp2.use_count() = " << bp2.use_count() << '\n';
} // UB: double-delete of Bad


```

+ https://habr.com/post/140222/ кратко и понятно

```

Эта небольшая статья в первую очередь предназначена для начинающих C++ программистов, которые либо слышали об умных указателях, но боялись их применять, либо они устали следить за new-delete.

UPD: Статья писалась, когда C++11 еще не был так популярен.

Итак, программисты С++ знают, что память нужно освобождать. Желательно всегда. И они знают, что если где-то пишется new, 
обязательно должен быть соответствующий delete. Но ручные манипуляции с памятью могут быть чреваты, например, следующими 
ошибками:
утечки памяти;
разыменовывание нулевого указателя, либо обращение к неициализированной области памяти;
удаление уже удаленного объекта;

Утечка в принципе не так критична, если программа не работает 24/7, либо код, ее вызывающий, не находится в цикле. При 
разыменовывании нулевого указателя мы гарантированно получим сегфолт, осталось только найти тот случай когда он становится 
нулевым (вы же понимаете о чем я). При повторном удалении может случиться вообще все, что угодно. Обычно (хотя может быть и не 
всегда), если вам выделяется блок памяти, то где-то с ним по соседству лежит значение, определяющее количество выделенной 
памяти. Детали зависят от реализациии, но допустим, что вы выделили 1 кб памяти начиная с некоторого адреса. Тогда по 
предыдущему адресу будет храниться число 1024, таким образом станет возможным при вызове delete удалить ровно 1024 байт 
памяти, не больше и не меньше. При первом вызове delete все отлично, при втором вы потрете не те данные. Чтобы всего этого 
избежать, либо уменьшить вероятность появления подобного рода ошибок, и были придуманы умные указатели.

Введение

Существует техника управления ресурсами посредством локальных объектов, называемая RAII. То есть, при получении какого-либо 
ресурса, его инициализируют в конструкторе, а, поработав с ним в функции, корректно освобождают в деструкторе. Ресурсом может 
быть что угодно, к примеру файл, сетевое соединение, а в нашем случае блок памяти. Вот простейший пример:

class VideoBuffer {
    int *myPixels;
public:
    VideoBuffer() {
        myPixels = new int[640 * 480];
    }
    void makeFrame() { /* Работаем с растром */ }
    ~VideoBuffer() {
        delete [] myPixels;
    }
};
int game() {
    VideoBuffer screen;
    screen.makeFrame();
}

Это удобно: по выходу из функции нам не нужно заботиться об освобождении буфера, так как для объекта screen вызовется 
деструктор, который в свою очередь освободит инкапсулированный в себе массив пикселей. Конечно, можно написать и так:

int game() {
    int *myPixels = new int[640 * 480];
    // Работаем
    delete [] myPixels;
}

В принципе, никакой разницы, но представим себе такой код:

int game() {
    int *myPixels = new int[640 * 480];
    // Работаем
    if (someCondition)
        return 1;        
    // Работаем дальше
    if (someCondition)
        return 4;        
    // Поработали
    delete [] myPixels;
}

Придется в каждой ветке выхода из функции писать delete [], либо вызывать какие-либо дополнительные функции деинициализации. А 
если выделений памяти много, либо они происходят в разных частях функции? Уследить за всем этим будет все сложнее и сложнее. 
Подобная ситуация возникает, если мы в середине функции бросаем исключение: гарантируется, что объекты на стеке будут 
уничтожены, но с кучей проблема остается открытой.
Ок, будем использовать RAII, в конструкторах инициализировать память, в деструкторе освобождать. И пусть поля нашего класса 
будут указателями на участки динамической памяти:

class Foo {
    int *data1;
    double *data2;
    char *data3;
public:
    Foo() {
        data1 = new int(5);
        ...
    }
    ~Foo() {
        delete data1;
        ...
    }
}

Теперь представьте, что полей не 3, а 30, а значит в деструкторе придется для всех них вызывать delete. А если мы второпях 
добавим новое поле, но забудем его убить в деструкторе, то последствия будут негативными. В итоге получается класс, 
нагруженный операциями выделения\освобождения памяти, да еще и непонятно, все ли было правильно удалено.
Поэтому предлагается использовать умные указатели: это объекты, которые хранят указатели на динамически аллоцированные участки 
памяти произвольного типа. Причем они автоматически очищают память по выходу из области видимости.
Сначала рассмотрим то, как они выглядят в С++, затем перейдем к обзору некоторых распространенных типов умных указателей.

Простейший smart pointer

// Класс нашего умного указателя
template <typename T>
class smart_pointer {
    T *m_obj;
public:
    // Отдаем ему во владение некий объект
    smart_pointer(T *obj)
        : m_obj(obj)
    { }
    // По выходу из области видимости этот объект мы уничтожим
    ~smart_pointer() {
        delete m_obj;
    }
    // Перегруженные операторы<
    // Селектор. Позволяет обращаться к данным типа T посредством "стрелочки"
    T* operator->() { return m_obj; }
    // С помощью такого оператора мы можем разыменовать указатель и получить ссылку на
    // объект, который он хранит
    T& operator* () { return *m_obj; }
}
int test {
    // Отдаем myClass во владение умному указателю
    smart_pointer<MyClass> pMyClass(new MyClass(/*params*/);    
    // Обращаемся к методу класса MyClass посредством селектора
    pMyClass->something();    
    // Допустим, что для нашего класса есть функция вывода его в ostream
    // Эта функция одним из параметров обычно получает ссылку на объект,
    // который должен быть выведен на экран
    std::cout << *pMyClass << std::endl;    
    // по выходу из скоупа объект MyClass будет удален
}

Понятно, что наш смарт пойнтер не лишен недостатков (например, как хранить в нем массив?), но он в полной мере реализует 
идиому RAII. Он ведет себя так же, как и обычный указатель (благодаря перегруженным операторам), причем нам не нужно 
заботиться об освобождении памяти: все будет сделано автоматически. По желанию к перегруженным операторам можно добавить 
const, гарантировав неизменность данных, на которые ссылается указатель.
Теперь, если вы поняли, что получаете определенные преимущества, при использовании таких указателей, рассмотрим их конкретные 
реализации. Если вам не нравится эта идея, то все равно, попробуйте использовать их в какой-нибудь своей маленькой программке, 
уверяю, вам должно понравиться.
Итак, наши смарт-пойнтеры:
boost::scoped_ptr
std::auto_ptr
std::tr1::shared_ptr (он же std::shared_ptr в C++11, либо boost::shared_ptr из boost)


boost::scoped_ptr

Он находится в библиотеке буст.
Реализация простая и понятная, практически идентичная нашей, за несколькими исключениями, одно из них: этот пойнтер не может 
быть скопирован (то есть у него приватный конструктор копирования и оператор присваивания). Поясню на примере:
#include <boost/scoped_ptr.hpp>
int test() {
    boost::scoped_ptr<int> p1(new int(6));
    boost::scoped_ptr<int> p2(new int(1));    
    p1 = p2; // Нельзя!
}

Оно и понятно, если бы было разрешено присваивание, то и p1 и p2 будут указывать на одну и ту же область памяти. А по выходу 
из функции оба удалятся. Что будет? Никто не знает. Соответственно, этот пойнтер нельзя передавать и в функции.
Тогда зачем он нужен? Советую применять его как указатель-обертка для каких-либо данных, которые выделяются динамически в 
начале функции и удаляются в конце, чтобы избавить себя от головной боли по поводу корректной очистки ресурсов.
Подробное описание здесь.

std::auto_ptr

Чуть-чуть улучшенный вариант предыдущего, к тому же он есть в стандартной библиотеке (хотя в C++11 вроде как deprecated). У 
него есть оператор присваивания и конструктор-копировщик, но работают они несколько необычно.
Поясняю:
#include <memory>
int test() {
    std::auto_ptr<MyObject> p1(new MyObject);
    std::auto_ptr<MyObject> p2;    
    p2 = p1;
}

Теперь при присваивании в p2 будет лежать указатель на MyObject (который мы создавали для p1), а в p1 не будет ничего. То есть 
p1 теперь обнулен. Это так называемая семантика перемещения. Кстати, оператор копирования поступает таким же образом.
Зачем это нужно? Ну например у вас есть функция, которая должна создавать какой-то объект:
std::auto_ptr<MyObject> giveMeMyObject();

Это означает, что функция создает новый объект типа MyObject и отдает его вам в распоряжение. Понятней станет, если эта 
функция сама является членом класса (допустим Factory): вы уверены, что этот класс (Factory) не хранит в себе еще один 
указатель на новый объект. Объект ваш и указатель на него один.
В силу такой необычной семантики auto_ptr нельзя использовать в контейнерах STL. Но у нас есть shared_ptr.

std::shared_ptr (С++11)

Умный указатель с подсчетом ссылок. Что это значит. Это значит, что где-то есть некая переменная, которая хранит количество 
указателей, которые ссылаются на объект. Если эта переменная становится равной нулю, то объект уничтожается. Счетчик 
инкрементируется при каждом вызове либо оператора копирования либо оператора присваивания. Так же у shared_ptr есть оператор 
приведения к bool, что в итоге дает нам привычный синтаксис указателей, не заботясь об освобождении памяти.
#include <memory> // Либо <tr1/memory> для компиляторов, еще не поддерживающих C++11
#include <iostream>
int test() {
    std::shared_ptr<MyObject> p1(new MyObject);
    std::shared_ptr<MyObject> p2;    
    p2 = p1;    
    if (p2)
        std::cout << "Hello, world!\n";
}

Теперь и p2 и p1 указывают на один объект, а счетчик ссылок равен 2, По выходу из скоупа счетчик обнуляется, и объект 
уничтожается. Мы можем передавать этот указатель в функцию:
int test(std::shared_ptr<MyObject> p1) {
    // Делаем что-то
}

Заметьте, если вы передаете указатель по ссылке, то счетчик не будет увеличен. Вы должны быть уверены, что объект MyObject 
будет жив, пока будет выполняться функция test.

Итак, smart pointers это хорошо, но есть и минусы. 
Во-первых это небольшой оверхед, но я думаю у вас найдется несколько тактов процессора ради такого удобства.
Во-вторых это boiler-plate, например 
std::tr1::shared_ptr<MyNamespace::Object> ptr = std::tr1::shared_ptr<MyNamespace::Object>(new MyNamespace::Object(param1, 
param2, param3))

Это частично можно решить при помощи дефайнов, допустим:
#define sptr(T) std::tr1::shared_ptr<T>

Либо при помощи typedef. 
В-третьих, существует проблема циклических ссылок. Рассматривать ее здесь не буду, чтобы не увеличивать статью. Так же 
остались нерассмотренными boost::weak_ptr, boost::intrusive_ptr и указатели для массивов.
Кстати, smart pointers достаточно хорошо описаны у Джеффа Элджера в книге «С++ for real programmers».
Теги:
c++
smart pointers
memory leaks
умные указатели
управление памятью


```

# 5 "Разработка обобщенных типов: шаблоны С++"
1) Прата, глава 14 (Подробно, все что нужно знать)
2) Джосаттис "Шаблоны С++", Часть 1 (Тут очень подробно, но самое важное в первой части)

# 6: "Парадигмы ООП"
1) http://www.codenet.ru/progr/cpp/ipn.php (Теория)
2) Прата. Глава 8. Перегрузка функций + Шаблоны функций (Немного больше о полиморфизме и про шаблоны функций к 5ому вопросу)
3) Прата. Глава 10. Классы С++. Управление доступом (Немного больше об инкапсуляции)
4) Прата. Глава 13. Наследование классов (Все очень подробно про наследование, можно прочитать резюме в конце, там кратко о главном)
5) Прата. Глава 14. Закрытое и защищенное наследование + Множественное наследование (Еще больше о наследовании)

# 7: "Нововведения С++11, С++14, С++17"
1) Лекция 1 от Бородина (немного затронута тема)
+ https://habr.com/post/182920/ (С++11)
+ https://habr.com/company/piter/blog/345560/ (С++17)
+ https://habr.com/post/184606/ (С++14 Ч.1)
+ https://habr.com/post/198238/ (С++14 Ч.2)
Собственно все лекции Бородина так или иначе о новых фишках С++ с 11ого

#### @AlexDeveloper24

8. Лямбда-функции, функторы, указатели на функции, std::functional
Для базового понимания данных вещей:
https://purecodecpp.com/archives/3448
https://habr.com/post/66021/
https://metanit.com/cpp/tutorial/4.8.php
https://ru.cppreference.com/w/cpp/utility/functional/function

Если кому проще воспринимать на видео(все подробнейшим образом объясняется)
https://www.youtube.com/watch?v=uzZw7VzZj5E
https://www.youtube.com/watch?v=_6eG9Q40lFM
https://www.youtube.com/watch?v=Bm2jmUxkUVw

Для более детального погружения в тему:
лямбда-функции стр.534(раздел 10.3)
функторы стр.513 (раздел 10.1)
std::functional стр.163 (раздел 5.4.4)

9. Rvalue ссылки, семантика перемещения, std::move
семантика перемещения и rvalue-ссылки стр.43(раздел 3.1.5)
Краткие сведения о rvalue и move:
https://habr.com/post/226229/
Более подробные сведения об перемещении:
https://habr.com/post/322132/

10. Универсальные ссылки, прямая передача и std::forward
Статья про универсальные ссылки и прямую передачу:
https://habr.com/post/242639/
std::forward:
https://www.youtube.com/watch?v=N4treTtmy94&t=734s
https://stackoverflow.com/questions/8526598/how-does-..

11. Перегрузка new и delete. Аллокаторы, системы управления памятью
Перегрузка new, delete:
http://www.amse.ru/courses/cpp2/2011_03_21.html
https://habr.com/post/185662/

Управление памятью:
https://habr.com/post/148657/

Статья по аллокаторам:
https://habr.com/post/274827/

Краткое описание аллокаторов на toster`е:
https://toster.ru/q/332274 (ред.)
 
Больше направлено на базовое понимание и знакомство, чем на детальное изучение всех тонкостей
 
книга откуда можно взять помеченные мною разделы

#### @yokkidack

16. Атомарные операции

Операция в общей области памяти называется атомарной, если она завершается в 
один шаг относительно других потоков, имеющих доступ к этой памяти. Во время
выполнения такой операции над переменной, ни один поток не может наблюдать 
изменение наполовину завершенным. 

Атомарный обьект - это такой обьект,операции над которым можно считать 
неделимыми, тюею такими, которые не могут быть прерваны или результат которых
не может быть получен до окончания операции.

В С++11 добавлено два типа атомарных обьектов:

std::atomic<T>
std::atomic_flag
Было упомянуто в лекции
https://github.com/bmstu-iu8-cpp/cpp-upper-intermediate/blob/master/cpp17/lectures/05_synchronization/synchronization.pdf
  
bmstu-iu8-cpp/cpp-upper-intermediate
github.com
Инфы не сильно больше, но я еще ищу

Страница 163. Атомарные операторы

#### @BroNaz

# 17. Управление потоками. Data race. Классы std::future, std::promise, std::packaged_task, функция std::async, std::condition_variable

Информация тут:

[лекция Бородина](https://github.com/bmstu-iu8-cpp/cpp-upper-intermediate/blob/master/cpp18/lectures/04_multithreads/multithreading.pdf)

[Стандартная библиотека языка C++](https://vk.com/doc182687495_486181627?hash=c0e733e1da504d26cd&dl=5f7b94af6d86fab217) стр 967 - 1047 ( вся 18 глава ) 

[ ПРИЛОЖЕНИЕ D.](https://psv4.userapi.com/c848124/u467983419/docs/d3/860053a31a6e/C__Parallelnoe_programmirovanie_-_Entoni_Uilyams_2012.pdf?extra=XbhmNPTgA_fWX9i1UwnNEpsC7SEbT1Au-d4Z5EL4nIFON0ijMyl8rdDKztjdcsq0QOz04PvwxOEuYiaZw4tFMmPmzUz6QtD6sMNOXsx4Lv_I6nDVb6Th3tN6c7X4vEJkZtwEImKXmBNqEt-HfnioCJ-jjA#%5B%7B%22num%22%3A498%2C%22gen%22%3A0%7D%2C%7B%22name%22%3A%22XYZ%22%7D%2C2.65%2C297.96%2Cnull%5D) книги Параллельное программирование на C++ в действии

[сравнение packaged_task и async](http://qaru.site/questions/69252/what-is-the-difference-between-packagedtask-and-async)

[про std::promise и когда его использовать(тупой перевод с ангельского, но если в теме то все понятно)](http://qaru.site/questions/249324/when-to-use-promise-over-async-or-packagedtask)

если все плохо и не шаришь за потоки, то тебе [сюда](https://habr.com/post/182610/), а потом [сюда](https://habr.com/post/182626/) 

#### @Kutyirov

# 18-21
# Вместо предисловия
Копал несколько часов в инете по данным вопросам, просмотрел достаточное количество статей, но вынужден признать, что книга параллельное программирование отвечает на данные вопросы наиболее полно. В лекциях Бородина эти вопросы также только упоминаются.
# Пул потоков

Итак если кратко, то простейший пул потоков представляет из себя потокобезопасную очередь потоков, каждый из которых запускается в конструкторе и затем выполняет некоторую функцию. В коде важен порядок объявления: флаг и объект должны быть объявлены до вектора потоков, который должен быть объявлен ранее joinera.
Страница 383 из параллельного программирования

Но данный пул потоков не поддерживает многие функции такие как ожидание задачи или предотвращение конкуренции потоков. Усложненные варианты написаны в следующих пунктах. Их можно посмотреть по диагонали, но чтобы разобраться потребуется несколько часов, поэтому запоминайте, что пул из листинга 9.1 очень не идеален, но реализация всех этих функций займет ОЧЕНЬ МНОГО времени
# Потокобезопасные стуктуры данных с блокировками
Для ответа на данный вопрос рекомендуется прочитать главу 6 (6.1, 6.2 полностью прочитать и понять, 6.3 наискось и на будущее запомнить, что такое тоже бывает)

# Реализация потокобезопасной очереди с блокировкой.
В этих пунктах на мой взгляд все довольно просто
читаем пункт 6.2.1 если на словах "скопируем код из главы 3" вы ипытываете ненависть, то возвращаемся и читаем страницы 81-83, начиная с листинга 3.5
# Реализация потокобезопасного стека с блокировкой.
пункт 6.2.2 нас интересует листинг 6.3 на странице 229 и все комментарии ниже до пункта 6.2.3. Если код в принципе понятен, но непонятны логические решения, то читаем данный пункт сначала(итоговый код это результат усовершенствования листингов 6.1 и 6.2) если вообще код не понятен, то смотри страницу 119 листинг 4.5 и раньше(хотя после разбора стека там особо новых логических ходов нет)

#### @yokkidack

# 22. Сетевое взаимодействие. Berkley sockets. boost asio
Сетевое взаимодействие 
https://github.com/bmstu-iu8-cpp/cpp-upper-intermediate/blob/master/cpp17/lectures/06_networks/networks.pdf
  
bmstu-iu8-cpp/cpp-upper-intermediate
github.com
Berkley sockets - тут есть примеры с кодом
https://en.wikipedia.org/wiki/Berkeley_sockets
  
Berkeley sockets - Wikipedia
en.wikipedia.org
https://ru.wikipedia.org/wiki/Сокеты_Беркли на русском подробно, но немного меньше, тоже с примерами, написано хорошо
  
Сокеты Беркли — Википедия
ru.wikipedia.org
boost asio
https://habr.com/sandbox/101087/ (Boost.Asio C++ Tutorial)
  
Boost.Asio C++ Tutorial / Песочница / Хабр
habr.com
https://www.boost.org/doc/libs/1_60_0/doc/html/boost_asio/tutorial.html (мануал от буста, но чтение не из приятных)
Tutorial - 1.60.0
www.boost.org
https://habr.com/post/192284/ (про Boost.Asio подробно)


«Boost.Asio C++ Network Programming». Глава 1: Приступая к работе с Boost.Asio
habr.com

# 23.

23. Шаблоны проектирования: фабрика, singleton, Pimp, итератор и др
В книге выделены цветом куски про каждый из паттернов

В книге описаны и другие паттерны проектирования, книгу рекомендовали на типме.

[pimp](http://qaru.site/questions/1929325/pimp-my-library-pattern-applied-to-class-hierarchy)


Первый подход: - недостаточно в соответствии с OP -

Это будет сделано, если предположить, что одна реализация foo соответствует всем классам вашей иерархии:

~~~

sealed abstract class A
case class B() extends A
case class C() extends A

class RichA(a: A) {
  def foo() { println(this.a.getClass.getSimpleName) }
}

implicit def a2RichA(a: A): RichA = new RichA(a)

(new C).foo() /* anon$1$C */

~~~

Второй подход: - отсутствует динамическая отправка -

Мой второй подход был вдохновлен внутренними структурами библиотеки Scala. Однако ему не хватает динамической отправки, поэтому он все еще не решает вашу проблему.

~~~

sealed abstract class A
case class B() extends A
case class C() extends A

abstract class RichA(a: A) {
  def foo(): Unit
}

class RichB(b: B) extends RichA(b) {
  def foo() { println("Doing B-specific stuff") }
}

class RichC(c: C) extends RichA(c) {
  def foo() { println("Doing C-specific stuff") }
}

sealed trait RichBuilder[T <: A] {
  def apply(t: T): RichA
}

implicit object RichB extends RichBuilder[B] {
  def apply(b: B) = new RichB(b)
}

implicit object RichC extends RichBuilder[C] {
  def apply(c: C) = new RichC(c)
}

implicit def a2RichA[T <: A](t: T)
                            (implicit rb: RichBuilder[T])
                            : RichA = {

  rb(t)
}

(new B).foo() /* B-specific */
(new C).foo() /* C-specific */
// (new C).asInstanceOf[A].foo() /* ERROR: Can't find an implicit */

~~~

Требования:

Если вам требуется поведение, зависящее от типа среды выполнения, есть две возможности, которые я могу увидеть:

Соответствие шаблону
Динамическая рассылка
Соответствие шаблону, используемое в вашем исходном коде, похоже, приводит к ситуации, когда у вас есть одно место в коде, в 
котором выполняется сопоставление. Следовательно, расширения вашей иерархии классов влекут за собой изменения в этом месте - 
что может быть невозможно, например, если иерархия расширена клиентами.

Динамическая диспетчеризация не страдает от этого недостатка, что может быть причиной того, почему этот подход используется в 
коллекции Scala (это кратко упоминается в статье). Таким образом, вы можете попытаться использовать двойную отправку (см. 
шаблон посетителя). Однако это имеет тот недостаток, что базовый класс A должен уже объявить соответствующий метод - который 
несколько поражает цель Pimp My Library Pattern. Scala 2.10s новая функция Dynamic может быть полезной, но из-за отсутствия 
опыта я не могу комментировать это.


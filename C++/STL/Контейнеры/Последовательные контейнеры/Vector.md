vector — коллекция элементов, сохраненных в массиве, изменяющегося по мере необходимости размера (обычно, увеличивающегося);

vector - реализует динамический массив. 
Размер вектора — это фактическое число элементов, а объём — количество используемой им памяти. 
Если при вставке в вектор новых элементов, его размер становится больше его объёма, происходит перераспределение памяти. Как правило, это приводит к тому, что вектор выделяет новую область хранения, перемещая элементы и свободные старые области в новый участок памяти. 
Поскольку адреса элементов в течение этого процесса меняются, любые ссылки или итераторы элементов в векторе могут стать недействительными. Использование недействительных ссылок приводит к неопределённому поведению.

устройство вектора:

Выделаяет память в куче. 
Хранит указатели на начало данных, конец данных и следующую ячейку памяти после выделенной под вектор.
Объект в заранее аллоцированной памяти создается с помощью конструкции [placement new](https://www.geeksforgeeks.org/placement-new-operator-cpp/). 
А начиная с C++11 с вводом perfect [forwarding](https://ru.wikipedia.org/wiki/%D0%9F%D1%80%D1%8F%D0%BC%D0%B0%D1%8F_%D0%BF%D0%B5%D1%80%D0%B5%D0%B4%D0%B0%D1%87%D0%B0_(C%2B%2B)) новый объект для вектора можно создавать in-place (с помощью метода emplace/emplace_back)

.size() - количество объяектов в векторе.  
.capacity() - под какое количество объектов зарезервированна память.

![устройство вектора](images/vector_1.png)

вставка нового элемента:

![вставка нового элемента](images/vector_2.png)

вставка нового элемента, в случае когда размер становится больше объема:

при нехватке места ветор увеличивается в 2 раза.

![вставка нового элемента, в случае когда размер становится больше объема](images/vector_3.png)
Это однонаправленный список - самая простая реализация списка. Список состоит из вершин.
Вершина списка это сам объект и указатель на следующую вершину (указатель принимает значение nullptr, если объект последний в списке).

Контейнер поддерживает быструю вставку и удаление объектов в любом месте, потому что для этого понадобится только правка next_ptr у вершины слева.
Впрочем, "быстрая вставка" относится исключительно к алгоритмической сложности.
Aллокация памяти для новой вершины может быть небыстрой.

Быстро получить N-й объект нельзя, для этого нужно пройтись от корневой вершины по next_ptr N раз.
Размер списка тоже можно узнать только пройдя по всем next_ptr, пока не увидим nullptr.

У контейнера даже нет метода .size().

![устройство forward_list](images/forward_list_1.png)
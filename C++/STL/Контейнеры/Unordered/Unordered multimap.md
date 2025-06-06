Unordered Multimap - это ассоциативный контейнер, который хранит элементы, состоящие из комбинации ключевого значения и отображаемого значения, подобно неупорядоченному отображению (unordered_map), но позволяющий различным элементам иметь эквивалентные ключи.

В unordered_multimap ключевое значение обычно используется для уникальной идентификации элемента, в то время как отображаемое значение является объектом, содержащим связанное с этим ключом содержимое. Типы ключа и отображаемого значения могут отличаться.

Внутренне элементы в unordered_multimap не отсортированы по какому-либо определенному порядку ни по ключу, ни по отображаемым значениям, но они организованы в корзины (buckets) в зависимости от их хэш-значений, что позволяет быстро получать отдельные элементы напрямую по их ключевым значениям (с постоянной средней сложностью по времени).

Элементы с эквивалентными ключами группируются в одну корзину и таким образом, что итератор (см. equal_range) может перебирать их все.

Итераторы в контейнере являются по крайней мере прямыми итераторами (forward iterators).

Обратите внимание, что этот контейнер не определен в своем собственном заголовочном файле, но использует заголовочный файл <unordered_map> вместе с неупорядоченным отображением (unordered_map).
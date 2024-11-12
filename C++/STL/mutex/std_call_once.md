Выполняет код, один раз, под мьютексом. Может принимать std::bind

```c++
std::once_flag init_flag;

std::call_once(init_flag,fun);
std::call_once(init_flag,&X::fun, this);
```
```cmake
project(hello_world)			# Название проекта

set(SOURCE_EXE main.cpp)		# Установка переменной со списком исходников для исполняемого файла

set(SOURCE_LIB foo.cpp)			# Тоже самое, но для библиотеки

add_library(foo STATIC ${SOURCE_LIB})	# Создание статической библиотеки с именем foo

add_executable(main ${SOURCE_EXE})	# Создает исполняемый файл с именем main

target_link_libraries(main foo)		# Линковка программы с библиотекой
```

Переменные могут хранить списки значений, разделённых пробелами\табуляциями\переносами:
```cmake
set(SOURCE main.cpp foo.cpp)
set(HEADER main.h
			foo.h)
```

Что бы получить значение переменной ипользуем конструкцию:
```cmake
${var_name}
```
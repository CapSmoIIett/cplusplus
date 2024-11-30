
CMake обладает достаточно развитыми средствами поиска установленых библиотек, правда они не встроеные, а реализованы в виде отдельных модулей. 
В стандартной поставке довольно много модулей, но некоторые проекты (например Ogre) поставляют свои. 
Они позволяют системе автоматически определить наличие необходимых для линковки проекта библиотек.

#### Поиск библиотеки
Если в системе её нет, выведется сообщение об ошибке и завершается выполнение cmake.
```cmake
find_package(SDL REQUIRED)
if(NOT SDL_FOUND)
	message(SEND_ERROR "Failed to find SDL")
	return()
else()
	include_directories(${SDL_INCLUDE_DIR})
endif()
```

Поиск необходимого компонента
```cmake
find_package(Boost COMPONENTS thread-mt REQUIRED)
if(NOT Boost_FOUND)
	message(SEND_ERROR "Failed to find boost::thread-mt.")
	return()
else()
	include_directories(${Boost_INCLUDE_DIRS})
endif()
```
SDL_FOUND, Boost_FOUND — признак присутствия бибилиотеки;  
SDL_LIBRARY, Boost_LIBRARIES — имена библиотек для линковки;  
SDL_INCLUDE_DIR, Boost_INCLUDE_DIRS — пути к заголовочным файлам.  
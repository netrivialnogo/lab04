**Задание 1**
Вам поручили перейти на систему автоматизированной сборки **CMake**. Исходные файлы находятся в директории [formatter_lib](https://github.com/tp-labs/lab03/blob/master/formatter_lib). В этой директории находятся файлы для статической библиотеки _formatter_. Создайте `CMakeList.txt` в директории [formatter_lib](https://github.com/tp-labs/lab03/blob/master/formatter_lib), с помощью которого можно будет собирать статическую библиотеку _formatter_.

    mkdir lab03
    git clone https://github.com/tp-labs/lab03.git lab03
    Клонирование в «lab03»...
    remote: Enumerating objects: 91, done.
    remote: Counting objects: 100% (30/30), done.
    remote: Compressing objects: 100% (9/9), done.
    remote: Total 91 (delta 23), reused 21 (delta 21), pack-reused 61 (from 1)
    Получение объектов: 100% (91/91), 1.02 МиБ | 1.41 МиБ/с, готово.
    Определение изменений: 100% (41/41), готово.
    cd lab03/formatter_lib
    nano CMakeLists.txt
    cmake_minimum_required(VERSION 3.4)
    set(CMAKE_CXX_STANDARD 11)
    set(CMAKE_CXX_STANDARD_REQUIRED ON)
    project(formatter_lib)
    add_library(formatter STATIC formatter.cpp)
	target_include_directories(formatter PUBLIC ${CMAKE_CURRENT_SOURCE_DIR})
    

**Задание 2**

[](https://gist.github.com/Kiril207/59c3bdaf8b2fc51d39886346d0fab174#задание-2)

У компании "Formatter Inc." есть перспективная библиотека, которая является расширением предыдущей библиотеки. Т.к. вы уже овладели навыком созданием `CMakeList.txt` для статической библиотеки _formatter_, ваш руководитель поручает заняться созданием `CMakeList.txt` для библиотеки _formatter_ex_, которая в свою очередь использует библиотеку _formatter_.

    cd ~/lab03/formatter_ex_lib
    
    nano CMakeLists.txt
    
    cmake_minimum_required(VERSION 3.4)
    set(CMAKE_CXX_STANDARD 11)
    set(CMAKE_CXX_STANDARD_REQUIRED ON)
    project(formatter_ex_lib)
    add_library(formatter_ex STATIC formatter_ex.cpp)
    target_include_directories(formatter_ex PUBLIC ${CMAKE_CURRENT_SOURCE_DIR})
    target_link_libraries(formatter_ex PUBLIC formatter)

## Задание 3

Конечно же ваша компания предоставляет примеры использования своих библиотек. Чтобы продемонстрировать как работать с библиотекой _formatter_ex_, вам необходимо создать два `CMakeList.txt` для двух простых приложений:

 _hello_world_, которое использует библиотеку _formatter_ex_;
_solver_, приложение которое испольует статические библиотеки _formatter_ex_ и _solver_lib_.

    cd ~/lab03/hello_world_application
    nano CMakeLists.txt
    cmake_minimum_required(VERSION 3.4)
    set(CMAKE_CXX_STANDARD 11)
    set(CMAKE_CXX_STANDARD_REQUIRED ON)
    project(hello_world)
    add_executable(hello_world hello_world.cpp)
    target_link_libraries(hello_world PRIVATE formatter_ex)
    cd ..
    cd solver_application
    nano CMakeLists.txt
    cmake_minimum_required(VERSION 3.4)
    set(CMAKE_CXX_STANDARD 11)
    set(CMAKE_CXX_STANDARD_REQUIRED ON)
    project(solver_application)
    add_executable(solver equation.cpp)
    target_link_libraries(solver PRIVATE formatter_ex solver_lib)
    cd ..
    cd solver_lib
    nano CMakeLists.txt
    cmake_minimum_required(VERSION 3.4)
    set(CMAKE_CXX_STANDARD 11)
    set(CMAKE_CXX_STANDARD_REQUIRED ON)
    project(solver_lib)
    add_library(solver_lib STATIC solver.cpp)
    target_include_directories(solver_lib PUBLIC ${CMAKE_CURRENT_SOURCE_DIR})
    cd ..
    nano CMakeLists.txt
    cmake_minimum_required(VERSION 3.4)
    set(CMAKE_CXX_STANDARD 11)
    set(CMAKE_CXX_STANDARD_REQUIRED ON)
    project(formatter_project) 
    add_subdirectory(formatter_lib)
    add_subdirectory(formatter_ex_lib)
    add_subdirectory(solver_lib)
    add_subdirectory(hello_world_application)
    add_subdirectory(solver_application)

## Проверяем

    mkdir build
    cd build
    cmake ..
    CMake Deprecation Warning at CMakeLists.txt:1 (cmake_minimum_required):
    Compatibility with CMake < 3.5 will be removed from a future version of
    CMake.
    
    Update the VERSION argument <min> value or use a ...<max> suffix to tell
    CMake that the project does not need compatibility with older versions.
    CMake Deprecation Warning at formatter_lib/CMakeLists.txt:1 (cmake_minimum_required):
    Compatibility with CMake < 3.5 will be removed from a future version of
    CMake.
    
    Update the VERSION argument <min> value or use a ...<max> suffix to tell
    CMake that the project does not need compatibility with older versions.
    
    CMake Deprecation Warning at formatter_ex_lib/CMakeLists.txt:1 (cmake_minimum_required):
    Compatibility with CMake < 3.5 will be removed from a future version of
    CMake.
    
    Update the VERSION argument <min> value or use a ...<max> suffix to tell
    CMake that the project does not need compatibility with older versions.
    
    
    CMake Deprecation Warning at solver_lib/CMakeLists.txt:1 (cmake_minimum_required):
    Compatibility with CMake < 3.5 will be removed from a future version of
    CMake.
    
    Update the VERSION argument <min> value or use a ...<max> suffix to tell
    CMake that the project does not need compatibility with older versions.
    
    
    CMake Deprecation Warning at hello_world_application/CMakeLists.txt:1 (cmake_minimum_required):
    Compatibility with CMake < 3.5 will be removed from a future version of
    CMake.
    
    Update the VERSION argument <min> value or use a ...<max> suffix to tell
    CMake that the project does not need compatibility with older versions.
    
    
    CMake Deprecation Warning at solver_application/CMakeLists.txt:1 (cmake_minimum_required):
    Compatibility with CMake < 3.5 will be removed from a future version of
    CMake.
    
    Update the VERSION argument <min> value or use a ...<max> suffix to tell
    CMake that the project does not need compatibility with older versions.
    
    
    -- Configuring done (0.0s)
    -- Generating done (0.0s)
    -- Build files have been written to: /home/netrivialnogo/lab03/build


cmake_minimum_required(VERSION 3.5)  # Указываем минимальную версию CMake, необходимую для сборки проекта.
set(CMAKE_CXX_STANDARD 17)  # Устанавливаем стандарт C++ 17.

project(PrototypePattern)  # Задаем название проекта.

option(BUILD_TESTS "Build tests" OFF)  # Опция для сборки тестов. По умолчанию выключена.
option(BUILD_DEMO "Build demo" ON)     # Опция для сборки демо. По умолчанию включена.

add_executable(PrototypePattern prototype/Prototype.cpp
                                prototype/Prototype.hpp
                                prototype/Client.cpp
                                prototype/Client.hpp)  # Создаем исполняемый файл.

if(BUILD_TESTS)
  enable_testing()  # Включаем поддержку тестирования.
  file(GLOB ${PROJECT_NAME}_TEST_SOURCES tests/*.cpp)  # Получаем исходные файлы тестов.
  add_subdirectory(third-party/gtest) # Добавляем библиотеку Google Test
  add_executable(ProtoTests ${${PROJECT_NAME}_TEST_SOURCES})  # Создаем исполняемый файл для тестов.
  target_link_libraries(ProtoTests gtest_main)  # Линкуем библиотеки для тестов.
  add_test(NAME ProtoTests COMMAND ProtoTests)  # Добавляем команду для запуска тестов.
endif()

if(BUILD_DEMO)
  add_executable(PrototypePatternDemo demo/main.cpp) # Получаем исходные демо тестов.
endif()

cmake_minimum_required(VERSION 3.14)
project(MQL5X)

set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

# Установочные пути (в билде)
set(MQL5_INCLUDE_DIR "${CMAKE_BINARY_DIR}/MQL5/Include")
set(CPP_INCLUDE_DIR "${CMAKE_BINARY_DIR}/include")
set(CPP_SRC_DIR     "${CMAKE_BINARY_DIR}/src")
set(CPP_LIB_DIR     "${CMAKE_BINARY_DIR}/lib")

# Добавить внешние зависимости
add_subdirectory(external)
add_subdirectory(MQL5)



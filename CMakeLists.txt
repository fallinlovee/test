cmake_minimum_required(VERSION 3.22)

project(oop_project VERSION 1.0)

set(CMAKE_CXX_STANDARD 17)

set(-DCMAKE_EXPORT_COMPILE_COMMANDS=ON)

set(CMAKE_CXX_CLANG_TIDY 
clang-tidy;   

-header-filter=.;
-checks='-*,cppcoreguidelines-*,google-*,modernize-*,readability-*,-modernize-use-trailing-return-type,bugprone-*,clang-analyzer-*;
#-warnings-as-errors=*;
-p=./build;
)

add_subdirectory(source_code)

add_executable(oop_project main.cpp)
target_link_libraries(oop_project PRIVATE Date)
target_link_libraries(oop_project PRIVATE Student)
target_link_libraries(oop_project PRIVATE Research)

add_library(Date
    include/date.hpp
    src/date.cpp
    )

add_library(Student
    include/human.hpp
    src/human.cpp
    include/student.hpp
    src/student.cpp
)

add_library(Research
    include/publication.hpp
    src/publication.cpp
    include/research.hpp
    src/research.cpp
)

target_include_directories(Date PUBLIC "${CMAKE_CURRENT_SOURCE_DIR}/include")
target_include_directories(Student PUBLIC "${CMAKE_CURRENT_SOURCE_DIR}/include")
target_include_directories(Research PUBLIC "${CMAKE_CURRENT_SOURCE_DIR}/include")

target_link_libraries(Student PRIVATE Date)
target_link_libraries(Research PRIVATE Student)



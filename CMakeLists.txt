cmake_minimum_required(VERSION 3.24)
project(qsqlmysql)

set(CMAKE_CXX_STANDARD 17)

# 自动把ui转换为c++代码
# uic qtcmake.ui > ui_qtcmake.h
set(CMAKE_AUTOUIC ON)

# 自动生成资源文件代码 rcc > .h
set(CMAKE_AUTORCC ON) 

# 自动生成信号槽代码
set(CMAKE_AUTOMOC ON)

set(Qt5_DIR ${QT5}/lib/cmake/Qt5)


add_definitions(
    -D_WINDOWS
    -DUNICODE
    -D_UNICODE
    -DWIN32
    -D_ENABLE_EXTENDED_ALIGNED_STORAGE
    -DWIN64
    -DQT_NO_LINKED_LIST 
    -DQT_NO_JAVA_STYLE_ITERATORS 
    -DQT_DEPRECATED_WARNINGS 
    -DQT_NO_NARROWING_CONVERSIONS_IN_CONNECT 
    -DQT_NO_CAST_TO_ASCII 
    -DQT_NO_CAST_FROM_ASCII 
    -DQT_NO_EXCEPTIONS
    -DQT_PLUGIN
    )

    
find_package(Qt5 COMPONENTS  Core Sql REQUIRED)

include_directories(
    ${CMAKE_CURRENT_SOURCE_DIR}/include
    ${QT5}/include/QtSql/5.15.2
    ${QT5}/include/QtCore/5.15.2
    )

file(GLOB SOURCE "*.cpp" "*.c"  "*.cc")
file(GLOB HEAD "*.h" "*.hpp")
file(GLOB QT "*.qrc" "*.ui" "*.rc")




LINK_DIRECTORIES(${CMAKE_CURRENT_SOURCE_DIR}/lib)

set(CMAKE_DEBUG_POSTFIX "d")
        
add_library(${PROJECT_NAME} SHARED 
    ${SOURCE}
    ${HEAD}
    ${QT}
)

target_link_libraries(${PROJECT_NAME} 
        PRIVATE
        Qt5::Core
        Qt5::Sql
        libmysql
        )




        



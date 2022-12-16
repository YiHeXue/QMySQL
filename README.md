# QMySQL
VS19 下编译Qt5.15.2的MySQL驱动  win10 

执行命令

 cmake  -S . -B build  -DQT5=D:/Qt/5.15.2/msvc2019_64 

Debug 编译
 cmake  --build build 

Release 编译
 cmake  --build build --config Release
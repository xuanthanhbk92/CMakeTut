# Use SHARED library
#add_library(MyLib SHARED chao.c)
add_library(MyLib chao.c)
# set version to create libMyLib.so.1.0.1
#set_target_properties(MyLib PROPERTIES VERSION "1.0.1")
# set so version libMyLib.so.1 will be a symlink to libmylib.so.1.0.1
#set_target_properties(MyLib PROPERTIES SOVERSION 1)
install (TARGETS MyLib DESTINATION bin)
install (FILES chao.h DESTINATION include)


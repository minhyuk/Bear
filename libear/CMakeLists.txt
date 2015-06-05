include(CheckFunctionExists)
include(CheckSymbolExists)
check_function_exists(execve HAVE_EXECVE)
check_function_exists(execv HAVE_EXECV)
check_function_exists(execvpe HAVE_EXECVPE)
check_function_exists(execvp HAVE_EXECVP)
check_function_exists(execvP HAVE_EXECVP2)
check_function_exists(execl HAVE_EXECL)
check_function_exists(execlp HAVE_EXECLP)
check_function_exists(execle HAVE_EXECLE)
#check_function_exists(fopen HAVE_FOPEN)
#check_function_exists(open HAVE_OPEN)
check_function_exists(posix_spawn HAVE_POSIX_SPAWN)
check_function_exists(posix_spawnp HAVE_POSIX_SPAWNP)
check_symbol_exists(_NSGetEnviron crt_externs.h HAVE_NSGETENVIRON)

configure_file(${CMAKE_CURRENT_SOURCE_DIR}/config.h.in ${CMAKE_CURRENT_BINARY_DIR}/config.h)
include_directories(${CMAKE_CURRENT_BINARY_DIR})

set(ORIG_CFLAG "${CMAKE_C_FLAGS}")

#set(CMAKE_C_FLAGS "${ORIG_CFLAG} -m32")
#set(CMAKE_SHARED_LINKER_FLAGS, "${CMAKE_SHARED_LINKER_FLAGS} -m32")
add_library(ear_lib SHARED ear.c)
set_target_properties(ear_lib PROPERTIES COMPILE_FLAGS "-m32")
target_link_libraries(ear_lib ${CMAKE_DL_LIBS})
set_target_properties(ear_lib PROPERTIES LINK_FLAGS "-m32")

#set(CMAKE_C_FLAGS "${ORIG_CFLAG} -m64")
#set(CMAKE_SHARED_LINKER_FLAGS, "${CMAKE_SHARED_LINKER_FLAGS} -m64")

add_library(ear_lib64 SHARED ear.c)
set_target_properties(ear_lib64 PROPERTIES COMPILE_FLAGS "-m64")
target_link_libraries(ear_lib64 ${CMAKE_DL_LIBS})
set_target_properties(ear_lib64 PROPERTIES LINK_FLAGS "-m64")

include(GNUInstallDirs)
install(TARGETS ear_lib
    LIBRARY DESTINATION ${CMAKE_INSTALL_LIBDIR})

install(TARGETS ear_lib64
    LIBRARY DESTINATION ${CMAKE_INSTALL_LIBDIR})


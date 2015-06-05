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
check_function_exists(posix_spawn HAVE_POSIX_SPAWN)
check_function_exists(posix_spawnp HAVE_POSIX_SPAWNP)
check_symbol_exists(_NSGetEnviron crt_externs.h HAVE_NSGETENVIRON)

configure_file(${CMAKE_CURRENT_SOURCE_DIR}/../config.h.in ${CMAKE_CURRENT_BINARY_DIR}/config.h)
include_directories(${CMAKE_CURRENT_BINARY_DIR})

set(ORIG_CFLAG "${CMAKE_C_FLAGS}")

add_library(ear64 SHARED ../ear.c)
set_target_properties(ear64 PROPERTIES COMPILE_FLAGS "-m64")
target_link_libraries(ear64 ${CMAKE_DL_LIBS})
set_target_properties(ear64 PROPERTIES LINK_FLAGS "-m64")
set_target_properties(ear64 PROPERTIES OUTPUT_NAME ear)

include(GNUInstallDirs)
install(TARGETS ear64
    LIBRARY DESTINATION ${CMAKE_INSTALL_LIBDIR})


cmake_minimum_required(VERSION 3.10.0)
project(bug_fmt VERSION 0.1.0 LANGUAGES C CXX)


add_subdirectory(fmt)
add_subdirectory(spdlog)

add_executable(bug_fmt main.cpp sysutilsX.cpp)
target_link_libraries(bug_fmt PRIVATE fmt::fmt spdlog::spdlog  )


  
target_compile_options(
    # -Wno-unknown-pragmas bo According to the GCC manpage -Wall turns on -Wunknown-pragmas for you, so just manually disable it using -Wno-unknown-pragmas after -Wall.
    bug_fmt PRIVATE $<$<COMPILE_LANG_AND_ID:CXX,Clang,AppleClang>:-Wall -Wextra -Werror -pedantic -fPIC -Werror=return-type -Wno-unknown-pragmas -Wno-error=deprecated-declarations> # -O3 -Werror
                PRIVATE $<$<COMPILE_LANG_AND_ID:CXX,GNU>:                 -Wall -Wextra                   -fPIC -Werror=return-type -Wno-unknown-pragmas -Wno-error=deprecated-declarations> # -O3 -Werror
                PRIVATE $<$<COMPILE_LANG_AND_ID:CXX,MSVC>: >  ) 
cmake_minimum_required(VERSION 3.15)
project(main CXX)

# Set C++ standard
set(CMAKE_CXX_STANDARD 20)
set(CMAKE_CXX_STANDARD_REQUIRED ON)
set(CMAKE_CXX_EXTENSIONS OFF)
set(CMAKE_CXX_COMPILER_ID "GNU")
set(CMAKE_CXX_COMPILER_VERSION "15.2.0")

# Add compiler warnings (-Wall -Wextra)
if(MSVC)
    add_compile_options(/W4)
else()
    add_compile_options(-Wall -Wextra)
endif()

# 1. Find needed packages
find_package(Curses REQUIRED)

# 2. Gather C++ source files
file(GLOB_RECURSE SRCS
    "./src/*.cpp"
)

# 3. Create executable target
add_executable(main ${SRCS})

# 4. Link yaml-cpp library target
target_link_libraries(main PRIVATE ${CURSES_LIBRARIES})
target_include_directories(main PRIVATE ${CURSES_INCLUDE_DIRS})

# 5. Output binary to ../bin directory
set_target_properties(main PROPERTIES
    RUNTIME_OUTPUT_DIRECTORY "${CMAKE_CURRENT_SOURCE_DIR}/bin"
)
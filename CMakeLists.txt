cmake_minimum_required(VERSION 3.13.4)

project(MyProject)

# set executable
add_executable(${PROJECT_NAME} main.cpp)

# set static libraries
# add_library(mylib myfile.cpp)

# set shared libraries
# add_library(mysharedlib SHARED mysharedfile.cpp)

# set variable
set(libDir "libs")

# set relative path link to shared libraries
set_target_properties(${PROJECT_NAME} PROPERTIES SKIP_BUILD_RPATH true LINK_FLAGS "-Wl,-rpath,$ORIGIN/")

# set include drectories
include_directories(${libDir}/include)

# set target link directories (libraries file)
target_link_directories(${PROJECT_NAME} PRIVATE ${libDir})

# set libraries will be link (libraries name)
target_link_libraries(${PROJECT_NAME} PRIVATE demolib demolib2)

# add command
add_custom_command(TARGET ${PROJECT_NAME}
    COMMAND cp ../${libDir}/libdemolib2.so ./
)

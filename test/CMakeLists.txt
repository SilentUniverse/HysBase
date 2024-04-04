add_executable(t FormatTest.cpp Test.cpp ../src/func.cpp)
target_link_libraries(t PRIVATE gtest)

include_directories(../include)

add_test(NAME t COMMAND t)
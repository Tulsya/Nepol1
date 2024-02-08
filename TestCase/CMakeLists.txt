# CMakeList.txt : CMake project for TestCase, include source and define
# project specific logic here.
#
cmake_minimum_required (VERSION 3.8)

# Enable Hot Reload for MSVC compilers if supported.
if (POLICY CMP0141)
  cmake_policy(SET CMP0141 NEW)
  set(CMAKE_MSVC_DEBUG_INFORMATION_FORMAT "$<IF:$<AND:$<C_COMPILER_ID:MSVC>,$<CXX_COMPILER_ID:MSVC>>,$<$<CONFIG:Debug,RelWithDebInfo>:EditAndContinue>,$<$<CONFIG:Debug,RelWithDebInfo>:ProgramDatabase>>")
endif()

project ("TestCase")

# Add source to this project's executable.
add_executable (TestCase "TestCase.cpp" "TestCase.h")

if (CMAKE_VERSION VERSION_GREATER 3.12)
  set_property(TARGET TestCase PROPERTY CXX_STANDARD 20)
endif()

# TODO: Add tests and install targets if needed.
# Добавляем путь к исходникам Catch2
add_subdirectory(external/Catch2-devel)

# Создаем исполняемый файл для тестов
add_executable(my_tests TestCase.cpp)

# Линкуем исполняемый файл с библиотекой Catch2
#target_link_libraries(my_tests PRIVATE Catch2::Catch2)

# Добавляем тесты
include(CTest)
include(Catch)
catch_discover_tests(my_tests)

cmake_minimum_required(VERSION 3.8.2)
project(Sample VERSION 1.0.0 LANGUAGES CXX)

include(CTest)
find_package(CMakeORTools REQUIRED)

add_executable(sample main.cpp)
target_compile_features(sample PUBLIC cxx_std_11)
set_target_properties(sample PROPERTIES VERSION ${PROJECT_VERSION})
target_link_libraries(sample PRIVATE CMakeORTools::Foo)

if(BUILD_TESTING)
	add_test(NAME sample_UT COMMAND sample)
endif()

include(GNUInstallDirs)
install(TARGETS sample
	EXPORT SampleTargets
	DESTINATION ${CMAKE_INSTALL_BINDIR})

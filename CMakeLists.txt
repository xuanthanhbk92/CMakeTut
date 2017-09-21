cmake_minimum_required (VERSION 2.6)
project (ProjectName)

# Set some marcro

set (VERSION_MAJOR 1)
set (VERSION_MINOR 0)

# configure header file 

configure_file (
	"${PROJECT_SOURCE_DIR}/inc/config.h.in"
	"${PROJECT_BINARY_DIR}/inc/config.h"
)

# add directories
include_directories ("${PROJECT_BINARY_DIR}/inc")
include_directories ("${PROJECT_SOURCE_DIR}/inc")

# Add library
include_directories ("${PROJECT_SOURCE_DIR}/lib")
add_subdirectory (lib) 

# Add exec file
add_executable(ProjectName main.c)
# Add linker lib
target_link_libraries (ProjectName MyLib)

# add the install targets
install (TARGETS ProjectName DESTINATION bin)
install (FILES "${PROJECT_BINARY_DIR}/inc/config.h" DESTINATION include)

#Testing 
include(CTest)

# Does application run
add_test (AppRun ProjectName)

# Does application run with parameter and check the output string
#add_test (AppWithPara ProjectName 25)
#set_tests_properties (AppWithPara PROPERTIES PASS_REGULAR_EXPRESSION "25 is 5")

# We can use marco 

#define a macro to simplify adding tests, then use it
macro (do_test arg result)
  add_test (TutorialComp${arg} Tutorial ${arg})
  set_tests_properties (TutorialComp${arg}
    PROPERTIES PASS_REGULAR_EXPRESSION ${result})
endmacro (do_test)
 
# do a bunch of result based tests
#do_test (25 "25 is 5")
#do_test (-25 "-25 is 0")



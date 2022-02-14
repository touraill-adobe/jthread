cmake_minimum_required(VERSION 3.20)

project(jthread)

set(CMAKE_CXX_STANDARD 17)

enable_testing()

add_library(jthread_jthread INTERFACE)
add_library(jthread::jthread ALIAS jthread_jthread)

target_include_directories(jthread_jthread
	INTERFACE
		source
)


foreach(_test
	cv
	cvcb
	cvprodcons
	cvrace
	cvrace_hh
	cvrace_pred
	cvrace_stop
	jthread1
	jthread2
	stoken
	stokencb
	stokenrace
	stopcb
)
	add_executable(test_${_test})
	target_sources(test_${_test} PRIVATE source/test_${_test}.cpp)
	target_link_libraries(test_${_test}	PRIVATE	jthread::jthread)
	add_test(NAME ${_test} COMMAND test_${_test})
endforeach()

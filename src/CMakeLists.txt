cmake_minimum_required(VERSION 2.8 FATAL_ERROR)

set(PROJECT_NAME server)

project(${PROJECT_NAME} CXX)

set(SRC_FILES server_app.cpp)

add_executable(${PROJECT_NAME} ${SRC_FILES})

set(EXT_LOG4CPLUS_NAME debug "log4cplusSD" optimized "log4cplusS" CACHE STRING "Log4cplus Libraries")

target_link_libraries(${PROJECT_NAME} ${EXT_LOG4CPLUS_NAME})
target_link_libraries(${PROJECT_NAME}
        ${Boost_THREAD_LIBRARY} ${Boost_SYSTEM_LIBRARY}
        ${Boost_DATE_TIME_LIBRARY} ${Boost_CHRONO_LIBRARY}
        ${Boost_REGEX_LIBRARY} ${Boost_FILESYSTEM_LIBRARY}
        ${Boost_ATOMIC_LIBRARY} ${Boost_PROGRAM_OPTIONS_LIBRARY}
        ${LIBZMQ_LIBRARIES}
	)
if(UNIX)
    target_link_libraries(${PROJECT_NAME} pthread)
endif()


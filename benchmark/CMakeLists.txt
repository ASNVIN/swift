option(SWIFT_INCLUDE_PERF_TESTSUITE "Create targets for swift performance benchmarks." NO)
if(CMAKE_SYSTEM_NAME STREQUAL "Darwin")
  # Performance test harness only builds on Darwin.
  if (SWIFT_INCLUDE_PERF_TESTSUITE)
    set(PERF_TESTSUITE_DIR "${CMAKE_CURRENT_SOURCE_DIR}/PerfTestSuite" CACHE STRING "Path to swift performance testsuite repo.")
    if(EXISTS ${PERF_TESTSUITE_DIR}/CMakeLists.txt)
      add_subdirectory(${PERF_TESTSUITE_DIR})
    else()
      message(FATAL_ERROR "Can't find the Swift performance suite at ${PERF_TESTSUITE_DIR}/.")
    endif()
    add_custom_target(benchmark-swift
        DEPENDS benchmark-swift PerfTests_Onone PerfTests_O
        PerfTests_Ounchecked)
  endif()
endif()


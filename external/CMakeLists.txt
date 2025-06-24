# external/CMakeLists.txt

set(MQL5_INCLUDE_DIR "${CMAKE_BINARY_DIR}/MQL5/Include")
set(CPP_INCLUDE_DIR "${CMAKE_BINARY_DIR}/include")
set(CPP_SRC_DIR     "${CMAKE_BINARY_DIR}/src")
set(CPP_LIB_DIR     "${CMAKE_BINARY_DIR}/lib")

### ------------------------------
### hmac-cpp (MQL5 headers only)
### ------------------------------

file(GLOB HMAC_HEADERS
    "${CMAKE_CURRENT_SOURCE_DIR}/hmac-cpp/*.mqh"
)
file(MAKE_DIRECTORY "${MQL5_INCLUDE_DIR}/hmac-cpp")
file(COPY ${HMAC_HEADERS} DESTINATION "${MQL5_INCLUDE_DIR}/hmac-cpp")

### ------------------------------
### SimpleNamedPipe (MQL5)
### ------------------------------

file(GLOB SNP_MQL_HEADERS
    "${CMAKE_CURRENT_SOURCE_DIR}/SimpleNamedPipe/MQL5/Include/SimpleNamedPipe/*.mqh"
)
file(MAKE_DIRECTORY "${MQL5_INCLUDE_DIR}/SimpleNamedPipe")
file(COPY ${SNP_MQL_HEADERS} DESTINATION "${MQL5_INCLUDE_DIR}/SimpleNamedPipe")

### ------------------------------
### SimpleNamedPipe (C++)
### ------------------------------

set(SNP_SOURCE_DIR "${CMAKE_CURRENT_SOURCE_DIR}/SimpleNamedPipe/include/SimpleNamedPipe")
set(SNP_TARGET_DIR "${CPP_INCLUDE_DIR}/SimpleNamedPipe")

file(MAKE_DIRECTORY "${SNP_TARGET_DIR}")
file(GLOB_RECURSE SNP_HEADERS
    "${SNP_SOURCE_DIR}/*.hpp"
    "${SNP_SOURCE_DIR}/*.ipp"
    "${SNP_SOURCE_DIR}/*.h"
)

foreach(header IN LISTS SNP_HEADERS)
    file(RELATIVE_PATH rel_path "${SNP_SOURCE_DIR}" "${header}")

    set(target_path "${SNP_TARGET_DIR}/${rel_path}")

    get_filename_component(target_dir "${target_path}" DIRECTORY)
    file(MAKE_DIRECTORY "${target_dir}")

    file(COPY "${header}" DESTINATION "${target_dir}")
endforeach()

# Optional: build static lib
option(SIMPLE_NAMED_PIPE_BUILD_STATIC "Build static lib for SimpleNamedPipe" OFF)
if (SIMPLE_NAMED_PIPE_BUILD_STATIC)
    add_subdirectory(SimpleNamedPipe)
endif()

### ------------------------------
### time-shield-cpp (MQL5)
### ------------------------------

file(GLOB TSC_MQL_HEADERS
    "${CMAKE_CURRENT_SOURCE_DIR}/time-shield-cpp/MQL5/Include/*.mqh"
)
file(GLOB TSC_MQL_HEADERS_NESTED
    "${CMAKE_CURRENT_SOURCE_DIR}/time-shield-cpp/MQL5/Include/time_shield/*.mqh"
)
file(MAKE_DIRECTORY "${MQL5_INCLUDE_DIR}/time_shield")
file(COPY ${TSC_MQL_HEADERS} DESTINATION "${MQL5_INCLUDE_DIR}")
file(COPY ${TSC_MQL_HEADERS_NESTED} DESTINATION "${MQL5_INCLUDE_DIR}/time_shield")

### ------------------------------
### time-shield-cpp (C++)
### ------------------------------

file(GLOB TSC_CPP_HEADERS
    "${CMAKE_CURRENT_SOURCE_DIR}/time-shield-cpp/include/time_shield_cpp/*.hpp"
)
file(GLOB TSC_CPP_HEADERS_NESTED
    "${CMAKE_CURRENT_SOURCE_DIR}/time-shield-cpp/include/time_shield_cpp/time_shield/*.hpp"
)
file(MAKE_DIRECTORY "${CPP_INCLUDE_DIR}/time_shield_cpp/time_shield")
file(COPY ${TSC_CPP_HEADERS} DESTINATION "${CPP_INCLUDE_DIR}/time_shield_cpp")
file(COPY ${TSC_CPP_HEADERS_NESTED} DESTINATION "${CPP_INCLUDE_DIR}/time_shield_cpp/time_shield")

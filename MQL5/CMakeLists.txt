# MQL5/CMakeLists.txt

set(MQL5_INCLUDE_SRC_DIR "${CMAKE_CURRENT_SOURCE_DIR}/Include")
set(MQL5_INCLUDE_DST_DIR "${CMAKE_BINARY_DIR}/MQL5/Include")

# --- Copy jason.mqh and related files ---

file(GLOB_RECURSE JASON_FILES
    "${MQL5_INCLUDE_SRC_DIR}/MQL5X/external/jason/*.mqh"
    "${MQL5_INCLUDE_SRC_DIR}/MQL5X/external/jason/*.txt"
)

foreach(file_path IN LISTS JASON_FILES)
    file(RELATIVE_PATH rel_path "${MQL5_INCLUDE_SRC_DIR}" "${file_path}")

    set(target_path "${MQL5_INCLUDE_DST_DIR}/${rel_path}")

    get_filename_component(target_dir "${target_path}" DIRECTORY)
    file(MAKE_DIRECTORY "${target_dir}")

    file(COPY "${file_path}" DESTINATION "${target_dir}")
endforeach()

# --- Copy MT4Orders.mqh and related files ---

file(GLOB_RECURSE MT4ORDERS_FILES
    "${MQL5_INCLUDE_SRC_DIR}/MQL5X/external/mt4orders/*.mqh"
    "${MQL5_INCLUDE_SRC_DIR}/MQL5X/external/mt4orders/*.txt"
    "${MQL5_INCLUDE_SRC_DIR}/MQL5X/external/mt4orders/*.dox"
)

foreach(file_path IN LISTS MT4ORDERS_FILES)
    file(RELATIVE_PATH rel_path "${MQL5_INCLUDE_SRC_DIR}" "${file_path}")
    set(target_path "${MQL5_INCLUDE_DST_DIR}/${rel_path}")
    get_filename_component(target_dir "${target_path}" DIRECTORY)
    file(MAKE_DIRECTORY "${target_dir}")
    file(COPY "${file_path}" DESTINATION "${target_dir}")
endforeach()

# --- Copy hash.mqh and related files ---
file(GLOB_RECURSE HASH_FILES
    "${MQL5_INCLUDE_SRC_DIR}/MQL5X/external/hash/*.mqh"
    "${MQL5_INCLUDE_SRC_DIR}/MQL5X/external/hash/*.txt"
    "${MQL5_INCLUDE_SRC_DIR}/MQL5X/external/hash/*.dox"
)
foreach(file_path IN LISTS HASH_FILES)
    file(RELATIVE_PATH rel_path "${MQL5_INCLUDE_SRC_DIR}" "${file_path}")
    set(target_path "${MQL5_INCLUDE_DST_DIR}/${rel_path}")
    get_filename_component(target_dir "${target_path}" DIRECTORY)
    file(MAKE_DIRECTORY "${target_dir}")
    file(COPY "${file_path}" DESTINATION "${target_dir}")
endforeach()
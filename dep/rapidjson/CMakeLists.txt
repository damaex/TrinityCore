# This file is part of the TrinityCore Project. See AUTHORS file for Copyright information
#
# This file is free software; as a special exception the author gives
# unlimited permission to copy and/or distribute it, with or without
# modifications, as long as this notice is preserved.
#
# This program is distributed in the hope that it will be useful, but
# WITHOUT ANY WARRANTY, to the extent permitted by law; without even the
# implied warranty of MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.

add_library(rapidjson INTERFACE)

target_include_directories(rapidjson
  INTERFACE
    ${CMAKE_CURRENT_SOURCE_DIR})

if(CMAKE_SYSTEM_PROCESSOR STREQUAL "aarch64")
  set(TC_RAPIDJSON_OPT "RAPIDJSON_NEON")
else()
  set(TC_RAPIDJSON_OPT "RAPIDJSON_SSE2")
endif()

target_compile_definitions(rapidjson
  INTERFACE
    -DRAPIDJSON_HAS_STDSTRING
    -D${TC_RAPIDJSON_OPT}
    -DRAPIDJSON_48BITPOINTER_OPTIMIZATION=0
    -DRAPIDJSON_ASSERT=WPAssert)

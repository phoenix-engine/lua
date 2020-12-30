set(SRC_lib
  lapi.c lcode.c lctype.c ldebug.c ldo.c ldump.c lfunc.c lgc.c llex.c
  lmem.c lobject.c lopcodes.c lparser.c lstate.c lstring.c ltable.c
  ltm.c lundump.c lvm.c lzio.c lauxlib.c lbaselib.c lcorolib.c ldblib.c
  liolib.c lmathlib.c loadlib.c loslib.c lstrlib.c ltablib.c lutf8lib.c
  linit.c
)

set(SRC_Lua  lua.c)
set(SRC_Luac luac.c)

add_library(liblua    STATIC ${SRC_lib})
add_library(libluadll SHARED ${SRC_lib})

target_compile_definitions(libluadll
  PRIVATE
  _CRT_SECURE_NO_WARNINGS
  LUA_BUILD_AS_DLL
)

if(CMAKE_BUILD_TYPE STREQUAL "Debug")
  # Compile with runtime checks enabled in debug mode.
  target_compile_definitions(libluadll LUA_USE_APICHECK)
endif(CMAKE_BUILD_TYPE STREQUAL "Debug")

set_target_properties(libluadll
  PROPERTIES
  OUTPUT_NAME lua5_4_2
)

add_executable(lua ${SRC_Lua})
target_link_libraries (lua liblua)

add_executable(luac ${SRC_Luac})
target_link_libraries(luac liblua)

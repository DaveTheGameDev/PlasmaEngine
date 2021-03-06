add_library(Platform)

plasma_setup_library(Platform ${CMAKE_CURRENT_LIST_DIR} TRUE)
plasma_use_precompiled_header(Platform ${CMAKE_CURRENT_LIST_DIR})

if(${PLASMA_RENDERER} MATCHES "BGFX")
  set(rendererSource
        ${CMAKE_CURRENT_LIST_DIR}/../BGFX/BGFXRenderer.cpp
        ${CMAKE_CURRENT_LIST_DIR}/../BGFX/BGFXRenderer.hpp 
  )
  set(rendererLib
    bgfx
  )
else(${PLASMA_RENDERER} MATCHES "OpenGL")
  set(rendererSource
      ${CMAKE_CURRENT_LIST_DIR}/../OpenGL/OpenglRenderer.cpp
      ${CMAKE_CURRENT_LIST_DIR}/../OpenGL/OpenglRenderer.hpp 
      ${CMAKE_CURRENT_LIST_DIR}/../OpenGL/OpenglRendererWindows.cpp
  )
  set(rendererLib
    GL
    Glew
  )
endif()

target_sources(Platform
  PRIVATE
    ${CMAKE_CURRENT_LIST_DIR}/../Curl/WebRequest.cpp
    ${CMAKE_CURRENT_LIST_DIR}/../Empty/MainLoop.cpp
    ${CMAKE_CURRENT_LIST_DIR}/../Libgit2/Git.cpp
    ${rendererSource}
    ${CMAKE_CURRENT_LIST_DIR}/Atomic.cpp
    ${CMAKE_CURRENT_LIST_DIR}/Audio.cpp
    ${CMAKE_CURRENT_LIST_DIR}/CallStack.cpp
    ${CMAKE_CURRENT_LIST_DIR}/ComPort.cpp
    ${CMAKE_CURRENT_LIST_DIR}/CrashHandler.cpp
    ${CMAKE_CURRENT_LIST_DIR}/DebugClassMap.cpp
    ${CMAKE_CURRENT_LIST_DIR}/DebugSymbolInformation.cpp
    ${CMAKE_CURRENT_LIST_DIR}/DirectoryWatcher.cpp
    ${CMAKE_CURRENT_LIST_DIR}/ExecutableResource.cpp
    ${CMAKE_CURRENT_LIST_DIR}/ExternalLibrary.cpp
    ${CMAKE_CURRENT_LIST_DIR}/File.cpp
    ${CMAKE_CURRENT_LIST_DIR}/FileSystem.cpp
    ${CMAKE_CURRENT_LIST_DIR}/FpControl.cpp
    ${CMAKE_CURRENT_LIST_DIR}/Intrinsics.cpp
    ${CMAKE_CURRENT_LIST_DIR}/Keys.inl
    ${CMAKE_CURRENT_LIST_DIR}/Main.cpp
    ${CMAKE_CURRENT_LIST_DIR}/MouseButtons.inl
    ${CMAKE_CURRENT_LIST_DIR}/Peripherals.cpp
    ${CMAKE_CURRENT_LIST_DIR}/PlatformStandard.cpp
    ${CMAKE_CURRENT_LIST_DIR}/Precompiled.cpp
    ${CMAKE_CURRENT_LIST_DIR}/Precompiled.hpp
    ${CMAKE_CURRENT_LIST_DIR}/Process.cpp
    ${CMAKE_CURRENT_LIST_DIR}/Resolution.cpp
    ${CMAKE_CURRENT_LIST_DIR}/Shell.cpp
    ${CMAKE_CURRENT_LIST_DIR}/Socket.cpp
    ${CMAKE_CURRENT_LIST_DIR}/StackWalker.cpp
    ${CMAKE_CURRENT_LIST_DIR}/StackWalker.hpp
    ${CMAKE_CURRENT_LIST_DIR}/Thread.cpp
    ${CMAKE_CURRENT_LIST_DIR}/ThreadIo.hpp
    ${CMAKE_CURRENT_LIST_DIR}/ThreadSync.cpp
    ${CMAKE_CURRENT_LIST_DIR}/Timer.cpp
    ${CMAKE_CURRENT_LIST_DIR}/Utilities.cpp
    ${CMAKE_CURRENT_LIST_DIR}/WString.cpp
    ${CMAKE_CURRENT_LIST_DIR}/WString.hpp
    ${CMAKE_CURRENT_LIST_DIR}/WinUtility.cpp
    ${CMAKE_CURRENT_LIST_DIR}/WinUtility.hpp
    ${CMAKE_CURRENT_LIST_DIR}/WindowsError.cpp
    ${CMAKE_CURRENT_LIST_DIR}/WindowsError.hpp
)

plasma_target_includes(Platform
  PUBLIC
    Common
)

target_link_libraries(Platform
  PUBLIC
    Curl
    ${rendererLib}
    Libgit2
    tracy
)

set_target_properties( Platform PROPERTIES FOLDER "PlasmaEngine" )

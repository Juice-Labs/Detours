cmake_minimum_required(VERSION 3.5)

project(detours)

add_library(${PROJECT_NAME} STATIC)

target_compile_options(${PROJECT_NAME}
    PRIVATE /nologo /W0 /Zi /Gy /Gm- /Zl /Od /DDETOUR_DEBUG=0)

if (${ARCH} STREQUAL "x86_64")
    target_compile_definitions(${PROJECT_NAME}
        PRIVATE
        WIN32_LEAN_AND_MEAN
        DETOURS_SOURCE_BROWSING=0
        DETOURS_OPTION_PROCESSOR=X86
        DETOURS_OPTION_BITS=32
    )
else()
    target_compile_definitions(${PROJECT_NAME}
        PRIVATE
        WIN32_LEAN_AND_MEAN
        DETOURS_SOURCE_BROWSING=0
        # Don't set DETOURS_OPTION_PROCESSOR for x64 because we
        # don't *know* that we'll run on a 64-bit machine.
        DETOURS_OPTION_BITS=64
    )
endif()

target_include_directories(${PROJECT_NAME}
    PUBLIC 
    src
)

target_sources(${PROJECT_NAME} 
    PRIVATE
    src/creatwth.cpp
    src/detours.cpp
    src/detours.h
    src/detver.h
    src/disasm.cpp
    src/disolarm.cpp
    src/disolarm64.cpp
    src/disolia64.cpp
    src/disolx64.cpp
    src/disolx86.cpp
    src/image.cpp
    src/modules.cpp
    src/uimports.cpp
)

# Ths file src/uiimports.cpp is included to generate source with
# different macros defined, don't compile it.
set_property(
    SOURCE src/uimports.cpp
    APPEND PROPERTY HEADER_FILE_ONLY true
)

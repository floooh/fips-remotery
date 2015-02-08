#
# project: fips-remotery
#
if (NOT FIPS_IMPORT)
    cmake_minimum_required(VERSION 2.8)
    get_filename_component(FIPS_ROOT_DIR "../fips" ABSOLUTE)
    include("${FIPS_ROOT_DIR}/cmake/fips.cmake")
    fips_setup()
    fips_project(fips-remotery)
endif()

if (FIPS_LINUX OR FIPS_MACOS OR FIPS_WINDOWS)
    fips_begin_lib(Remotery)
        fips_dir(Remotery/lib GROUP ".")
        fips_files(Remotery.c Remotery.h)
        if (FIPS_LINUX)
            fips_libs(rt)
        endif()
    fips_end_lib()

    # silence some warnings when compiling remotery
    if (FIPS_CLANG)
        set_target_properties(Remotery PROPERTIES COMPILE_FLAGS "-Wno-missing-field-initializers -Wno-unused-function")
    elseif (FIPS_GCC)
        set_target_properties(Remotery PROPERTIES COMPILE_FLAGS "-Wno-unused-function -Wno-unused-but-set-variable")
    endif()
endif()
if (NOT FIPS_IMPORT)
    fips_finish()
endif()


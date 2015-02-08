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

fips_include_directories(Remotery/lib)
fips_begin_lib(Remotery)
    fips_dir(Remotery/lib GROUP ".")
    fips_files(Remotery.c Remotery.h)
fips_end_lib()

# silence some warnings when compiling remotery
if (FIPS_CLANG)
    set_target_properties(Remotery PROPERTIES COMPILE_FLAGS "-Wno-missing-field-initializers -Wno-unused-function")
endif()

if (NOT FIPS_IMPORT)
    fips_finish()
endif()


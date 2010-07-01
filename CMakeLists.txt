# This is the root ITK CMakeLists file.
cmake_minimum_required(VERSION 2.8)
if(COMMAND CMAKE_POLICY)
  cmake_policy(SET CMP0003 NEW)
endif(COMMAND CMAKE_POLICY)


project(ITK)
include_regular_expression("^([Nn]rrd|itk|vtk|vnl|vcl|vxl|v3p|f2c|netlib|ce|itpack|DICOM|meta|png|dbh|tif|jpeg|zlib|gdcm).*$")
source_group("XML Files" REGULAR_EXPRESSION "[.]xml$")

# On Visual Studio 8 MS deprecated C. This removes all 1.276E1265 security
# warnings
if(WIN32)
  if(not CYGWIN)
    if(not MINGW)
      if(not ITK_ENABLE_VISUAL_STUDIO_DEPRECATED_C_WARNINGS)
        add_definitions(
          -D_CRT_FAR_MAPPINGS_NO_DEPRECATE
          -D_CRT_IS_WCTYPE_NO_DEPRECATE
          -D_CRT_MANAGED_FP_NO_DEPRECATE
          -D_CRT_NONSTDC_NO_DEPRECATE
          -D_CRT_SECURE_NO_DEPRECATE
          -D_CRT_SECURE_NO_DEPRECATE_GLOBALS
          -D_CRT_SETERRORMODE_BEEP_SLEEP_NO_DEPRECATE
          -D_CRT_TIME_FUNCTIONS_NO_DEPRECATE
          -D_CRT_VCCLRIT_NO_DEPRECATE
          -D_SCL_SECURE_NO_DEPRECATE
          )
      endif(not ITK_ENABLE_VISUAL_STUDIO_DEPRECATED_C_WARNINGS)
    endif(not MINGW)
  endif(not CYGWIN)
endif(WIN32)

#-----------------------------------------------------------------------------
# ITK version number.  An even minor number corresponds to releases.
set(ITK_VERSION_MAJOR "4")
set(ITK_VERSION_MINOR "0")
set(ITK_VERSION_PATCH "0")

# Version string should not include patch level.  The major.minor is
# enough to distinguish available features of the toolkit.
set(ITK_VERSION_STRING "${ITK_VERSION_MAJOR}.${ITK_VERSION_MINOR}")

include(CTest)
include(CPack)

add_subdirectory(Code)
add_subdirectory(Testing)


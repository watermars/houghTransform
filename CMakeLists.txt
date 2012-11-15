#-----------------------------------------------------------------------------
cmake_minimum_required(VERSION 2.8.4)
#-----------------------------------------------------------------------------

#-----------------------------------------------------------------------------
# See http://cmake.org/cmake/help/cmake-2-8-docs.html#section_Policies for details
#-----------------------------------------------------------------------------
if(POLICY CMP0017)
  cmake_policy(SET CMP0017 OLD)
endif()

#-----------------------------------------------------------------------------
# Module name
#   - Usually identique to the directory name)
#   - You shouldn't call 'project(...)'. See SlicerConfig.cmake for more details.
#-----------------------------------------------------------------------------

set(MODULE_NAME houghTransformCLI)

#-----------------------------------------------------------------------------
# Prerequisites
#-----------------------------------------------------------------------------
if(NOT Slicer_SOURCE_DIR)
  find_package(Slicer REQUIRED)

  # Additional C/CXX flags - Should be defined before including Slicer_USE_FILE
  set(ADDITIONAL_C_FLAGS "" CACHE STRING "Additional ${EXTENSION_NAME} C Flags")
  set(ADDITIONAL_CXX_FLAGS "" CACHE STRING "Additional ${EXTENSION_NAME} CXX Flags")

  include(${Slicer_USE_FILE})

  set(EXTENSION_DEPENDS NA) # Specified as a space separated list or 'NA' if any
  set(EXTENSION_LICENSE_FILE ${Slicer_LICENSE_FILE})
  set(EXTENSION_README_FILE ${Slicer_README_FILE})
  set(EXTENSION_LICENSE_SHORT_DESCRIPTION ${Slicer_LICENSE_SHORT_DESCRIPTION})

  include(SlicerEnableExtensionTesting)
endif()

# Configure XML description
configure_file(
  ${EXTENSION_NAME}.xml
  ${CMAKE_CURRENT_BINARY_DIR}/${EXTENSION_NAME}.xml
  @ONLY
  )


#add_subdirectory(Logic)

set(cli_module_export_directive "Q_SLICER_QTMODULES_LOADABLEEXTENSIONTEMPLATE_EXPORT")

# Additional includes
set(cli_module_include_directories
  )

# Additional source files
set(cli_module_SRCS
  )

# I added these for local headers and libs. (Yi Gao)


# Additional Target libraries
set(cli_module_target_libraries
    ${ITK_LIBRARIES}
    ${VTK_LIBRARIES}
)


#-----------------------------------------------------------------------------
# Build
#-----------------------------------------------------------------------------

SlicerMacroBuildCLI(
  NAME ${EXTENSION_NAME}
  #LOGO_HEADER ${Slicer_SOURCE_DIR}/Resources/NAMICLogo.h
  TARGET_LIBRARIES ${cli_module_target_libraries} ${ITK_LIBRARIES}
  INCLUDE_DIRECTORIES ${cli_module_include_directories} 
  INCLUDE_DIRECTORIES ${ITK_LIBRARIES} ${VTK_LIBRARIES} ${cli_module_include_directories}
  ADDITIONAL_SRCS ${cli_module_SRCS}
  #EXECUTABLE_ONLY
  )

# SlicerMacroBuildCLI(
  # NAME ${EXTENSION_NAME}
  # #LOGO_HEADER ${Slicer_SOURCE_DIR}/Resources/NAMICLogo.h
  # TARGET_LIBRARIES ${cli_module_target_libraries} ${ITK_LIBRARIES}
  # INCLUDE_DIRECTORIES ${cli_module_include_directories} 
  # INCLUDE_DIRECTORIES ${ITK_LIBRARIES} ${VTK_LIBRARIES} ${cli_module_include_directories}
  # ADDITIONAL_SRCS ${cli_module_SRCS}
  # #EXECUTABLE_ONLY
  # )

# #-----------------------------------------------------------------------------
# # Testing
# #-----------------------------------------------------------------------------
# if(BUILD_TESTING)
#   add_subdirectory(Testing)
# endif()

#-----------------------------------------------------------------------------
# Generate extension description file '<EXTENSION_NAME>.s4ext'
#-----------------------------------------------------------------------------
# if(NOT Slicer_SOURCE_DIR)
#   include(SlicerFunctionGenerateExtensionDescription)
#   slicerFunctionGenerateExtensionDescription(
#     EXTENSION_NAME ${EXTENSION_NAME}
#     EXTENSION_CATEGORY ${EXTENSION_CATEGORY}
#     EXTENSION_ICONURL ${EXTENSION_ICONURL}
#     EXTENSION_STATUS ${EXTENSION_STATUS}
#     EXTENSION_HOMEPAGE ${EXTENSION_HOMEPAGE}
#     EXTENSION_CONTRIBUTORS ${EXTENSION_CONTRIBUTORS}
#     EXTENSION_DESCRIPTION ${EXTENSION_DESCRIPTION}
#     EXTENSION_SCREENSHOTURLS ${EXTENSION_SCREENSHOTURLS}
#     EXTENSION_DEPENDS ${EXTENSION_DEPENDS}
#     DESTINATION_DIR ${CMAKE_CURRENT_BINARY_DIR}
#     SLICER_WC_REVISION ${Slicer_WC_REVISION}
#     SLICER_WC_ROOT ${Slicer_WC_ROOT}
#     )
# endif()

# #-----------------------------------------------------------------------------
# # Packaging
# #-----------------------------------------------------------------------------
# if(NOT Slicer_SOURCE_DIR)
#   include(${Slicer_EXTENSION_CPACK})
# endif()

#message(${ITK_LIBRARIES})

# ################################################################################
# # exe's
# option(build_mainComputeNeedelTensorImage "build mainComputeNeedelTensorImage?" OFF)
# if (build_mainComputeNeedelTensorImage)
#     set(cexx mainComputeNeedelTensorImage)
#     add_executable(${cexx} ${cexx}.cxx)
#     target_link_libraries(${cexx} ${ITK_LIBRARIES})
# endif (build_mainComputeNeedelTensorImage)


# option(build_mainFitLines "build mainFitLines?" OFF)
# if (build_mainFitLines)
#     set(cexx mainFitLines)
#     add_executable(${cexx} ${cexx}.cxx)
#     target_link_libraries(${cexx} myLib ${ITK_LIBRARIES} ${VTK_LIBRARIES})
# endif (build_mainFitLines)


# option(build_houghTransform "build houghTransform?" ON)
# if (build_houghTransform)
    # set(cexx houghTransform)
    # add_executable(${cexx} ${cexx}.cxx)
    # target_link_libraries(${cexx} ${ITK_LIBRARIES} ${VTK_LIBRARIES})
# endif (build_houghTransform)
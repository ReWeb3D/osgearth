#the old construct SUBDIRS( was substituded by ADD_SUBDIRECTORY that is to be preferred according on CMake docs.
FOREACH( lib
         osgEarth
         osgEarthAnnotation
         osgEarthFeatures
         osgEarthUtil
         osgEarthSymbology )

    ADD_SUBDIRECTORY(${lib})
    
    SET_PROPERTY(TARGET ${lib} PROPERTY FOLDER "Libs")

ENDFOREACH( lib )

ADD_SUBDIRECTORY( osgEarthDrivers )

IF (OSGEARTH_BUILD_EXAMPLES)
	ADD_SUBDIRECTORY( applications )
ENDIF()

IF (QT4_FOUND AND NOT ANDROID AND OSGEARTH_USE_QT)
    ADD_SUBDIRECTORY(osgEarthQt)
    SET_PROPERTY(TARGET osgEarthQt PROPERTY FOLDER "Libs")
ENDIF()

IF(MSVC80)
  OPTION(OSGEARTH_MSVC_GENERATE_PLUGINS_AND_WRAPPERS_MANIFESTS "Generate or not manifests files under VS8 for dynamically loaded dlls" ON)
ENDIF(MSVC80)



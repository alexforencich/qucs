PROJECT(qucslib CXX C)
CMAKE_MINIMUM_REQUIRED(VERSION 2.6)
cmake_policy(VERSION 2.6)

SET(CMAKE_BUILD_TYPE Debug)

ADD_DEFINITIONS( -DHAVE_CONFIG_H )

# define variables
SET(BINARYDIR "${CMAKE_INSTALL_PREFIX}/bin/")
SET(BITMAPDIR "${CMAKE_INSTALL_PREFIX}/share/qucs/bitmaps/")
SET(DOCDIR "${CMAKE_INSTALL_PREFIX}/share/qucs/docs/")
SET(LANGUAGEDIR "${CMAKE_INSTALL_PREFIX}/share/qucs/lang/")
SET(LIBRARYDIR "${CMAKE_INSTALL_PREFIX}/share/qucs/library/")
SET(OCTAVEDIR "${CMAKE_INSTALL_PREFIX}/share/qucs/octave/")

# configure the header config.h
CONFIGURE_FILE (
    "${PROJECT_SOURCE_DIR}/../config.h.cmake"
    "${PROJECT_BINARY_DIR}/config.h"
)

INCLUDE_DIRECTORIES("${PROJECT_BINARY_DIR}")

FIND_PACKAGE( Qt4 REQUIRED )
SET( QT_USE_QTGUI TRUE )
#SET( QT_USE_QT3SUPPORT TRUE )

INCLUDE( ${QT_USE_FILE} )

ADD_DEFINITIONS(${QT_DEFINITIONS})

SET(QUCSLIB_SRCS
main.cpp qucslib.cpp displaydialog.cpp symbolwidget.cpp searchdialog.cpp librarydialog.cpp
)

SET(QUCSLIB_MOC_HDRS
qucslib.h displaydialog.h symbolwidget.h searchdialog.h librarydialog.h
)

QT4_WRAP_CPP( QUCSLIB_MOC_SRCS ${QUCSLIB_MOC_HDRS} )

SET(RESOURCES qucslib.qrc)
QT4_ADD_RESOURCES(RESOURCES_SRCS ${RESOURCES})

IF(APPLE)
  # set information on Info.plist file
	SET(MACOSX_BUNDLE_INFO_STRING "${PROJECT_NAME} ${PROJECT_VERSION}")
  SET(MACOSX_BUNDLE_BUNDLE_VERSION "${PROJECT_NAME} ${PROJECT_VERSION}")
  SET(MACOSX_BUNDLE_LONG_VERSION_STRING "${PROJECT_NAME} ${PROJECT_VERSION}")
  SET(MACOSX_BUNDLE_SHORT_VERSION_STRING "${PROJECT_VERSION}")
  SET(MACOSX_BUNDLE_COPYRIGHT "${PROJECT_COPYRIGHT_YEAR} ${PROJECT_VENDOR}")
  SET(MACOSX_BUNDLE_GUI_IDENTIFIER "${PROJECT_DOMAIN_SECOND}.${PROJECT_DOMAIN_FIRST}")
  SET(MACOSX_BUNDLE_BUNDLE_NAME "${PROJECT_NAME}")
  SET(MACOSX_BUNDLE_COPYRIGHT "(C) 2013 Qucs team" )
  SET(MACOSX_BUNDLE_ICON_FILE qucslib.icns)

  # set where in the bundle to put the icns file
  SET_SOURCE_FILES_PROPERTIES(${CMAKE_CURRENT_SOURCE_DIR}/../qucs/bitmaps/qucslib.icns PROPERTIES MACOSX_PACKAGE_LOCATION Resources)
  # include the icns file in the target
  SET(QUCSLIB_SRCS ${QUCSLIB_SRCS} ${CMAKE_CURRENT_SOURCE_DIR}/../qucs/bitmaps/qucslib.icns)

ENDIF(APPLE)

ADD_EXECUTABLE(qucslib MACOSX_BUNDLE WIN32
  ${QUCSLIB_SRCS}
  ${QUCSLIB_MOC_SRCS}
  ${RESOURCES_SRCS} )

TARGET_LINK_LIBRARIES(qucslib ${QT_LIBRARIES})

INSTALL(TARGETS qucslib
    BUNDLE DESTINATION . COMPONENT Runtime
    RUNTIME DESTINATION bin COMPONENT Runtime
    )

ADD_SUBDIRECTORY( library )

# man pages
INSTALL( FILES qucslib.1 DESTINATION share/man/man1 )


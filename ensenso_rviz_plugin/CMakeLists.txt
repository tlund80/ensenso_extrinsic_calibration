cmake_minimum_required(VERSION 2.8.3)
project(ensenso_rviz_plugin)

find_package(catkin REQUIRED COMPONENTS
             grinding_ensenso_extrinsic_calibration
             rviz)

catkin_package()

include_directories(${catkin_INCLUDE_DIRS})

find_package(Qt4 COMPONENTS QtCore QtGui REQUIRED)
include(${QT_USE_FILE})

add_definitions(-DQT_NO_KEYWORDS)

qt4_wrap_cpp(MOC_FILES
  src/ensenso_panel.h
)

set(SOURCE_FILES
  src/ensenso_panel.cpp 
  ${MOC_FILES}
)

add_library(${PROJECT_NAME} ${SOURCE_FILES})
target_link_libraries(${PROJECT_NAME} ${QT_LIBRARIES} ${catkin_LIBRARIES})
add_dependencies(${PROJECT_NAME} grinding_ensenso_extrinsic_calibration_generate_messages_cpp)

install(TARGETS
  ${PROJECT_NAME}
  ARCHIVE DESTINATION ${CATKIN_PACKAGE_LIB_DESTINATION}
  LIBRARY DESTINATION ${CATKIN_PACKAGE_LIB_DESTINATION}
  RUNTIME DESTINATION ${CATKIN_PACKAGE_BIN_DESTINATION}
)

install(FILES 
  plugin_description.xml
  DESTINATION ${CATKIN_PACKAGE_SHARE_DESTINATION})


SET(ROSSRC_PKG_MODULES
  gstreamer-base-1.0
  roscpp
  std_msgs
)

PKG_CHECK_MODULES(PKGS REQUIRED ${ROSSRC_PKG_MODULES})

LINK_DIRECTORIES(${PKGS_LIBRARY_DIRS})

ADD_LIBRARY(tensor_ros_src tensor_ros_src.cc)
ADD_DEPENDENCIES(tensor_ros_src nns_ros_bridge)
TARGET_INCLUDE_DIRECTORIES(tensor_ros_src PRIVATE
  ${PKGS_INCLUDE_DIRS}
)

TARGET_LINK_LIBRARIES(tensor_ros_src
  nns_ros_bridge
  ${PKGS_COMMON_LIBRARIES}
  ${PKGS_LIBRARIES}
)

INSTALL(TARGETS tensor_ros_src
  RUNTIME DESTINATION ${NNS_INSTALL_BINDIR}
  LIBRARY DESTINATION ${NNS_INSTALL_GSTDIR}
  ARCHIVE DESTINATION ${NNS_INSTALL_LIBDIR}
)

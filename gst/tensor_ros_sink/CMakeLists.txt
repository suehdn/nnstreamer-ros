SET(PKG_MODULES
  gstreamer-base-1.0
)

PKG_CHECK_MODULES(PKGS REQUIRED ${PKG_MODULES})

ADD_LIBRARY(tensor_ros_sink tensor_ros_sink.c)
ADD_DEPENDENCIES(tensor_ros_sink nns_ros_bridge)
TARGET_INCLUDE_DIRECTORIES(tensor_ros_sink PRIVATE
  ${PKGS_INCLUDE_DIRS}
)

TARGET_LINK_LIBRARIES(tensor_ros_sink
  nns_ros_bridge
  ${PKGS_COMMON_LIBRARIES}
  ${PKGS_LIBRARIES}
)

INSTALL(TARGETS tensor_ros_sink
  RUNTIME DESTINATION ${NNS_INSTALL_BINDIR}
  LIBRARY DESTINATION ${NNS_INSTALL_GSTDIR}
  ARCHIVE DESTINATION ${NNS_INSTALL_LIBDIR}
)

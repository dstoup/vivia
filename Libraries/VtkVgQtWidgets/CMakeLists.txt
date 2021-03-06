project(vtkVgQtWidgets)

include_directories(SYSTEM
  ${VTK_INCLUDE_DIRS}
)

include_directories(
  ${CMAKE_CURRENT_SOURCE_DIR}
  ${CMAKE_CURRENT_BINARY_DIR}
)

set(vtkVgQtWidgetsSources
  vtkVgRegionWidget.cxx
)

set(vtkVgQtWidgetsMocHeaders
  vtkVgRegionWidget.h
)

set(vtkVgQtWidgetsInstallHeaders
  vtkVgRegionWidget.h
)

qt5_wrap_cpp(vtkVgQtWidgetsMocSources ${vtkVgQtWidgetsMocHeaders})

add_library(${PROJECT_NAME}
  ${vtkVgQtWidgetsSources}
  ${vtkVgQtWidgetsMocSources}
)

vg_add_dependencies(${PROJECT_NAME}
  PRIVATE_INTERFACE_TARGETS
  qtVgCommon
  qtExtensions
  vtkVgModelView
  vtkVgQtUtil
  LINK_LIBRARIES
  LINK_PRIVATE
  ${VTK_OPENGL_RENDERING_COMPONENTS}
  vtkGUISupportQt
  LINK_PUBLIC
  vtkInteractionWidgets
)

install_library_targets(${PROJECT_NAME})
install_headers(${vtkVgQtWidgetsInstallHeaders} TARGET ${PROJECT_NAME}
                DESTINATION include/vtkVgQtWidgets)

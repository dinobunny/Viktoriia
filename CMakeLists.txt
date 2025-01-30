cmake_minimum_required(VERSION 3.16)

project(Viktoriia VERSION 0.1 LANGUAGES CXX)

set(CMAKE_CXX_STANDARD_REQUIRED ON)

find_package(Qt6 REQUIRED COMPONENTS Quick QuickControls2)

qt_standard_project_setup(REQUIRES 6.5)

# Указываем исполняемый файл
qt_add_executable(appViktoriia
    main.cpp
)


# Подключаем файлы QML
qt_add_qml_module(appViktoriia
    URI Viktoriia
    VERSION 1.0
    QML_FILES
        Views/main.qml
        Views/Login.qml
)

# Настройки для macOS/Windows
set_target_properties(appViktoriia PROPERTIES
    MACOSX_BUNDLE_BUNDLE_VERSION ${PROJECT_VERSION}
    MACOSX_BUNDLE_SHORT_VERSION_STRING ${PROJECT_VERSION_MAJOR}.${PROJECT_VERSION_MINOR}
    MACOSX_BUNDLE TRUE
    WIN32_EXECUTABLE TRUE
)

# Линковка библиотек
target_link_libraries(appViktoriia
    PRIVATE Qt6::Quick
    PRIVATE Qt6::QuickControls2
)

# Установка приложения
include(GNUInstallDirs)
install(TARGETS appViktoriia
    BUNDLE DESTINATION .
    LIBRARY DESTINATION ${CMAKE_INSTALL_LIBDIR}
    RUNTIME DESTINATION ${CMAKE_INSTALL_BINDIR}
)

cmake_minimum_required(VERSION 3.8)
project(Zdolshin LANGUAGES CXX)

add_subdirectory(RLBotCPP)

add_executable(Zdolshin main.cc zdolshin.cc zdolshin.h)
target_include_directories(Zdolshin PRIVATE RLBotCPP/inc RLBotCPP/lib/inc)

if (UNIX)
    target_link_libraries(Zdolshin RLBotCPP pthread)
else (UNIX)
    target_link_libraries(Zdolshin RLBotCPP)
endif (UNIX)

target_compile_features(Zdolshin PRIVATE cxx_std_17)

# Copy port config to output folder
add_custom_command(TARGET Zdolshin POST_BUILD
    COMMAND ${CMAKE_COMMAND} -E copy_if_different
        "${PROJECT_SOURCE_DIR}/port.cfg"
        $<TARGET_FILE_DIR:Zdolshin>)
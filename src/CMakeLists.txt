add_executable(${PROJECT_NAME})

target_sources(${PROJECT_NAME} PUBLIC
    base.cpp
)

target_link_libraries(${PROJECT_NAME}
    ${Boost_LIBRARIES}
)
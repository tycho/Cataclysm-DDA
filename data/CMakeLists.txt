set(CATACLYSM_DATA_DIRS
    ${CMAKE_SOURCE_DIR}/data/core
    ${CMAKE_SOURCE_DIR}/data/font
    ${CMAKE_SOURCE_DIR}/data/json
    ${CMAKE_SOURCE_DIR}/data/mods
    ${CMAKE_SOURCE_DIR}/data/names
    ${CMAKE_SOURCE_DIR}/data/raw
    ${CMAKE_SOURCE_DIR}/data/motd
    ${CMAKE_SOURCE_DIR}/data/credits
    ${CMAKE_SOURCE_DIR}/data/title
    ${CMAKE_SOURCE_DIR}/data/core
    ${CMAKE_SOURCE_DIR}/data/screenshots
    ${CMAKE_SOURCE_DIR}/data/xdg
    ${CMAKE_SOURCE_DIR}/data/help)

if (SOUND)
    list(APPEND CATACLYSM_DATA_DIRS ${CMAKE_SOURCE_DIR}/data/sound)
endif ()

set(CATACLYSM_DATA_FILES
        changelog.txt
        cataicon.ico
        fontdata.json)

file(COPY ${CATACLYSM_DATA_FILES} DESTINATION ${CMAKE_BINARY_DIR}/data)

if (RELEASE)
    install(DIRECTORY ${CATACLYSM_DATA_DIRS} TYPE DATA)
    install(FILES ${CATACLYSM_DATA_FILES} TYPE DATA)
endif ()

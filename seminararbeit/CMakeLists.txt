cmake_minimum_required(VERSION 3.15)
project(IT_GRC)
set(SEMINAR_FILE Thema_08_Heim_Maximilian_GRC-03_Seminararbeit)
add_custom_target(${SEMINAR_FILE}.tex
COMMAND ${CMAKE_COMMAND} -E copy ${CMAKE_CURRENT_SOURCE_DIR}/${SEMINAR_FILE}.tex ${CMAKE_BINARY_DIR})
add_custom_target(${SEMINAR_FILE}.pdf
latexmk -pdf ${SEMINAR_FILE}.tex
DEPENDS ${SEMINAR_FILE}.tex)
add_custom_target(seminararbeit
COMMAND ${CMAKE_COMMAND} -E copy ${CMAKE_CURRENT_BINARY_DIR}/${SEMINAR_FILE}.pdf ${CMAKE_CURRENT_SOURCE_DIR}/${SEMINAR_FILE}.pdf
DEPENDS ${SEMINAR_FILE}.pdf)
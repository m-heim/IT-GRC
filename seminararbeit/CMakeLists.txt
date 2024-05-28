cmake_minimum_required(VERSION 3.15)
project(IT_GRC)
set(FILES_PREFIX Thema_08_Heim_Maximilian_GRC-)
set(PAPER_IN ${FILES_PREFIX}03_Seminararbeit.tex)
set(PAPER_OUT ${FILES_PREFIX}04_Seminararbeit)
set(PRESENTATION_IN ${FILES_PREFIX}01_Seminarpraesentation.tex)
set(PRESENTATION_OUT ${FILES_PREFIX}02_Seminarpraesentation)
set(EXERCISES_IN ${FILES_PREFIX}05_Aufgabenblatt.tex)
set(EXERCISES_OUT ${FILES_PREFIX}06_Aufgabenblatt)
set(BIB_FILE bib.bib)

add_custom_target(${PRESENTATION_IN}
COMMAND ${CMAKE_COMMAND} -E copy ${CMAKE_CURRENT_SOURCE_DIR}/${PRESENTATION_IN} ${CMAKE_BINARY_DIR})
add_custom_target(${PAPER_IN}
COMMAND ${CMAKE_COMMAND} -E copy ${CMAKE_CURRENT_SOURCE_DIR}/${PAPER_IN} ${CMAKE_BINARY_DIR})
add_custom_target(${EXERCISES_IN}
COMMAND ${CMAKE_COMMAND} -E copy ${CMAKE_CURRENT_SOURCE_DIR}/${EXERCISES_IN} ${CMAKE_BINARY_DIR})

add_custom_target(${PAPER_OUT}
latexmk -pdf --jobname=${PAPER_OUT} ${PAPER_IN} 
DEPENDS ${PAPER_IN} prereq)
add_custom_target(${PRESENTATION_OUT}
latexmk -pdf --jobname=${PRESENTATION_OUT} ${PRESENTATION_IN} 
DEPENDS ${PRESENTATION_IN} prereq)
add_custom_target(${EXERCISES_OUT}
latexmk -pdf --jobname=${EXERCISES_OUT} ${EXERCISES_IN} 
DEPENDS ${EXERCISES_IN} prereq)

add_custom_target(assets
COMMAND ${CMAKE_COMMAND} -E copy_directory ${CMAKE_CURRENT_SOURCE_DIR}/assets ${CMAKE_CURRENT_BINARY_DIR}/assets
DEPENDS assets)

add_custom_target(${BIB_FILE}
COMMAND ${CMAKE_COMMAND} -E copy ${CMAKE_CURRENT_SOURCE_DIR}/${BIB_FILE} ${CMAKE_CURRENT_BINARY_DIR}/${BIB_FILE}
DEPENDS ${BIB_FILE})

add_custom_target(prereq
DEPENDS assets ${BIB_FILE})

add_custom_target(seminararbeit
COMMAND ${CMAKE_COMMAND} -E copy ${CMAKE_CURRENT_BINARY_DIR}/${PAPER_OUT}.pdf ${CMAKE_CURRENT_SOURCE_DIR}/${PAPER_OUT}.pdf
DEPENDS ${PAPER_OUT})
add_custom_target(praesentation
COMMAND ${CMAKE_COMMAND} -E copy ${CMAKE_CURRENT_BINARY_DIR}/${PRESENTATION_OUT}.pdf ${CMAKE_CURRENT_SOURCE_DIR}/${PRESENTATION_OUT}.pdf
DEPENDS ${PRESENTATION_OUT})
add_custom_target(aufgabenblatt
COMMAND ${CMAKE_COMMAND} -E copy ${CMAKE_CURRENT_BINARY_DIR}/${EXERCISES_OUT}.pdf ${CMAKE_CURRENT_SOURCE_DIR}/${EXERCISES_OUT}.pdf
DEPENDS ${EXERCISES_OUT})
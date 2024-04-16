cmake_minimum_required(VERSION 3.15)
project(semniararbeit_it_grc)
add_custom_target(seminararbeit.tex
COMMAND ${CMAKE_COMMAND} -E copy ${CMAKE_CURRENT_SOURCE_DIR}/seminararbeit.tex ${CMAKE_BINARY_DIR})
add_custom_target(seminararbeit.pdf
latexmk -pdf seminararbeit.tex
DEPENDS seminararbeit.tex)
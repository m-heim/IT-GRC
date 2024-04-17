cmake_minimum_required(VERSION 3.15)
project(IT_GRC)
add_custom_target(Thema_08_Heim_Maximilian_GRC-03_Seminararbeit.tex
COMMAND ${CMAKE_COMMAND} -E copy ${CMAKE_CURRENT_SOURCE_DIR}/Thema_08_Heim_Maximilian_GRC-03_Seminararbeit.tex ${CMAKE_BINARY_DIR})
add_custom_target(Thema_08_Heim_Maximilian_GRC-03_Seminararbeit.pdf
latexmk -pdf Thema_08_Heim_Maximilian_GRC-03_Seminararbeit.tex
DEPENDS Thema_08_Heim_Maximilian_GRC-03_Seminararbeit.tex)
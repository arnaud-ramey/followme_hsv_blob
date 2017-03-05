add_executable(blob_tracker.exe  blob_tracker.cpp)
target_link_libraries(blob_tracker.exe ${catkin_LIBRARIES}  ${OpenCV_LIBS})

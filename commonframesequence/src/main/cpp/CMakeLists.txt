cmake_minimum_required(VERSION 3.4.1)

find_library(log-lib  log)
find_library(jnigraphics-lib  jnigraphics)

add_library(framesequence SHARED
        BitmapDecoderJNI.cpp FrameSequence.cpp FrameSequenceJNI.cpp
        FrameSequence_gif.cpp JNIHelpers.cpp Registry.cpp Stream.cpp)
include_directories(gif/)

add_library(gif STATIC
        gif/dgif_lib.c  gif/egif_lib.c  gif/gifalloc.c  gif/gif_err.c  gif/gif_hash.c
        gif/openbsd-reallocarray.c  gif/quantize.c)

target_link_libraries(framesequence
        gif
        ${jnigraphics-lib}
        ${log-lib})
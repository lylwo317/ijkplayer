# For more information about using CMake with Android Studio, read the
# documentation: https://d.android.com/studio/projects/add-native-code.html

# Sets the minimum version of CMake required to build the native library.

cmake_minimum_required(VERSION 3.4.1)

project("ijkplayer")

add_definitions(-DANDROID -DNDEBUG)

set(IJK_PROF_PATH ${CMAKE_SOURCE_DIR}/../../../ijkprof/android-ndk-profiler-dummy/jni/)
set(IJK_MEDIA_PATH ${CMAKE_SOURCE_DIR}/../../../ijkmedia)
set(IJK_MEDIA_J4A_PATH ${IJK_MEDIA_PATH}/ijkj4a)
set(IJK_MEDIA_PLAYER_PATH ${IJK_MEDIA_PATH}/ijkplayer)
set(IJK_MEDIA_SDL_PATH ${IJK_MEDIA_PATH}/ijksdl)
set(IJK_MEDIA_SOUNDTOUCH_PATH ${IJK_MEDIA_PATH}/ijksoundtouch)
set(IJK_MEDIA_YUV_PATH ${IJK_MEDIA_PATH}/ijkyuv)

if (${ANDROID_ABI} STREQUAL armeabi-v7a)
    set(MY_APP_FFMPEG_OUTPUT_PATH ${CMAKE_SOURCE_DIR}/../../../android/contrib/build/ffmpeg-armv7a/output)
elseif (${ANDROID_ABI} STREQUAL armeabi)
    set(MY_APP_FFMPEG_OUTPUT_PATH ${CMAKE_SOURCE_DIR}/../../../android/contrib/build/ffmpeg-armv5/output)
elseif (${ANDROID_ABI} STREQUAL arm64-v8a)
    set(MY_APP_FFMPEG_OUTPUT_PATH ${CMAKE_SOURCE_DIR}/../../../android/contrib/build/ffmpeg-arm64/output)
elseif (${ANDROID_ABI} STREQUAL x86)
    set(MY_APP_FFMPEG_OUTPUT_PATH ${CMAKE_SOURCE_DIR}/../../../android/contrib/build/ffmpeg-x86/output)
elseif (${ANDROID_ABI} STREQUAL x86_64)
    set(MY_APP_FFMPEG_OUTPUT_PATH ${CMAKE_SOURCE_DIR}/../../../android/contrib/build/ffmpeg-x86_64/output)
endif ()


set(PROF_SRC
        ${IJK_PROF_PATH}/prof.c)

set(IJK_J4A_SRC
        ${IJK_MEDIA_J4A_PATH}/j4a/j4a_allclasses.c
        ${IJK_MEDIA_J4A_PATH}/j4a/j4a_base.c
        ${IJK_MEDIA_J4A_PATH}/j4a/class/android/media/AudioTrack.c
        ${IJK_MEDIA_J4A_PATH}/j4a/class/android/media/MediaCodec.c
        ${IJK_MEDIA_J4A_PATH}/j4a/class/android/media/MediaFormat.c
        ${IJK_MEDIA_J4A_PATH}/j4a/class/android/media/PlaybackParams.c
        ${IJK_MEDIA_J4A_PATH}/j4a/class/android/os/Build.c
        ${IJK_MEDIA_J4A_PATH}/j4a/class/android/os/Bundle.c
        ${IJK_MEDIA_J4A_PATH}/j4a/class/java/nio/Buffer.c
        ${IJK_MEDIA_J4A_PATH}/j4a/class/java/nio/ByteBuffer.c
        ${IJK_MEDIA_J4A_PATH}/j4a/class/java/util/ArrayList.c
        ${IJK_MEDIA_J4A_PATH}/j4a/class/tv/danmaku/ijk/media/player/misc/IMediaDataSource.c
        ${IJK_MEDIA_J4A_PATH}/j4a/class/tv/danmaku/ijk/media/player/misc/IAndroidIO.c
        ${IJK_MEDIA_J4A_PATH}/j4a/class/tv/danmaku/ijk/media/player/IjkMediaPlayer.c

        ${IJK_MEDIA_J4A_PATH}/j4au/class/android/media/AudioTrack.util.c
        ${IJK_MEDIA_J4A_PATH}/j4au/class/java/nio/ByteBuffer.util.c)

set(IJK_PLAYER_SRC
        #ijkplayer
        ${IJK_MEDIA_PLAYER_PATH}/ff_cmdutils.c
        ${IJK_MEDIA_PLAYER_PATH}/ff_ffplay.c
        ${IJK_MEDIA_PLAYER_PATH}/ff_ffpipeline.c
        ${IJK_MEDIA_PLAYER_PATH}/ff_ffpipenode.c
        ${IJK_MEDIA_PLAYER_PATH}/ijkmeta.c
        ${IJK_MEDIA_PLAYER_PATH}/ijkplayer.c

        ${IJK_MEDIA_PLAYER_PATH}/pipeline/ffpipeline_ffplay.c
        ${IJK_MEDIA_PLAYER_PATH}/pipeline/ffpipenode_ffplay_vdec.c

        ${IJK_MEDIA_PLAYER_PATH}/android/ffmpeg_api_jni.c
        ${IJK_MEDIA_PLAYER_PATH}/android/ijkplayer_android.c
        ${IJK_MEDIA_PLAYER_PATH}/android/ijkplayer_jni.c

        ${IJK_MEDIA_PLAYER_PATH}/android/pipeline/ffpipeline_android.c
        ${IJK_MEDIA_PLAYER_PATH}/android/pipeline/ffpipenode_android_mediacodec_vdec.c

        ${IJK_MEDIA_PLAYER_PATH}/ijkavformat/allformats.c
        ${IJK_MEDIA_PLAYER_PATH}/ijkavformat/cJSON.c
        ${IJK_MEDIA_PLAYER_PATH}/ijkavformat/ijklas.c
        ${IJK_MEDIA_PLAYER_PATH}/ijkavformat/ijklivehook.c
        ${IJK_MEDIA_PLAYER_PATH}/ijkavformat/ijkmediadatasource.c
        ${IJK_MEDIA_PLAYER_PATH}/ijkavformat/ijkio.c
        ${IJK_MEDIA_PLAYER_PATH}/ijkavformat/ijkiomanager.c
        ${IJK_MEDIA_PLAYER_PATH}/ijkavformat/ijkiocache.c
        ${IJK_MEDIA_PLAYER_PATH}/ijkavformat/ijkioffio.c
        ${IJK_MEDIA_PLAYER_PATH}/ijkavformat/ijkioandroidio.c
        ${IJK_MEDIA_PLAYER_PATH}/ijkavformat/ijkioprotocol.c
        ${IJK_MEDIA_PLAYER_PATH}/ijkavformat/ijkioapplication.c
        ${IJK_MEDIA_PLAYER_PATH}/ijkavformat/ijkiourlhook.c

        ${IJK_MEDIA_PLAYER_PATH}/ijkavformat/ijkasync.c
        ${IJK_MEDIA_PLAYER_PATH}/ijkavformat/ijkurlhook.c
        ${IJK_MEDIA_PLAYER_PATH}/ijkavformat/ijklongurl.c
        ${IJK_MEDIA_PLAYER_PATH}/ijkavformat/ijksegment.c

        ${IJK_MEDIA_PLAYER_PATH}/ijkavutil/ijkdict.c
        ${IJK_MEDIA_PLAYER_PATH}/ijkavutil/ijkutils.c
        ${IJK_MEDIA_PLAYER_PATH}/ijkavutil/ijkthreadpool.c
        ${IJK_MEDIA_PLAYER_PATH}/ijkavutil/ijktree.c
        ${IJK_MEDIA_PLAYER_PATH}/ijkavutil/ijkfifo.c
        ${IJK_MEDIA_PLAYER_PATH}/ijkavutil/ijkstl.cpp
        )

set(IJK_SDL_SRC
        ${IJK_MEDIA_SDL_PATH}/ijksdl_aout.c
        ${IJK_MEDIA_SDL_PATH}/ijksdl_audio.c
        ${IJK_MEDIA_SDL_PATH}/ijksdl_egl.c
        ${IJK_MEDIA_SDL_PATH}/ijksdl_error.c
        ${IJK_MEDIA_SDL_PATH}/ijksdl_mutex.c
        ${IJK_MEDIA_SDL_PATH}/ijksdl_stdinc.c
        ${IJK_MEDIA_SDL_PATH}/ijksdl_thread.c
        ${IJK_MEDIA_SDL_PATH}/ijksdl_timer.c
        ${IJK_MEDIA_SDL_PATH}/ijksdl_vout.c
        ${IJK_MEDIA_SDL_PATH}/ijksdl_extra_log.c
        ${IJK_MEDIA_SDL_PATH}/gles2/color.c
        ${IJK_MEDIA_SDL_PATH}/gles2/common.c
        ${IJK_MEDIA_SDL_PATH}/gles2/renderer.c
        ${IJK_MEDIA_SDL_PATH}/gles2/renderer_rgb.c
        ${IJK_MEDIA_SDL_PATH}/gles2/renderer_yuv420p.c
        ${IJK_MEDIA_SDL_PATH}/gles2/renderer_yuv444p10le.c
        ${IJK_MEDIA_SDL_PATH}/gles2/shader.c
        ${IJK_MEDIA_SDL_PATH}/gles2/fsh/rgb.fsh.c
        ${IJK_MEDIA_SDL_PATH}/gles2/fsh/yuv420p.fsh.c
        ${IJK_MEDIA_SDL_PATH}/gles2/fsh/yuv444p10le.fsh.c
        ${IJK_MEDIA_SDL_PATH}/gles2/vsh/mvp.vsh.c

        ${IJK_MEDIA_SDL_PATH}/dummy/ijksdl_vout_dummy.c

        ${IJK_MEDIA_SDL_PATH}/ffmpeg/ijksdl_vout_overlay_ffmpeg.c
        ${IJK_MEDIA_SDL_PATH}/ffmpeg/abi_all/image_convert.c

        ${IJK_MEDIA_SDL_PATH}/android/android_audiotrack.c
        ${IJK_MEDIA_SDL_PATH}/android/android_nativewindow.c
        ${IJK_MEDIA_SDL_PATH}/android/ijksdl_android_jni.c
        ${IJK_MEDIA_SDL_PATH}/android/ijksdl_aout_android_audiotrack.c
        ${IJK_MEDIA_SDL_PATH}/android/ijksdl_aout_android_opensles.c
        ${IJK_MEDIA_SDL_PATH}/android/ijksdl_codec_android_mediacodec_dummy.c
        ${IJK_MEDIA_SDL_PATH}/android/ijksdl_codec_android_mediacodec_internal.c
        ${IJK_MEDIA_SDL_PATH}/android/ijksdl_codec_android_mediacodec_java.c
        ${IJK_MEDIA_SDL_PATH}/android/ijksdl_codec_android_mediacodec.c
        ${IJK_MEDIA_SDL_PATH}/android/ijksdl_codec_android_mediadef.c
        ${IJK_MEDIA_SDL_PATH}/android/ijksdl_codec_android_mediaformat_java.c
        ${IJK_MEDIA_SDL_PATH}/android/ijksdl_codec_android_mediaformat.c
        ${IJK_MEDIA_SDL_PATH}/android/ijksdl_vout_android_nativewindow.c
        ${IJK_MEDIA_SDL_PATH}/android/ijksdl_vout_android_surface.c
        ${IJK_MEDIA_SDL_PATH}/android/ijksdl_vout_overlay_android_mediacodec.c
        )

set(IJK_SOUNDTOUCH_SRC
        ${IJK_MEDIA_SOUNDTOUCH_PATH}/source/SoundTouch/AAFilter.cpp
        ${IJK_MEDIA_SOUNDTOUCH_PATH}/source/SoundTouch/FIFOSampleBuffer.cpp
        ${IJK_MEDIA_SOUNDTOUCH_PATH}/source/SoundTouch/FIRFilter.cpp
        ${IJK_MEDIA_SOUNDTOUCH_PATH}/source/SoundTouch/cpu_detect_x86.cpp
        ${IJK_MEDIA_SOUNDTOUCH_PATH}/source/SoundTouch/sse_optimized.cpp
        ${IJK_MEDIA_SOUNDTOUCH_PATH}/source/SoundTouch/RateTransposer.cpp
        ${IJK_MEDIA_SOUNDTOUCH_PATH}/source/SoundTouch/InterpolateCubic.cpp
        ${IJK_MEDIA_SOUNDTOUCH_PATH}/source/SoundTouch/InterpolateLinear.cpp
        ${IJK_MEDIA_SOUNDTOUCH_PATH}/source/SoundTouch/InterpolateShannon.cpp
        ${IJK_MEDIA_SOUNDTOUCH_PATH}/source/SoundTouch/TDStretch.cpp
        ${IJK_MEDIA_SOUNDTOUCH_PATH}/source/SoundTouch/BPMDetect.cpp
        ${IJK_MEDIA_SOUNDTOUCH_PATH}/source/SoundTouch/PeakFinder.cpp
        ${IJK_MEDIA_SOUNDTOUCH_PATH}/source/SoundTouch/SoundTouch.cpp
        ${IJK_MEDIA_SOUNDTOUCH_PATH}/source/SoundTouch/mmx_optimized.cpp
        ${IJK_MEDIA_SOUNDTOUCH_PATH}/ijksoundtouch_wrap.cpp
        )

if (${ANDROID_ABI} STREQUAL armeabi-v7a)
    set(IJK_YUV_NEON_SRC
            ${IJK_MEDIA_YUV_PATH}/source/compare_neon.cc
            ${IJK_MEDIA_YUV_PATH}/source/rotate_neon.cc
            ${IJK_MEDIA_YUV_PATH}/source/row_neon.cc
            ${IJK_MEDIA_YUV_PATH}/source/scale_neon.cc
            )
elseif (${ANDROID_ABI} STREQUAL arm64-v8a)
    set(IJK_YUV_NEON_SRC
            ${IJK_MEDIA_YUV_PATH}/source/compare_neon64.cc
            ${IJK_MEDIA_YUV_PATH}/source/rotate_neon64.cc
            ${IJK_MEDIA_YUV_PATH}/source/row_neon64.cc
            ${IJK_MEDIA_YUV_PATH}/source/scale_neon64.cc
            )
else ()

endif ()


set(IJK_YUV_SRC
        ${IJK_MEDIA_YUV_PATH}/source/compare.cc
        ${IJK_MEDIA_YUV_PATH}/source/compare_common.cc
        ${IJK_MEDIA_YUV_PATH}/source/compare_posix.cc
        ${IJK_MEDIA_YUV_PATH}/source/convert.cc
        ${IJK_MEDIA_YUV_PATH}/source/convert_argb.cc
        ${IJK_MEDIA_YUV_PATH}/source/convert_from.cc
        ${IJK_MEDIA_YUV_PATH}/source/convert_from_argb.cc
        ${IJK_MEDIA_YUV_PATH}/source/convert_to_argb.cc
        ${IJK_MEDIA_YUV_PATH}/source/convert_to_i420.cc
        ${IJK_MEDIA_YUV_PATH}/source/cpu_id.cc
        ${IJK_MEDIA_YUV_PATH}/source/format_conversion.cc
        ${IJK_MEDIA_YUV_PATH}/source/planar_functions.cc
        ${IJK_MEDIA_YUV_PATH}/source/rotate.cc
        ${IJK_MEDIA_YUV_PATH}/source/rotate_argb.cc
        ${IJK_MEDIA_YUV_PATH}/source/rotate_mips.cc
        ${IJK_MEDIA_YUV_PATH}/source/row_any.cc
        ${IJK_MEDIA_YUV_PATH}/source/row_common.cc
        ${IJK_MEDIA_YUV_PATH}/source/row_mips.cc
        ${IJK_MEDIA_YUV_PATH}/source/row_posix.cc
        ${IJK_MEDIA_YUV_PATH}/source/scale.cc
        ${IJK_MEDIA_YUV_PATH}/source/scale_argb.cc
        ${IJK_MEDIA_YUV_PATH}/source/scale_common.cc
        ${IJK_MEDIA_YUV_PATH}/source/scale_mips.cc
        ${IJK_MEDIA_YUV_PATH}/source/scale_posix.cc
        ${IJK_MEDIA_YUV_PATH}/source/video_common.cc
        ${IJK_YUV_NEON_SRC}
        )
#copy ffmpeg
configure_file(${MY_APP_FFMPEG_OUTPUT_PATH}/libijkffmpeg.so ${CMAKE_SOURCE_DIR}/src/jniLibs/${ANDROID_ABI}/libijkffmpeg.so COPYONLY)

add_library(ijkffmpeg SHARED IMPORTED)
set_target_properties(ijkffmpeg PROPERTIES IMPORTED_LOCATION ${CMAKE_SOURCE_DIR}/src/jniLibs/${ANDROID_ABI}/libijkffmpeg.so)

find_library(log-lib log)
find_library(m-lib m)
find_library(z-lib z)
find_library(android-lib android)
find_library(EGL-lib EGL)
find_library(jnigraphics-lib jnigraphics)
find_library(GLES-lib GLESv2)
find_library(OpenSLES-lib OpenSLES)


include_directories(
        ${MY_APP_FFMPEG_OUTPUT_PATH}/include
        ${IJK_MEDIA_PATH}
        ${IJK_MEDIA_PATH}/ijkplayer
        ${IJK_MEDIA_PATH}/ijkj4a
        ${IJK_MEDIA_PATH}/ijksdl
        ${IJK_MEDIA_PATH}/ijksoundtouch
        ${IJK_MEDIA_PATH}/ijksoundtouch/include
        ${IJK_MEDIA_PATH}/ijkyuv
        ${IJK_MEDIA_PATH}/ijkyuv/include
)

add_library(ijksdl
        SHARED
        ${IJK_J4A_SRC}
        ${IJK_SDL_SRC}
        ${IJK_YUV_SRC}
        )


target_link_libraries( # Specifies the target library.
        ijksdl
        ijkffmpeg ${log-lib} ${android-lib} ${EGL-lib} ${GLES-lib} ${OpenSLES-lib})

add_library(ijkplayer
        SHARED
        ${PROF_SRC}
        ${IJK_PLAYER_SRC}
        ${IJK_SOUNDTOUCH_SRC}
        )

target_link_libraries( # Specifies the target library.
        ijkplayer
        ijksdl
        ijkffmpeg )
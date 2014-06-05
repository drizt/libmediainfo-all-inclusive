project(mediainfo)

cmake_minimum_required(VERSION 2.8)

set(MEDIAINFO_MAJOR_VERSION 0)
set(MEDIAINFO_MINOR_VERSION 7)
set(MEDIAINFO_PATCH_VERSION 69)
set(MEDIAINFO_VERSION ${MEDIAINFO_MAJOR_VERSION}.${MEDIAINFO_MINOR_VERSION}.${MEDIAINFO_PATCH_VERSION})

set(mediainfo_SOURCES_PATH ${CMAKE_CURRENT_SOURCE_DIR}/../../Source)
set(zlib_INCLUDE_PATH ${CMAKE_CURRENT_SOURCE_DIR}/../../../zlib)
set(zenlib_INCLUDE_PATH ${CMAKE_CURRENT_SOURCE_DIR}/../../../ZenLib/Source)

set(zlib_LIBRARY ${CMAKE_CURRENT_SOURCE_DIR}/../../../zlib/libzlib.a)
set(zenlib_LIBRARY ${CMAKE_CURRENT_SOURCE_DIR}/../../../ZenLib/Project/CMake/libzenlib.a)

include_directories(${mediainfo_SOURCES_PATH})
include_directories(${mediainfo_SOURCES_PATH}/ThirdParty/md5/)
include_directories(${mediainfo_SOURCES_PATH}/ThirdParty/tinyxml2/)
include_directories(${mediainfo_SOURCES_PATH}/ThirdParty/base64/)
include_directories(${zlib_INCLUDE_PATH})
include_directories(${zenlib_INCLUDE_PATH})

add_definitions(-DMEDIAINFO_LIBMMS_NO)
add_definitions(-DMEDIAINFO_LIBCURL_NO)
add_definitions(-DUNICODE)

set(mediainfo_PUBLIC_HDRS
  ${mediainfo_SOURCES_PATH}/MediaInfo/MediaInfo.h
  ${mediainfo_SOURCES_PATH}/MediaInfo/MediaInfoList.h
  ${mediainfo_SOURCES_PATH}/MediaInfo/MediaInfo_Const.h
  ${mediainfo_SOURCES_PATH}/MediaInfo/MediaInfo_Events.h
  ${mediainfo_SOURCES_PATH}/MediaInfoDLL/MediaInfoDLL.h
  ${mediainfo_SOURCES_PATH}/MediaInfoDLL/MediaInfoDLL_Static.h
)

set(mediainfo_SRCS
  ${mediainfo_SOURCES_PATH}/ThirdParty/tinyxml2/tinyxml2.cpp
  ${mediainfo_SOURCES_PATH}/ThirdParty/md5/md5.c
  ${mediainfo_SOURCES_PATH}/MediaInfo/File__Analyze.cpp
  ${mediainfo_SOURCES_PATH}/MediaInfo/File__Analyze_Buffer.cpp
  ${mediainfo_SOURCES_PATH}/MediaInfo/File__Analyze_Buffer_MinimizeSize.cpp
  ${mediainfo_SOURCES_PATH}/MediaInfo/File__Analyze_Streams.cpp
  ${mediainfo_SOURCES_PATH}/MediaInfo/File__Analyze_Streams_Finish.cpp
  ${mediainfo_SOURCES_PATH}/MediaInfo/File__Base.cpp
  ${mediainfo_SOURCES_PATH}/MediaInfo/File__MultipleParsing.cpp
  ${mediainfo_SOURCES_PATH}/MediaInfo/File__Duplicate.cpp
  ${mediainfo_SOURCES_PATH}/MediaInfo/File_Dummy.cpp
  ${mediainfo_SOURCES_PATH}/MediaInfo/File_Other.cpp
  ${mediainfo_SOURCES_PATH}/MediaInfo/File_Unknown.cpp
  ${mediainfo_SOURCES_PATH}/MediaInfo/MediaInfo.cpp
  ${mediainfo_SOURCES_PATH}/MediaInfo/MediaInfo_Config.cpp
  ${mediainfo_SOURCES_PATH}/MediaInfo/MediaInfo_Config_Automatic.cpp
  ${mediainfo_SOURCES_PATH}/MediaInfo/MediaInfo_Config_MediaInfo.cpp
  ${mediainfo_SOURCES_PATH}/MediaInfo/MediaInfo_Config_PerPackage.cpp
  ${mediainfo_SOURCES_PATH}/MediaInfo/MediaInfo_File.cpp
  ${mediainfo_SOURCES_PATH}/MediaInfo/MediaInfo_Inform.cpp
  ${mediainfo_SOURCES_PATH}/MediaInfo/MediaInfo_Internal.cpp
  ${mediainfo_SOURCES_PATH}/MediaInfo/MediaInfoList.cpp
  ${mediainfo_SOURCES_PATH}/MediaInfo/MediaInfoList_Internal.cpp
  ${mediainfo_SOURCES_PATH}/MediaInfo/TimeCode.cpp
  ${mediainfo_SOURCES_PATH}/MediaInfo/Archive/File_7z.cpp
  ${mediainfo_SOURCES_PATH}/MediaInfo/Archive/File_Ace.cpp
  ${mediainfo_SOURCES_PATH}/MediaInfo/Archive/File_Bzip2.cpp
  ${mediainfo_SOURCES_PATH}/MediaInfo/Archive/File_Elf.cpp
  ${mediainfo_SOURCES_PATH}/MediaInfo/Archive/File_Gzip.cpp
  ${mediainfo_SOURCES_PATH}/MediaInfo/Archive/File_Iso9660.cpp
  ${mediainfo_SOURCES_PATH}/MediaInfo/Archive/File_Mz.cpp
  ${mediainfo_SOURCES_PATH}/MediaInfo/Archive/File_Rar.cpp
  ${mediainfo_SOURCES_PATH}/MediaInfo/Archive/File_Tar.cpp
  ${mediainfo_SOURCES_PATH}/MediaInfo/Archive/File_Zip.cpp
  ${mediainfo_SOURCES_PATH}/MediaInfo/Audio/File_Aac.cpp
  ${mediainfo_SOURCES_PATH}/MediaInfo/Audio/File_Aac_GeneralAudio.cpp
  ${mediainfo_SOURCES_PATH}/MediaInfo/Audio/File_Aac_GeneralAudio_Sbr.cpp
  ${mediainfo_SOURCES_PATH}/MediaInfo/Audio/File_Aac_GeneralAudio_Sbr_Ps.cpp
  ${mediainfo_SOURCES_PATH}/MediaInfo/Audio/File_Aac_Main.cpp
  ${mediainfo_SOURCES_PATH}/MediaInfo/Audio/File_Aac_Others.cpp
  ${mediainfo_SOURCES_PATH}/MediaInfo/Audio/File_Ac3.cpp
  ${mediainfo_SOURCES_PATH}/MediaInfo/Audio/File_Adpcm.cpp
  ${mediainfo_SOURCES_PATH}/MediaInfo/Audio/File_Als.cpp
  ${mediainfo_SOURCES_PATH}/MediaInfo/Audio/File_Amr.cpp
  ${mediainfo_SOURCES_PATH}/MediaInfo/Audio/File_Amv.cpp
  ${mediainfo_SOURCES_PATH}/MediaInfo/Audio/File_Ape.cpp
  ${mediainfo_SOURCES_PATH}/MediaInfo/Audio/File_Au.cpp
  ${mediainfo_SOURCES_PATH}/MediaInfo/Audio/File_Celt.cpp
  ${mediainfo_SOURCES_PATH}/MediaInfo/Audio/File_ChannelGrouping.cpp
  ${mediainfo_SOURCES_PATH}/MediaInfo/Audio/File_Dts.cpp
  ${mediainfo_SOURCES_PATH}/MediaInfo/Audio/File_DolbyE.cpp
  ${mediainfo_SOURCES_PATH}/MediaInfo/Audio/File_ExtendedModule.cpp
  ${mediainfo_SOURCES_PATH}/MediaInfo/Audio/File_Flac.cpp
  ${mediainfo_SOURCES_PATH}/MediaInfo/Audio/File_ImpulseTracker.cpp
  ${mediainfo_SOURCES_PATH}/MediaInfo/Audio/File_La.cpp
  ${mediainfo_SOURCES_PATH}/MediaInfo/Audio/File_Midi.cpp
  ${mediainfo_SOURCES_PATH}/MediaInfo/Audio/File_Module.cpp
  ${mediainfo_SOURCES_PATH}/MediaInfo/Audio/File_Mpc.cpp
  ${mediainfo_SOURCES_PATH}/MediaInfo/Audio/File_MpcSv8.cpp
  ${mediainfo_SOURCES_PATH}/MediaInfo/Audio/File_Mpega.cpp
  ${mediainfo_SOURCES_PATH}/MediaInfo/Audio/File_OpenMG.cpp
  ${mediainfo_SOURCES_PATH}/MediaInfo/Audio/File_Opus.cpp
  ${mediainfo_SOURCES_PATH}/MediaInfo/Audio/File_Pcm.cpp
  ${mediainfo_SOURCES_PATH}/MediaInfo/Audio/File_Pcm_M2ts.cpp
  ${mediainfo_SOURCES_PATH}/MediaInfo/Audio/File_Pcm_Vob.cpp
  ${mediainfo_SOURCES_PATH}/MediaInfo/Audio/File_Ps2Audio.cpp
  ${mediainfo_SOURCES_PATH}/MediaInfo/Audio/File_Rkau.cpp
  ${mediainfo_SOURCES_PATH}/MediaInfo/Audio/File_ScreamTracker3.cpp
  ${mediainfo_SOURCES_PATH}/MediaInfo/Audio/File_SmpteSt0302.cpp
  ${mediainfo_SOURCES_PATH}/MediaInfo/Audio/File_SmpteSt0337.cpp
  ${mediainfo_SOURCES_PATH}/MediaInfo/Audio/File_SmpteSt0331.cpp
  ${mediainfo_SOURCES_PATH}/MediaInfo/Audio/File_Speex.cpp
  ${mediainfo_SOURCES_PATH}/MediaInfo/Audio/File_Tak.cpp
  ${mediainfo_SOURCES_PATH}/MediaInfo/Audio/File_Tta.cpp
  ${mediainfo_SOURCES_PATH}/MediaInfo/Audio/File_TwinVQ.cpp
  ${mediainfo_SOURCES_PATH}/MediaInfo/Audio/File_Vorbis.cpp
  ${mediainfo_SOURCES_PATH}/MediaInfo/Audio/File_Wvpk.cpp
  ${mediainfo_SOURCES_PATH}/MediaInfo/Duplicate/File__Duplicate__Base.cpp
  ${mediainfo_SOURCES_PATH}/MediaInfo/Duplicate/File__Duplicate__Writer.cpp
  ${mediainfo_SOURCES_PATH}/MediaInfo/Duplicate/File__Duplicate_MpegTs.cpp
  ${mediainfo_SOURCES_PATH}/MediaInfo/Export/Export_EbuCore.cpp
  ${mediainfo_SOURCES_PATH}/MediaInfo/Export/Export_Mpeg7.cpp
  ${mediainfo_SOURCES_PATH}/MediaInfo/Export/Export_PBCore.cpp
  ${mediainfo_SOURCES_PATH}/MediaInfo/Export/Export_reVTMD.cpp
  ${mediainfo_SOURCES_PATH}/MediaInfo/Image/File_ArriRaw.cpp
  ${mediainfo_SOURCES_PATH}/MediaInfo/Image/File_Bmp.cpp
  ${mediainfo_SOURCES_PATH}/MediaInfo/Image/File_Dds.cpp
  ${mediainfo_SOURCES_PATH}/MediaInfo/Image/File_Dpx.cpp
  ${mediainfo_SOURCES_PATH}/MediaInfo/Image/File_Exr.cpp
  ${mediainfo_SOURCES_PATH}/MediaInfo/Image/File_Gif.cpp
  ${mediainfo_SOURCES_PATH}/MediaInfo/Image/File_Ico.cpp
  ${mediainfo_SOURCES_PATH}/MediaInfo/Image/File_Jpeg.cpp
  ${mediainfo_SOURCES_PATH}/MediaInfo/Image/File_Pcx.cpp
  ${mediainfo_SOURCES_PATH}/MediaInfo/Image/File_Png.cpp
  ${mediainfo_SOURCES_PATH}/MediaInfo/Image/File_Psd.cpp
  ${mediainfo_SOURCES_PATH}/MediaInfo/Image/File_Rle.cpp
  ${mediainfo_SOURCES_PATH}/MediaInfo/Image/File_Tiff.cpp
  ${mediainfo_SOURCES_PATH}/MediaInfo/Image/File_Tga.cpp
  ${mediainfo_SOURCES_PATH}/MediaInfo/Multiple/File__ReferenceFilesHelper.cpp
  ${mediainfo_SOURCES_PATH}/MediaInfo/Multiple/File_Aaf.cpp
  ${mediainfo_SOURCES_PATH}/MediaInfo/Multiple/File_Ancillary.cpp
  ${mediainfo_SOURCES_PATH}/MediaInfo/Multiple/File_Bdmv.cpp
  ${mediainfo_SOURCES_PATH}/MediaInfo/Multiple/File_Cdxa.cpp
  ${mediainfo_SOURCES_PATH}/MediaInfo/Multiple/File_DashMpd.cpp
  ${mediainfo_SOURCES_PATH}/MediaInfo/Multiple/File_DcpAm.cpp
  ${mediainfo_SOURCES_PATH}/MediaInfo/Multiple/File_DcpCpl.cpp
  ${mediainfo_SOURCES_PATH}/MediaInfo/Multiple/File_DcpPkl.cpp
  ${mediainfo_SOURCES_PATH}/MediaInfo/Multiple/File_Dpg.cpp
  ${mediainfo_SOURCES_PATH}/MediaInfo/Multiple/File_DvDif.cpp
  ${mediainfo_SOURCES_PATH}/MediaInfo/Multiple/File_DvDif_Analysis.cpp
  ${mediainfo_SOURCES_PATH}/MediaInfo/Multiple/File_Dvdv.cpp
  ${mediainfo_SOURCES_PATH}/MediaInfo/Multiple/File_Dxw.cpp
  ${mediainfo_SOURCES_PATH}/MediaInfo/Multiple/File_Flv.cpp
  ${mediainfo_SOURCES_PATH}/MediaInfo/Multiple/File_Gxf.cpp
  ${mediainfo_SOURCES_PATH}/MediaInfo/Multiple/File_HdsF4m.cpp
  ${mediainfo_SOURCES_PATH}/MediaInfo/Multiple/File_Hls.cpp
  ${mediainfo_SOURCES_PATH}/MediaInfo/Multiple/File_Gxf.cpp
  ${mediainfo_SOURCES_PATH}/MediaInfo/Multiple/File_Gxf_TimeCode.cpp
  ${mediainfo_SOURCES_PATH}/MediaInfo/Multiple/File_Ibi.cpp
  ${mediainfo_SOURCES_PATH}/MediaInfo/Multiple/File_Ibi_Creation.cpp
  ${mediainfo_SOURCES_PATH}/MediaInfo/Multiple/File_Ism.cpp
  ${mediainfo_SOURCES_PATH}/MediaInfo/Multiple/File_Ivf.cpp
  ${mediainfo_SOURCES_PATH}/MediaInfo/Multiple/File_Lxf.cpp
  ${mediainfo_SOURCES_PATH}/MediaInfo/Multiple/File_Mk.cpp
  ${mediainfo_SOURCES_PATH}/MediaInfo/Multiple/File_Mpeg4.cpp
  ${mediainfo_SOURCES_PATH}/MediaInfo/Multiple/File_Mpeg4_Descriptors.cpp
  ${mediainfo_SOURCES_PATH}/MediaInfo/Multiple/File_Mpeg4_Elements.cpp
  ${mediainfo_SOURCES_PATH}/MediaInfo/Multiple/File_Mpeg4_TimeCode.cpp
  ${mediainfo_SOURCES_PATH}/MediaInfo/Multiple/File_Mpeg_Descriptors.cpp
  ${mediainfo_SOURCES_PATH}/MediaInfo/Multiple/File_Mpeg_Psi.cpp
  ${mediainfo_SOURCES_PATH}/MediaInfo/Multiple/File_MpegPs.cpp
  ${mediainfo_SOURCES_PATH}/MediaInfo/Multiple/File_MpegTs.cpp
  ${mediainfo_SOURCES_PATH}/MediaInfo/Multiple/File_MpegTs_Duplicate.cpp
  ${mediainfo_SOURCES_PATH}/MediaInfo/Multiple/File_Mxf.cpp
  ${mediainfo_SOURCES_PATH}/MediaInfo/Multiple/File_Nut.cpp
  ${mediainfo_SOURCES_PATH}/MediaInfo/Multiple/File_Ogg.cpp
  ${mediainfo_SOURCES_PATH}/MediaInfo/Multiple/File_Ogg_SubElement.cpp
  ${mediainfo_SOURCES_PATH}/MediaInfo/Multiple/File_P2_Clip.cpp
  ${mediainfo_SOURCES_PATH}/MediaInfo/Multiple/File_Pmp.cpp
  ${mediainfo_SOURCES_PATH}/MediaInfo/Multiple/File_Ptx.cpp
  ${mediainfo_SOURCES_PATH}/MediaInfo/Multiple/File_Riff.cpp
  ${mediainfo_SOURCES_PATH}/MediaInfo/Multiple/File_Riff_Elements.cpp
  ${mediainfo_SOURCES_PATH}/MediaInfo/Multiple/File_Rm.cpp
  ${mediainfo_SOURCES_PATH}/MediaInfo/Multiple/File_SequenceInfo.cpp
  ${mediainfo_SOURCES_PATH}/MediaInfo/Multiple/File_Skm.cpp
  ${mediainfo_SOURCES_PATH}/MediaInfo/Multiple/File_Swf.cpp
  ${mediainfo_SOURCES_PATH}/MediaInfo/Multiple/File_Umf.cpp
  ${mediainfo_SOURCES_PATH}/MediaInfo/Multiple/File_Wm.cpp
  ${mediainfo_SOURCES_PATH}/MediaInfo/Multiple/File_Wm_Elements.cpp
  ${mediainfo_SOURCES_PATH}/MediaInfo/Multiple/File_Xdcam_Clip.cpp
  ${mediainfo_SOURCES_PATH}/MediaInfo/Reader/Reader_Directory.cpp
  ${mediainfo_SOURCES_PATH}/MediaInfo/Reader/Reader_File.cpp
  ${mediainfo_SOURCES_PATH}/MediaInfo/Reader/Reader_libcurl.cpp
  ${mediainfo_SOURCES_PATH}/MediaInfo/Reader/Reader_libmms.cpp
  ${mediainfo_SOURCES_PATH}/MediaInfo/Tag/File__Tags.cpp
  ${mediainfo_SOURCES_PATH}/MediaInfo/Tag/File_ApeTag.cpp
  ${mediainfo_SOURCES_PATH}/MediaInfo/Tag/File_Id3.cpp
  ${mediainfo_SOURCES_PATH}/MediaInfo/Tag/File_Id3v2.cpp
  ${mediainfo_SOURCES_PATH}/MediaInfo/Tag/File_Lyrics3.cpp
  ${mediainfo_SOURCES_PATH}/MediaInfo/Tag/File_Lyrics3v2.cpp
  ${mediainfo_SOURCES_PATH}/MediaInfo/Tag/File_VorbisCom.cpp
  ${mediainfo_SOURCES_PATH}/MediaInfo/Text/File_AribStdB24B37.cpp
  ${mediainfo_SOURCES_PATH}/MediaInfo/Text/File_Cdp.cpp
  ${mediainfo_SOURCES_PATH}/MediaInfo/Text/File_Cmml.cpp
  ${mediainfo_SOURCES_PATH}/MediaInfo/Text/File_DvbSubtitle.cpp
  ${mediainfo_SOURCES_PATH}/MediaInfo/Text/File_DtvccTransport.cpp
  ${mediainfo_SOURCES_PATH}/MediaInfo/Text/File_Eia608.cpp
  ${mediainfo_SOURCES_PATH}/MediaInfo/Text/File_Eia708.cpp
  ${mediainfo_SOURCES_PATH}/MediaInfo/Text/File_Kate.cpp
  ${mediainfo_SOURCES_PATH}/MediaInfo/Text/File_N19.cpp
  ${mediainfo_SOURCES_PATH}/MediaInfo/Text/File_OtherText.cpp
  ${mediainfo_SOURCES_PATH}/MediaInfo/Text/File_Pgs.cpp
  ${mediainfo_SOURCES_PATH}/MediaInfo/Text/File_Scc.cpp
  ${mediainfo_SOURCES_PATH}/MediaInfo/Text/File_Scte20.cpp
  ${mediainfo_SOURCES_PATH}/MediaInfo/Text/File_SubRip.cpp
  ${mediainfo_SOURCES_PATH}/MediaInfo/Text/File_Teletext.cpp
  ${mediainfo_SOURCES_PATH}/MediaInfo/Text/File_TimedText.cpp
  ${mediainfo_SOURCES_PATH}/MediaInfo/Text/File_Ttml.cpp
  ${mediainfo_SOURCES_PATH}/MediaInfo/Video/File_Aic.cpp
  ${mediainfo_SOURCES_PATH}/MediaInfo/Video/File_AfdBarData.cpp
  ${mediainfo_SOURCES_PATH}/MediaInfo/Video/File_Avc.cpp
  ${mediainfo_SOURCES_PATH}/MediaInfo/Video/File_Avc_Duplicate.cpp
  ${mediainfo_SOURCES_PATH}/MediaInfo/Video/File_AvsV.cpp
  ${mediainfo_SOURCES_PATH}/MediaInfo/Video/File_Canopus.cpp
  ${mediainfo_SOURCES_PATH}/MediaInfo/Video/File_Dirac.cpp
  ${mediainfo_SOURCES_PATH}/MediaInfo/Video/File_Flic.cpp
  ${mediainfo_SOURCES_PATH}/MediaInfo/Video/File_Fraps.cpp
  ${mediainfo_SOURCES_PATH}/MediaInfo/Video/File_H263.cpp
  ${mediainfo_SOURCES_PATH}/MediaInfo/Video/File_Hevc.cpp
  ${mediainfo_SOURCES_PATH}/MediaInfo/Video/File_Lagarith.cpp
  ${mediainfo_SOURCES_PATH}/MediaInfo/Video/File_Mpeg4v.cpp
  ${mediainfo_SOURCES_PATH}/MediaInfo/Video/File_Mpegv.cpp
  ${mediainfo_SOURCES_PATH}/MediaInfo/Video/File_ProRes.cpp
  ${mediainfo_SOURCES_PATH}/MediaInfo/Video/File_Theora.cpp
  ${mediainfo_SOURCES_PATH}/MediaInfo/Video/File_Vc1.cpp
  ${mediainfo_SOURCES_PATH}/MediaInfo/Video/File_Vc3.cpp
  ${mediainfo_SOURCES_PATH}/MediaInfo/Video/File_Vp8.cpp
  ${mediainfo_SOURCES_PATH}/MediaInfo/Video/File_Y4m.cpp
  ${mediainfo_SOURCES_PATH}/MediaInfoDLL/MediaInfoDLL.cpp
  ${mediainfo_SOURCES_PATH}/MediaInfoDLL/MediaInfoDLL.def
)

add_library(mediainfo STATIC ${mediainfo_SRCS})

# target_link_libraries(mediainfo
# 	${zenlib_LIBRARY}
# 	${zlib_LIBARY}
# )

set_target_properties(mediainfo PROPERTIES
	VERSION ${MEDIAINFO_VERSION}
	SOVERSION ${MEDIAINFO_MAJOR_VERSION}
)

install(TARGETS mediainfo
  RUNTIME DESTINATION bin
  ARCHIVE DESTINATION lib
  LIBRARY DESTINATION lib )

foreach(HEADER ${mediainfo_PUBLIC_HDRS})
  string(REPLACE ${mediainfo_SOURCES_PATH} "" DIR ${HEADER})
  string(REGEX REPLACE "/[^/]*$" "" DIR ${DIR})
  install(FILES ${HEADER} DESTINATION include/${DIR})
endforeach(HEADER ${mediainfo_PUBLIC_HDRS})

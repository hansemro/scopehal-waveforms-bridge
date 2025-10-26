###############################################################################
#C++ compilation
add_executable(wfmserver
	DigilentSCPIServer.cpp
	WaveformServerThread.cpp
	main.cpp
)

#Locate Digilent WaveForms Library
if(WIN32)
	set(WAVEFORMS_SDK_PATH "C:/Program Files (x86)/Digilent/WaveFormsSDK")
	add_library(dwf UNKNOWN IMPORTED)
	# TODO: support ARM64, x86 targets
	set_target_properties(dwf PROPERTIES
		IMPORTED_LOCATION "${WAVEFORMS_SDK_PATH}/lib/x64/dwf.lib"
		INTERFACE_INCLUDE_DIRECTORIES "${WAVEFORMS_SDK_PATH}/inc")
endif()

###############################################################################
#Linker settings
target_link_libraries(wfmserver
	xptools
	log
	dwf
	scpi-server-tools
	)


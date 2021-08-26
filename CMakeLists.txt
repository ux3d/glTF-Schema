	project(glTF-Schema)
    
    # generate glTF json schema include file
	file(GLOB_RECURSE gltf_schema_files RELATIVE "${CMAKE_CURRENT_SOURCE_DIR}" "*.schema.json")

	set(combined_schemas "")
	foreach(gltf_schema_file IN LISTS gltf_schema_files)
		file(READ "${CMAKE_CURRENT_SOURCE_DIR}/${gltf_schema_file}" content)
		if(NOT combined_schemas STREQUAL "")
			string(APPEND combined_schemas ",\n")
		endif()
		get_filename_component(file_name ${gltf_schema_file} NAME)
		string(APPEND combined_schemas "\"${file_name}\" : ${content}")
	endforeach()

	set(generated_file "#pragma once\nconst auto gltfSchemas = R\"gltf(\n{\n${combined_schemas}\n})gltf\";")
	file(WRITE "${CMAKE_CURRENT_BINARY_DIR}/include/gltf_schema/gltf_single_json.h" "${generated_file}")
	project(glTF-Schema)
    
    # generate glTF json schema include file
	file(GLOB_RECURSE gltf_schema_files RELATIVE "${CMAKE_CURRENT_SOURCE_DIR}" "*.schema.json")

	set(combined_schemas "")
	foreach(gltf_schema_file IN LISTS gltf_schema_files)
		file(READ "${CMAKE_CURRENT_SOURCE_DIR}/${gltf_schema_file}" content)
		get_filename_component(file_name ${gltf_schema_file} NAME)
		string(APPEND combined_schemas "\"${file_name}\",\nR\"gltf(${content})gltf\",\n")
	endforeach()

	set(generated_file "#pragma once\n#include <nlohmann/json.hpp>\nnamespace gltf_schema {\n\n\ninline nlohmann::json merged() {\n	   static const std::string gltfSchemaArray[] = {${combined_schemas}};\n    auto gltfSchemas = nlohmann::json::object();\n    for (int i = 0; i < sizeof(gltfSchemaArray) / sizeof(*gltfSchemaArray); i=i+2) {\n        auto partSchema = nlohmann::json::parse(gltfSchemaArray[i+1]);\n        gltfSchemas[gltfSchemaArray[i]] = partSchema;\n   }\n    return gltfSchemas;\n}\n}\n")
	file(WRITE "${CMAKE_CURRENT_BINARY_DIR}/include/gltf_schema/gltf_single_json.h" "${generated_file}")
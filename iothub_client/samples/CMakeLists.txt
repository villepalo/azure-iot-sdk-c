#Copyright (c) Microsoft. All rights reserved.
#Licensed under the MIT license. See LICENSE file in the project root for full license information.

#this is CMakeLists.txt for samples. There's noithig here, except redirections to 
#individual protocol samples

usePermissiveRulesForSdkSamplesAndTests()

function(add_sample_directory whatIsBuilding)
    add_subdirectory(${whatIsBuilding})

    set_target_properties(${whatIsBuilding}
               PROPERTIES
               FOLDER "IoTHub_Samples")
endfunction()

add_sample_directory(iothub_convenience_sample)
add_sample_directory(iothub_ll_c2d_sample)
add_sample_directory(iothub_ll_client_x509_sample)
add_sample_directory(iothub_ll_telemetry_sample)

if(${use_http})
    add_sample_directory(iothub_client_sample_http_shared)
    if(NOT ${dont_use_uploadtoblob})
        add_sample_directory(iothub_client_sample_upload_to_blob)
        add_sample_directory(iothub_client_sample_upload_to_blob_mb)
    endif()
endif()

if(${use_mqtt})
    if(LINUX)
        add_sample_directory(iothub_client_sample_mqtt_dm)
    endif()
endif()

if(${use_amqp})
    add_sample_directory(iothub_client_sample_amqp_shared)
    add_sample_directory(iothub_ll_client_sample_amqp_shared)
    
    add_sample_directory(iothub_client_sample_amqp_websockets_shared)
    add_sample_directory(iothub_client_sample_amqp_shared_ws_methods)
endif()

if(${use_amqp} OR ${use_mqtt})
    add_sample_directory(iothub_client_sample_device_method)
    add_sample_directory(iothub_client_sample_device_twin)
endif()

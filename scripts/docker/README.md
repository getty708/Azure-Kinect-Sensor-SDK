# Build "examples/fastpointcloud"


## apt でインストール
```bash
curl -sSL https://packages.microsoft.com/keys/microsoft.asc | apt-key add -
apt-add-repository https://packages.microsoft.com/ubuntu/18.04/prod
apt-get update
apt install k4a-tools
```

```bash
apt-get update
apt-get install libturbojpeg
```


## Sourceからビルド

```bash
apt install k4a-tools
mkdir build && cd $_
cmake .. -GNinja -DCMAKE_BUILD_TYPE=Debug
ninja
tree ./bin
```

これでビルドはできた．

```bash
root@2f587a19cd72:~/Azure-Kinect-Sensor-SDK/build/bin# ./transformation_example -h
Usage: transformation_example capture <output_directory> [device_id]
Usage: transformation_example playback <filename.mkv> [timestamp (ms)] [output_file]
[2021-11-11 09:11:33.522] [error] [t=4096] ../src/dynlib/dynlib_linux.c (82): dynlib_create(). Failed to load shared object libdepthengine.so.2.0 with error: libdepthengine.so.2.0: cannot open shared object file: No such file or directory
[2021-11-11 09:11:33.522] [error] [t=4096] ../src/deloader/deloader.cpp (75): deloader_init_once(). Failed to Load Depth Engine Plugin (depthengine). Depth functionality will not work
[2021-11-11 09:11:33.522] [error] [t=4096] ../src/deloader/deloader.cpp (76): deloader_init_once(). Make sure the depth engine plugin is in your loaders path
root@2f587a19cd72:~/Azure-Kinect-Sensor-SDK/build/bin# ./transformation_example playback ../../dataStore/20211014_U0001_S0500_kinect.mkv 2000 ../../dataStore/outputs/out.ply  
Seeking to timestamp: 2000/1768400 (ms)
[2021-11-11 09:28:38.057] [error] [t=4098] ../src/dynlib/dynlib_linux.c (82): dynlib_create(). Failed to load shared object libdepthengine.so.2.0 with error: libdepthengine.so.2.0: cannot open shared object file: No such file or directory
[2021-11-11 09:28:38.057] [error] [t=4098] ../src/deloader/deloader.cpp (75): deloader_init_once(). Failed to Load Depth Engine Plugin (depthengine). Depth functionality will not work
[2021-11-11 09:28:38.057] [error] [t=4098] ../src/deloader/deloader.cpp (76): deloader_init_once(). Make sure the depth engine plugin is in your loaders path
[2021-11-11 09:28:38.057] [error] [t=4098] ../src/deloader/deloader.cpp (186): deloader_transform_engine_create_and_initialize(). Failed to load depth engine plugin
[2021-11-11 09:28:38.057] [error] [t=4098] ../src/tewrapper/tewrapper.c (61): transform_engine_start_helper(). Transform engine create and initialize failed with error code: 108.
[2021-11-11 09:28:38.057] [error] [t=4098] ../src/tewrapper/tewrapper.c (68): teresult == K4A_DEPTH_ENGINE_RESULT_SUCCEEDED returned failure in transform_engine_start_helper()
[2021-11-11 09:28:38.057] [error] [t=4098] ../src/tewrapper/tewrapper.c (86): transform_engine_start_helper(tewrapper) returned failure in transform_engine_thread()
[2021-11-11 09:28:38.057] [error] [t=4097] ../src/tewrapper/tewrapper.c (313): tewrapper_create(). Transform Engine thread failed to start
[2021-11-11 09:28:38.057] [error] [t=4097] ../src/transformation/transformation.c (637): transformation_context->tewrapper != NULL returned failure in transformation_create()
[2021-11-11 09:28:38.064] [error] [t=4097] ../src/transformation/transformation.c (584): k4a_transformation_t_get_context(). Invalid k4a_transformation_t (nil)
[2021-11-11 09:28:38.064] [error] [t=4097] ../src/transformation/transformation.c (688): Invalid argument to transformation_depth_image_to_color_camera_custom(). transformation_handle ((nil)) is not a valid handle of type k4a_transformation_t
[2021-11-11 09:28:38.064] [error] [t=4097] ../src/sdk/k4a.c (1201): transformation_depth_image_to_color_camera_custom(transformation_handle, depth_image_buffer, &depth_image_descriptor, custom_image_buffer, &dummy_descriptor, transformed_depth_image_buffer, &transformed_depth_image_descriptor, transformed_custom_image_buffer, &dummy_descriptor, interpolation_type, invalid_custom_value) returned failure in k4a_transformation_depth_image_to_color_camera()
Failed to compute transformed depth image
Failed to transform depth to color
```

## Example
Exampleを個別にビルドするためには，CMakeList.txt を編集することが必要


## Reference

- [ROS勉強記録 - Azure Kinect DK使ってみた](http://ros-robot.blogspot.com/2020/03/azure-kinect-dk.html)
- [Azure Kinect Sensor SDKをUbuntu Linuxでビルドしてみる](https://qiita.com/bathtimefish/items/258ac1104ecb00826e9b)


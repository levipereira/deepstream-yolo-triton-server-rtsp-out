# Sample Application `deepstream-yolo-triton-server-rtsp-out`  

The Purpose of this repository is to create a Deepstream/Triton-Server sample application that utilizes yolov7, yolov7_qat, yolov9 models to perform inference on video files or RTSP streams. It then showcases the output on an RTSP URL, providing a straightforward demonstration of end-to-end AI processing.

Follow this steps to Use this Sample App

### 1. Deploy and Start Triton Server

Follow the steps on below link to Start Triton Server<br>
[Triton Server - yolov9.](https://github.com/levipereira/docker_images/triton-server-yolov9)


### 2. Deploy and Start Deepstream 
Follow the steps on below link to Start Deepstream<br>
[Deepstream - yolov9.](https://github.com/levipereira/docker_images/deepstream-yolov9)


### 3. Using Sample Application `deepstream-yolo-triton-server-rtsp-out`  

To use this sample application, follow the steps below from within the container:

The sample application is installed on `/deepstream_python_apps/apps/deepstream-yolo-triton-server-rtsp-out/`

This sample application supports input streaming from both `file://` and `rtsp://` sources. It processes the input and streams the output via RTSP at the following URL: `rtsp://localhost:8554/ds-test`

```bash
python3 deepstream_yolo-triton-server_rtsp_out.py -i <input_files> -m <model> -c <codec> -b <bitrate> [--rtsp-ts]

#example
python3 deepstream_yolov9-triton-server_rtsp_out.py  \
-i file:///videos/input.mp4 rtsp://myserver:554  \
-m  yolov9-c-converted \
-c H264   
```


### Arguments 
*   `-i`, `--input`: Path to input `file://` or `rtsp://` elementary stream. Multiple input files can be provided.
*   `-m`, `--model`: Choice  ['yolov7','yolov7_qat','yolov9-c','yolov9-e','yolov9-c-converted', 'yolov9-e-converted','gelan-c','gelan-e']. 
*   `-c`, `--codec`: RTSP Streaming Codec. Choose between H264 and H265. (Default: H264)
*   `-b`, `--bitrate`: Set the encoding bitrate. (Default: 4000000)
*   `--rtsp-ts`: Attach NTP timestamp from RTSP source. (Default: False)

<br><br><br> 



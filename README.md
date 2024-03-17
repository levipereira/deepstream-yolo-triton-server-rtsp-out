# Sample App Nvidia DeepStream - Triton-Server (YOLO Models)

The Purpose of this repository is to create a DeepStream/Triton-Server sample application that utilizes `yolov7`, `yolov7-qat`, `yolov9` `yolov9-qat` models to perform inference on video files or RTSP streams. It then showcases the output on an RTSP URL, providing a straightforward demonstration of end-to-end AI processing.

Follow this steps to Use this Sample App

### 1. Deploy and Start Triton Server

Follow the steps on below link to Start Triton Server<br>
[Triton Server - YOLO.](https://github.com/levipereira/triton-server-yolo/)

 

### 2. Deploy and Start DeepStream 

1. Start Nvidia Container `nvcr.io/nvidia/deepstream:6.4-triton-multiarch` <br>
   Install Deepstream Python Bindings `./user_deepstream_python_apps_install.sh --version 1.1.10`
   

2. Install custom parse lib `NvDsInferYolov9EfficientNMS` for Gst-nvinferserver <br>
   Clone this repository [nvdsinfer_yolo_efficient_nms](https://github.com/levipereira/nvdsinfer_yolo_efficient_nms)   
   The custom library is built and installed using the provided Makefile.


3.   Install Application for DeepStream 6.4 `ds-6.4-ts-yolo-rtsp-out` 
    Follow the steps on below link to Build DeepStream <br>
    [DeepStream - YOLO](https://github.com/levipereira/docker_images/ds-6.4-ts-yolo)


4. Using Sample Application `ds-6.4-ts-yolo-rtsp-out`  

    To use this sample application, follow the steps below from within the container:

    The sample application is installed on `/deepstream_python_apps/apps/ds-6.4-ts-yolo-rtsp-out/`

    This sample application supports input streaming from both `file://` and `rtsp://` sources. It processes the input and streams the output via RTSP at the following URL: `rtsp://localhost:8554/ds-test`

    ```bash
    python3 ds-6.4-ts-yolo-rtsp-out.py -i <input_files> -m <model> -c <codec> -b <bitrate> [--rtsp-ts]

    #example
    python3 ds-6.4-ts-yolo-rtsp-out.py  \
    -i file:///opt/nvidia/deepstream/deepstream/samples/streams/sample_1080p_h264.mp4  \
    -m  yolov9-c \
    -c H264   
    ```
  
    ### Arguments 
    *   `-i`, `--input`: Path to input `file://` or `rtsp://` elementary stream. Multiple input files can be provided.
    *   `-m`, `--model`: Choice  [`'yolov7'`,`'yolov7x'`,`'yolov7-qat'`,`'yolov7x-qat'`,`'yolov9-c'`,`'yolov9-e'`, `'yolov9-c-qat'`,`'yolov9-e-qat'`]. 
    *   `-c`, `--codec`: RTSP Streaming Codec. Choose between `H264` and `H265`. (Default: `H264`)
    *   `-b`, `--bitrate`: Set the encoding bitrate. (Default: `4000000`)
    *   `--rtsp-ts`: Attach NTP timestamp from RTSP source. (Default: `False`)


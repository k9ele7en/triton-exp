# triton-exp
Repo for experimenting NVIDIA Triton Inference server

# Run image
cd triton-exp

sudo docker run --gpus=1 --rm -p8000:8000 -p8001:8001 -p8002:8002 -v ./model_repository:/models nvcr.io/nvidia/tritonserver:21.05-py3 tritonserver --model-repository=/models
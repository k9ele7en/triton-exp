# triton-exp
Repo for experimenting NVIDIA Triton Inference server

# Run image
cd triton-exp

sudo docker run --gpus=1 --rm -p8000:8000 -p8001:8001 -p8002:8002 -v <(full-path-to)/model_repository>:/models nvcr.io/nvidia/tritonserver:21.05-py3 tritonserver --model-repository=/models

## Ex:
Run on vm:
sudo docker run --gpus=1 --rm -p8000:8000 -p8001:8001 -p8002:8002 -v /home/maverick911/repo/server/docs/examples/model_repository:/models nvcr.io/nvidia/tritonserver:21.05-py3 tritonserver --model-repository=/models

Run this ex:
sudo docker run --gpus=1 --rm -p8000:8000 -p8001:8001 -p8002:8002 -v /home/maverick911/repo/triton-exp/model_repository:/models nvcr.io/nvidia/tritonserver:21.05-py3 tritonserver --model-repository=/models

# Note:
Trained model which saved by torch.save (usually .pth) must be convert into torchscript by torch.jit.save (into model.pt as default name of Triton).
Ex: git
    # define model class...
    model = model.to(device)
    # Switch the model to eval model
    model.eval()
    # An example input you would normally provide to your model's forward() method.
    x = torch.randn(1, 3, 768, 768).to(device)
    # Use torch.jit.trace to generate a torch.jit.ScriptModule via tracing.
    traced_script_module = torch.jit.trace(model, x)
    # Save the TorchScript model
    traced_script_module.save('model.pt')

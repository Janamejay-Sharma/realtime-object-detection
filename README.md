# Introduction

Transfer learning is a technique where a pre-trained model, initially trained on a large dataset for a specific task, is fine-tuned for a different but related task.

Instead of starting from scratch, we leverage the pre-trained model and adapt it to our specific problem. This approach can significantly reduce training time and data requirements.

In this project, I performed transfer learning on the `SSD MobileNet V2 FPNLite 320x320` model using Tensorflow's Object Detection API to allow it to detect glasses on a person's face in real-time.

[<img src="workspace\images\demo.gif" width="200"/>]()

# Setup Guide

This guide assumes that you already have Python, CUDA, and CUDNN installed.

## Installing Protocol Buffers (protoc)

Protocol Buffers are a data serialization format used by TensorFlow to define and serialize data structures, especially for exchanging data between different components of a TensorFlow-based system.

1. Go to the Protocol Buffers release page on Github and download the .zip file for your OS: https://github.com/protocolbuffers/protobuf/releases

1. Extract the directory to an installion location of your choice.

1. Add the address of the `bin` subdirectory to the environment variables/path of your system. A restart may be necessary for the changes to apply successfully.

## Installing Tensorflow Object Detection API

1. Clone the Tensorflow Models repository:

```
git clone https://github.com/tensorflow/models.git
```

2. Navigate to the `models` subdirectory:

```
cd models/research
```

3. Run the following command:

```
protoc object_detection/protos/*.proto --python_out=.
```

4. Copy the `.py` setup file to the current directory:

```
cp object_detection/packages/tf2/setup.py .
```

5. Run the setup. I recommend doing this in a new Python virtual environment to avoid conflicts:

```
python -m pip install .
```

6. Verify the install by running the following imports in Python:

```
import tensorflow as tf
from object_detection.utils import config_util
from object_detection.protos import pipeline_pb2
from google.protobuf import text_format
```

## Possible Installation Errors

1. After you run "`python -m pip install .`", you may get the following error:

```
Error:
Collecting PyYAML==5.4.1
  Using cached PyYAML-5.4.1.tar.gz (175 kB)
  Installing build dependencies ... done
  Getting requirements to build wheel ... error
  error: subprocess-exited-with-error

  × Getting requirements to build wheel did not run successfully.
  │ exit code: 1
```

This is caused by the setup not checking if `wheel` is installed and/or an incorrect version of `Cython` being installed. To solve this:

```
pip install wheel
pip install "Cython<3.0" "pyyaml<6" --no-build-isolation
```

2. Importing from `object_detection` may throw a `protobuf` error. This can be solved by installing an older version of `protobuf`:

```
pip install --upgrade protobuf<=3.20
```

3. You may also get a warning message along the lines of `WARNING: Ignoring invalid distribution`. To remove this, navigate to `C:\users\MYNAME\appdata\local\programs\python\python310\lib\site-packages` or your equivalent packages directory and run:

```
 rm ~rotobuf-3.19.6.dist-info
```

## Installing labelImg Python Package

```
pip install labelImg
```

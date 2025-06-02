Details of the Co-Design Process for Hardware-Software on Raspberry Pi with Coral USB Accelerator:
A. Software:

1. Install Raspberry Pi OS (Bullseye, 64-bit) and update packages.
2. Install Python 3.10, pip, TensorFlow Lite Runtime (compatible version with Edge TPU), and PyCoral (library suite for inference on Coral).
3. Copy the .tflite file that has been compiled with “int8” quantization for use with the Edge TPU.
4. Write the inference script (in Python) using the tflite_runtime.interpreter class to load the TFLite model, bind input tensors, and preprocess images in real-time. Also apply pycoral.utils.edgetpu to initialize the interpreter with the Edge TPU delegate.
5. Set batch size = 1 (due to Edge TPU limitations) and resize images to 640×640 before calling interpreter.invoke().
6. Post-process the results (boxes, scores, class_ids): apply a confidence threshold of 0.25, then perform non-maximum suppression (NMS) using the pycoral.adapters.common.non_max_suppression library to output the final bounding boxes.
   B. Hardware:
7. Actual device: Raspberry Pi 4 Model B (4GB RAM) powered at 5V–3A, connected to the Coral USB Accelerator via a USB 3.0 port.
8. Driver configuration:
   o Install libedgetpu1-std and python3-pycoral from the Coral repository.
   o Check Edge TPU status using the lsusb command (should display ID “1a6e:089a Coral USB Accelerator”).
9. Inference latency measurement: use the time.time() library to measure the duration from the moment interpreter.invoke() is called to receiving the output.
10. Auto-start the inference script on device boot (via a systemd service) to handle network disconnections or reboots.

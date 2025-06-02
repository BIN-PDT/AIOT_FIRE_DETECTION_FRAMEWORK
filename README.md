**1. PROJECT**

-   _Train a `YOLO model` using Ultralytics library in Python_.

-   _Build a `Firebase project` to obtain necessary credentials for system and mobile configurations_.

-   _Install `Raspberry Pi OS with desktop and recommended software (64-bit)` using Raspberry Pi Imager_.

**2. CONFIGURATION**

```
sudo apt-get update
```

```
sudo apt-get upgrade
```

-   _Configure for Core System_

    ```
    python -m venv --system-site-packages .venv
    ```

    ```
    source .venv/bin/activate
    ```

    ```
    pip install ultralytics
    ```

    ```
    pip install firebase-admin
    ```

-   _Configure for Coral Accelerator_

    -   _Download suitable `libedgetpu1 package` from https://github.com/feranick/libedgetpu/releases_.

    -   _Install downloaded package using command `sudo dpkg -i path/to/package.deb`_.

    ```
    pip uninstall tensorflow tensorflow-aarch64
    ```

    ```
    pip install -U tflite-runtime
    ```

    ```
    pip install 'numpy<2'
    ```

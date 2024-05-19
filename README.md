# Image Processing API Documentation

This documentation provides details on using the Image Processing API, built using Flask (Python) and TensorFlow. The API accepts an image as input, performs image processing using a pre-trained MobileNetV2 model, and returns the top predicted classes along with their confidence scores.

## Overview

The Image Processing API utilizes Flask, a micro web framework for Python, to handle HTTP requests and responses. It employs a pre-trained MobileNetV2 model, available through TensorFlow's Keras applications, for image processing tasks. The MobileNetV2 model is a convolutional neural network architecture that is optimized for mobile devices while maintaining high accuracy.

## Model Details

- **Model Architecture**: MobileNetV2
- **Pre-trained Weights**: ImageNet
- **Details**: MobileNetV2 is a lightweight deep neural network architecture designed for mobile and embedded vision applications. It consists of depthwise separable convolutions and inverted residual blocks, making it highly efficient in terms of computational resources. The pre-trained weights are obtained by training the model on the ImageNet dataset, which contains millions of labeled images across thousands of classes.

## Requirements

1. **Pre-trained Model**: The API uses a pre-trained MobileNetV2 model for image processing. This model is included in TensorFlow's Keras applications and is trained on the ImageNet dataset.

2. **Flask Application**:
    - The Flask application exposes an API endpoint for image processing.
    - Uploaded images are preprocessed and fed into the MobileNetV2 model for prediction.
    - The top predicted classes along with their confidence scores are returned in JSON format.

## Usage

### Installation

1. Clone the repository:

    ```bash
    git clone https://github.com/Swapnil-DevGeek/flask-api-image-processing
    ```

2. Navigate to the project directory:

    ```bash
    cd  flask-api-image-processing
    ```

3. Install the required dependencies:

    ```bash
    pip install -r requirements.txt
    ```

### Running the API

1. Run the Flask application:

    ```bash
    python app.py
    ```

2. The API will start running on `http://localhost:8000`.

3. You can also upload files via the web interface by visiting `http://localhost:8000` in your browser.

### API Endpoints

- **Upload Image**: 
    - **URL**: `/predict`
    - **Method**: POST
    - **Request Body**: Form-data with key as `file` and value as the image file.
    - **Response**: JSON containing the top predicted classes and their confidence scores.

## Example

### Request

```bash
curl -X POST -F "file=@/path/to/image.jpg" http://localhost:8000/predict
```

### Response

```json
[
    {
        "label": "Labrador_retriever",
        "score": 0.8543121218681335
    },
    {
        "label": "golden_retriever",
        "score": 0.049841642797231674
    },
    {
        "label": "Great_Pyrenees",
        "score": 0.021127985954403877
    }
]
```
## Notes

- **Ensure that the API server is running before making requests.**
- **The API is designed to handle image files in common formats such as JPEG, PNG, etc.**
- **The predictions are based on the ImageNet classes that the MobileNetV2 model was trained on.**
- **The confidence scores represent the probability of each predicted class.**

## Handling Long-Running Tasks with Redis and Asynchronous Approach

### Asynchronous Approach

The asynchronous approach utilizes Celery with Redis as the message broker to handle long-running image processing tasks efficiently. Tasks are queued asynchronously, allowing the API to respond quickly while processing tasks in the background. Clients can poll for task status or receive real-time updates using Redis Pub/Sub.

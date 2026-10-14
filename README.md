# Potato Disease Detection

A full-stack machine learning project for identifying potato leaf diseases from images. The system classifies a uploaded leaf image into one of three classes: Early Blight, Late Blight, or Healthy.

It combines a trained TensorFlow model, a FastAPI backend for inference, and a React frontend for user interaction.

## Project Overview

This project was designed to help users quickly assess the health of potato plants by analyzing leaf images. The workflow is:

1. A user uploads a potato leaf image in the frontend.
2. The frontend sends the image to the API.
3. The FastAPI backend prepares the image tensor and sends it to a TensorFlow model server.
4. The model returns the predicted class and confidence score.
5. The result is displayed in the browser.

## Supported Disease Classes

- Early Blight
- Late Blight
- Healthy

## Repository Structure

```text
.
├── api/                     # FastAPI backend
│   ├── main.py              # Prediction endpoint and image processing logic
│   └── requirements.txt     # Python dependencies
├── frontend/                # React web application
│   ├── public/              # Static frontend assets
│   ├── src/                # React components and styling
│   └── package.json         # Frontend scripts and dependencies
├── saved_models/            # TensorFlow SavedModel files used by serving
├── training/                # Training notebook and plant image data
├── models.config            # TensorFlow Serving model configuration
├── potatoes.h5             # Trained Keras model file (if used in training or experiments)
├── README.md               # Project documentation
└── .gitignore              # Repository ignore rules
```

## Tech Stack

- Python
- FastAPI
- TensorFlow
- TensorFlow Serving
- React
- Docker
- npm

## Prerequisites

Before running the project, make sure you have:

- Python 3.8+ or 3.9+
- Node.js and npm
- Docker
- A terminal with access to the project folder

## Setup Instructions

### 1. Clone the repository

```bash
git clone <repository-url>
cd potato-disease
```

### 2. Set up the backend environment

In a Python environment, install the backend dependencies:

```bash
cd api
pip install -r requirements.txt
```

If you're using Conda, the environment can look like this:

```bash
conda create -n potato-env python=3.9
conda activate potato-env
cd api
pip install -r requirements.txt
```

### 3. Start the TensorFlow model server

This project uses TensorFlow Serving to expose the trained model over HTTP.

From the project root, run:

```bash
sudo docker run -t --rm -p 8502:8502 \
  -v $(pwd):/potato-disease \
  tensorflow/serving \
  --rest_api_port=8502 \
  --model_config_file=/potato-disease/models.config
```

This loads the model configuration and makes the trained model available at:

```text
http://localhost:8502/v1/models/potatoes_model:predict
```

### 4. Start the FastAPI backend

Open a second terminal and start the API:

```bash
cd api
uvicorn main:app --host 0.0.0.0 --port 8000 --reload
```

The API will be available at:

```text
http://localhost:8000
```

Swagger documentation is available at:

```text
http://localhost:8000/docs
```

### 5. Start the frontend

Open a third terminal and install the frontend dependencies:

```bash
cd frontend
npm install
```

Then start the React app:

```bash
REACT_APP_API_URL=http://localhost:8000/predict npm start
```

The frontend should be available at:

```text
http://localhost:3000
```

## How to Use the Application

1. Open the frontend in your browser.
2. Upload an image of a potato leaf.
3. Wait for the model to process the image.
4. View the predicted class and confidence level.

## Model and Training Information

The project includes a training workspace under `training/` and a prepared TensorFlow model under `saved_models/`. The model was trained to detect plant diseases visually from leaf images, with a focus on potato health classification.

The training data is organized by class folders and can be extended with new images for future retraining.

## Notes

- This repository is intended as a reference/demo project for image-based disease recognition.
- For production use, consider adding validation, logging, monitoring, and a more robust deployment setup.
- If the model or dataset changes, update the serving configuration and retrain the model as needed.

## License

This project is provided for educational and research use. Update the license file if you plan to distribute or publish the repository publicly.

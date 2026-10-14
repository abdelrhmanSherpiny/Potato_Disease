# Potato Disease Detection

## Step 1: Start TensorFlow Serving (Terminal 1)

Ensure your external drive is connected so the system mounts the `/run/media/...` directory.

Open a terminal and run the Docker container:

```bash
sudo docker run -t --rm -p 8502:8502 \
  -v /run/media/abdelrhman-sherpiny/Activity/College/Code/potato-disease:/potato-disease \
  tensorflow/serving \
  --rest_api_port=8502 \
  --model_config_file=/potato-disease/models.config
```

## Step 2: Start the FastAPI Server (Terminal 2)

Open a new terminal window, activate the machine learning environment, navigate to the `api` folder, and launch Uvicorn:

```bash
conda activate ml-env
cd /run/media/abdelrhman-sherpiny/Activity/College/Code/potato-disease/api
uvicorn main:app --host localhost --port 8000
```

## Step 3: Access the Application

Once both terminals show that the servers are running, open your web browser and navigate to:

<http://localhost:8000/docs>

Use the Swagger UI to test predictions.

# Majorproject

# Fire Detection System

A complete fire detection system that uses both image analysis and sensor data to detect fire hazards in restaurants and hotel rooms. The system includes a user-friendly web interface for testing and monitoring.

## Features

- Image-based fire detection using CNN model
- Sensor data analysis for fire risk assessment
- Interactive web interface for testing and visualization
- Support for both image uploads and real-time sensor data analysis

## System Requirements

- Python 3.7 or higher
- pip (Python package manager)
- Web browser (Chrome, Firefox, Safari, or Edge)
- At least 4GB of RAM
- GPU (optional but recommended for faster image processing)

## Project Structure

```
fire-detection-system/
├── static/
│   ├── css/
│   │   └── styles.css
│   ├── js/
│   │   └── script.js
│   └── uploads/          # Folder for uploaded images and CSV files
├── templates/
│   └── index.html
├── app.py                # Main Flask application
├── fire_detection_model.py # CNN model for fire detection
├── sensor_data_processor.py # Sensor data processing utilities
├── requirements.txt      # Python dependencies
└── README.md            # This file
```

## Installation

Follow these steps to set up the fire detection system:

1. Clone or download this repository to your local machine.

2. Create and activate a virtual environment (recommended):

```bash
# Create virtual environment
python -m venv venv

# Activate on Windows
venv\Scripts\activate

# Activate on macOS/Linux
source venv/bin/activate
```

3. Install the required dependencies:

```bash
pip install -r requirements.txt
```

## Data Preparation

### Image Dataset

The system expects a dataset with the following structure:

```
fire_dataset/
├── 0/            # Images with no fire
│   ├── img1.jpg
│   ├── img2.jpg
│   └── ...
└── 1/            # Images with fire
    ├── img1.jpg
    ├── img2.jpg
    └── ...
```

Place your fire dataset in the project directory or update the `DATASET_PATH` variable in `fire_detection_model.py` to point to your dataset location.

### Sensor Data

The system accepts CSV files containing sensor data. The CSV should contain relevant sensor readings such as temperature, smoke levels, humidity, etc. If your CSV has a column indicating fire/no fire status, the system will use that for training; otherwise, it will make assumptions based on the data patterns.

## Training the Models

### Image Model

To train the fire detection image model:

```bash
python fire_detection_model.py
```

This will train a CNN model using the provided dataset and save it as `fire_detection_model.h5`.

### Sensor Model

The sensor model can be trained through the web interface by uploading a CSV file, or programmatically:

```bash
python -c "from sensor_data_processor import SensorDataProcessor; SensorDataProcessor('your_sensor_data.csv').train_model()"
```

## Running the Application

Start the web application with:

```bash
python app.py
```

Then open your web browser and navigate to [http://localhost:5000](http://localhost:5000) to access the fire detection system interface.

## Using the System

### Image-based Fire Detection

1. Navigate to the "Image-based Fire Detection" section.
2. Click "Choose File" and select an image to analyze.
3. Click "Detect Fire" to process the image.
4. View the results, including fire detection status and probability.

### Sensor Data Analysis

1. First, upload your sensor data CSV file in the "Sensor Data Analysis" section.
2. Once the model is trained, you can input individual sensor values for real-time testing.
3. Click "Analyze Sensors" to get the fire risk assessment based on the entered values.

## Deployment

For production deployment:

1. Set up a proper web server like Nginx or Apache.
2. Configure a WSGI server (e.g., Gunicorn) to run the Flask application.
3. Consider security measures like input validation and access control.
4. Use environment variables for sensitive configurations.

Example deployment with Gunicorn:

```bash
pip install gunicorn
gunicorn -w 4 -b 0.0.0.0:8000 app:app
```

Then configure Nginx to proxy requests to Gunicorn.

## Extending the System

### Adding More Sensor Types

Modify the `index.html` and `sensor_data_processor.py` files to include additional sensor types relevant to your fire detection needs.

### Improving the Image Model

To enhance the image-based detection:
- Add more training data
- Try transfer learning with pre-trained models like ResNet or MobileNet
- Implement real-time video analysis

### Path Finding Implementation

For the shortest path feature mentioned in the requirements:
- Implement a graph-based representation of the building layout
- Use algorithms like Dijkstra's or A* for path finding
- Integrate with the fire detection system to avoid fire-affected areas

## Troubleshooting

- If the model training fails, ensure you have enough memory and check dataset paths.
- If the web interface doesn't load, check Flask server logs for errors.
- For prediction issues, verify that model files (.h5 and .joblib) exist in the project directory.
- If sensor data processing fails, check that the CSV format matches the expected structure.

## License

This project is provided for educational and development purposes.

## Contact

For support or questions, please [create an issue](https://github.com/yourusername/fire-detection-system/issues) on the GitHub repository.

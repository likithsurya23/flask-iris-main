MACHINE LEARNING MODEL FOR IRIS DATASET (https://www.kaggle.com/code/sxsntd/iris-dataset)
Here's an `README.md` for your Iris dataset prediction project:
# Iris Flower Prediction System

## Overview

This project is a web-based application that predicts the species of an Iris flower based on user input. It uses a pre-trained model to make predictions. The application is built using Flask, a lightweight web framework for Python.

### Supervised by
Prof. Agughasi Victor Ikechukwu,  
(Assistant Professor)  
Department of CSE, MIT Mysore

## Project Structure

```
Iris_Flower_Prediction/
│
├── models/
│   └── iris_model.pkl
│
├── static/
│   ├── css/
│   │   └── styles.css
│   ├── js/
│   │   └── scripts.js
│   └── images/
│       └── logo.png
│
├── templates/
│   ├── home.html
│   └── after.html
│
├── app.py
└── README.md
```

## Files Description

- **models/iris_model.pkl**: The pre-trained model saved in pickle format.
- **static/**: Directory for static files like CSS, JavaScript, and images.
  - **css/styles.css**: The main stylesheet.
  - **js/scripts.js**: The main JavaScript file.
  - **images/logo.png**: An example image file.
- **templates/home.html**: The HTML template for the input form.
- **templates/after.html**: The HTML template for displaying the prediction result.
- **app.py**: The main Flask application file.
- **README.md**: Project documentation file.

## Setup Instructions

### Prerequisites

- Python 3.12
- Flask
- scikit-learn
- numpy
- pandas

### Installation

1. **Clone the repository**:
    ```bash
    git clone https://github.com/yourusername/Iris_Flower_Prediction
    cd Iris_Flower_Prediction
    ```

2. **Create a virtual environment**:
    ```bash
    # On Windows use
    python -m venv venv
    venv\Scripts\activate
    ```

3. **Install the required packages**:
    ```bash
    pip install flask scikit-learn numpy pandas
    ```

4. **Ensure the model file exists**:
    Make sure `iris_model.pkl` is present in the `models` directory.

## Usage

1. **Run the Flask application**:
    ```bash
    python app.py
    ```

2. **Access the application**:
    Open your web browser and go to `http://127.0.0.1:5000/`.

3. **Enter the required details**:
    Fill in the form with the necessary details and click on the "Predict" button to get the prediction.

## Code Explanation

### `app.py`

This is the main Flask application file.

```python
from flask import Flask, render_template, request
import pickle
import numpy as np

# Load the model
model = pickle.load(open('models/iris_model.pkl', 'rb'))

app = Flask(__name__)

@app.route('/')
def main():
    return render_template('home.html')

@app.route('/predict', methods=['POST'])
def predict():
    data1 = request.form['a']
    data2 = request.form['b']
    data3 = request.form['c']
    data4 = request.form['d']
    arr = np.array([[data1, data2, data3, data4]])
    pred = model.predict(arr)
    return render_template('after.html', data=pred)

if __name__ == "__main__":
    app.run(debug=True)
```

### `templates/home.html`

This is the HTML template for the home page.

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Iris Flower Prediction</title>
    <link rel="stylesheet" href="{{ url_for('static', filename='css/styles.css') }}">
</head>
<body>
    <h1>Enter Data for Prediction</h1>
    <form action="{{ url_for('predict') }}" method="POST">
        <input type="text" name="a" placeholder="Enter sepal length">
        <input type="text" name="b" placeholder="Enter sepal width">
        <input type="text" name="c" placeholder="Enter petal length">
        <input type="text" name="d" placeholder="Enter petal width">
        <button type="submit">Predict</button>
    </form>
</body>
</html>
```

### `templates/after.html`

This is the HTML template for displaying the prediction result.

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Prediction Result</title>
    <link rel="stylesheet" href="{{ url_for('static', filename='css/styles.css') }}">
</head>
<body>
    <h1>Prediction Result</h1>
    <p>The predicted Iris species is: {{ data }}</p>
    <a href="{{ url_for('main') }}">Predict Again</a>
</body>
</html>
```

## Screenshots

![image](https://github.com/yourusername/Iris_Flower_Prediction/assets/sample_image.png)

## Conclusion

This documentation provides a comprehensive guide to setting up and running the Iris Flower Prediction System. By following the steps outlined, you should be able to deploy the application and make predictions based on user input. If you encounter any issues, ensure that all dependencies are installed and that the model file is correctly placed in the `models` directory.
```
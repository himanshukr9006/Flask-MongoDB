Google Docx - [https://docs.google.com/document/d/10Af1tHBE94kK_axCEQES8kw0RYknvw7psqOMFbY5qjE/edit?usp=sharing]

# Project-Flask
1. Create a Flask application with an /api route. When this route is accessed, it should return a JSON list. The data should be stored in a backend file, read from it, and sent as a response.

app.py
from flask import Flask, jsonify

app = Flask(__name__)

@app.route('/api')
def api():
    
    data = ["Apple", "Banana", "Mango"]

    return jsonify(data)


if __name__ == '__main__':
    app.run(debug=True)

data.txt
from flask import Flask, jsonify

app = Flask(__name__)

@app.route('/api')
def api():
    
    data = ["Apple", "Banana", "Mango"]

    return jsonify(data)


if __name__ == '__main__':
    app.run(debug=True)


# Flask-MongoDB
2. Create a form on the frontend that, when submitted, inserts data into MongoDB Atlas. Upon successful submission, the user should be redirected to another page displaying the message "Data submitted successfully". If there's an error during submission, display the error on the same page without redirection.

Flask-MongoDB
|
|>templates
  index.html
  success.html
|app.py

app.py
from flask import Flask, render_template, request
import pymongo

app = Flask(__name__)

# MongoDB Connection
client = pymongo.MongoClient("mongodb+srv://studyhimanshu9006_db_user:xsOgmvKOPphJl91p@cluster0.q1aokau.mongodb.net/?appName=Cluster0")

db = client["testdb"]

collection = db["users"]

# Home Page
@app.route('/')
def home():

    return render_template('index.html')

# Form Submit
@app.route('/submit', methods=['POST'])
def submit():

    # Get form data
    name = request.form.get('name')

    # Insert into MongoDB
    collection.insert_one({
        "name": name
    })

    # Success page
    return render_template('success.html')

# Run Server
if __name__ == '__main__':
    app.run(debug=True)

index.html
<!DOCTYPE html>
<html>
<head>
    <title>Form</title>
</head>
<body>

    <h1>Enter Your Name</h1>

    <form action="/submit" method="POST">

        <input type="text" name="name">

        <button type="submit">Submit</button>

    </form>

</body>
</html>

success.html
<!DOCTYPE html>
<html>
<head>
    <title>Success</title>
</head>

    
<body>

    <h1>Data submitted successfully</h1>

</body>
</html>

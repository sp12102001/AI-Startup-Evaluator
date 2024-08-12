# VentureCommunist - AI Venture Scout Assistant

Welcome to **VentureCommunist**, your ultimate AI assistant designed to guide AI venture scouts through the complex world of AI startups. This repository contains everything you need to set up and run the VentureCommunist web application, including configuration files, styling, and instructions for creating custom webhooks.

## Table of Contents

- [Introduction](#introduction)
- [Project Structure](#project-structure)
- [Installation](#installation)
- [Usage](#usage)
- [Configuring the JSON File](#configuring-the-json-file)
- [Creating Your Own Webhooks](#creating-your-own-webhooks)
  - [Using Node.js](#using-nodejs)
  - [Using Python (Flask)](#using-python-flask)
- [Contributing](#contributing)
- [License](#license)

## Introduction

VentureCommunist is an AI-powered web application that helps venture scouts navigate the AI startup ecosystem. It’s built with a lighthearted, humorous tone, making your venture scouting experience both fun and effective.

## Project Structure

Here's a breakdown of the files included in this repository:

- **`.github/workflows/jekyll-gh-pages.yml`**: Automates deployment of the site using Jekyll and GitHub Pages, ensuring continuous deployment whenever changes are pushed to the main branch.
  
- **`api/VentureCommunist.json`**: This JSON file contains data related to AI recommendations and configurations used by the application. It's the backend data source for the venture scouting process.

- **`index.html`**: The main HTML file for the application. This file defines the structure of the web page and links to styles and scripts that power the UI and interactions.

- **`styles.css`**: The CSS file that styles the web application, ensuring it looks modern and is responsive across devices.

## Installation

To set up the project locally, follow these steps:

1. **Clone the repository**:
    ```bash
    git clone https://github.com/yourusername/venturecommunist.git
    ```
2. **Navigate to the project directory**:
    ```bash
    cd venturecommunist
    ```

No additional installation steps are required—just open the `index.html` file in your browser and you're ready to go!

## Usage

1. **Open the application**: After cloning the repository, open `index.html` in your browser.
2. **Interact with the UI**: Enter your startup's URL and name, and submit the form. The application will use the JSON data and webhooks to provide feedback and recommendations.

## Configuring the JSON File

The `VentureCommunist.json` file in the `api/` directory is a key part of how the application functions. Here’s how you can configure and use it:

### Structure of `VentureCommunist.json`

The JSON file contains data that the application uses to generate recommendations or perform actions based on user input. The structure typically includes arrays or objects that store information like:

- **Startup Data**: Information about various startups.
- **Recommendations**: Custom messages or advice based on user inputs.
- **Webhook URLs**: Endpoints where data should be sent after form submission.

### Example Structure:

```
{
  "startups": [
    {
      "name": "Example Startup",
      "url": "https://www.examplestartup.com",
      "category": "AI",
      "recommendation": "Invest heavily in AI research."
    }
  ],
  "webhooks": {
    "default": "https://yourwebhookurl.com",
    "alternative": "https://anotherwebhookurl.com"
  }
}
```
### How to Modify:
```
{
  "startups": [
    {
      "name": "Example Startup",
      "url": "https://www.examplestartup.com",
      "category": "AI",
      "recommendation": "Invest heavily in AI research."
    }
  ],
  "webhooks": {
    "default": "https://yourwebhookurl.com",
    "alternative": "https://anotherwebhookurl.com"
  }
}
```
1. **Add Startups**: You can add new startup entries with different names, URLs, and recommendations.
2. **Update Webhook URLs**: Modify the `webhooks` section to point to your own webhook endpoints.

## Creating Your Own Webhooks

To fully utilize the VentureCommunist application, you can create your own webhooks to handle the data submitted by users. Below are instructions for creating webhooks using Node.js and Python (Flask).

### Using Node.js

#### Step 1: Set Up Your Node.js Environment

1. **Initialize a new Node.js project**:
   ```
    mkdir venturecommunist-webhook
    cd venturecommunist-webhook
    npm init -y
``
3. **Install the necessary packages**:
```
    npm install express body-parser
```
#### Step 2: Create the Webhook Server

1. **Create a file named `server.js`**:
   ```
    const express = require('express');
    const bodyParser = require('body-parser');
   
    const app = express();
    const PORT = process.env.PORT || 3000;

    app.use(bodyParser.urlencoded({ extended: true }));

    app.post('/webhook', (req, res) => {
        const { url, name } = req.body;
        console.log(`Received URL: ${url}`);
        console.log(`Received Name: ${name}`);
        
        // Perform your custom logic here

        res.send(`Data received! Hello ${name}, your startup URL is ${url}.`);
    });

    app.listen(PORT, () => {
        console.log(`Server is running on port ${PORT}`);
    });

   ```
3. **Run the server**:
```
    node server.js
    
```
4. **Test the webhook**:
    - The server will listen on `http://localhost:3000/webhook`.
    - You can use tools like Postman or submit the form in your `index.html` to send POST requests to this endpoint.

#### Step 3: Update `VentureCommunist.json`

Update the webhook URL in `VentureCommunist.json` to point to your local or deployed server:

```
{
  "webhooks": {
    "default": "http://localhost:3000/webhook"
  }
}
```

### Using Python (Flask)

#### Step 1: Set Up Your Python Environment

1. **Create a new directory for your project**:
    \```bash
    mkdir venturecommunist-flask
    cd venturecommunist-flask
    \```

2. **Set up a virtual environment**:
    \```bash
    python3 -m venv venv
    source venv/bin/activate
    \```

3. **Install Flask**:
    \```bash
    pip install Flask
    \```

#### Step 2: Create the Webhook Server

1. **Create a file named `app.py`**:
    \```python
    from flask import Flask, request, jsonify

    app = Flask(__name__)

    @app.route('/webhook', methods=['POST'])
    def webhook():
        data = request.form
        url = data.get('url')
        name = data.get('name')
        
        print(f"Received URL: {url}")
        print(f"Received Name: {name}")

        # Perform your custom logic here

        return jsonify(message=f"Data received! Hello {name}, your startup URL is {url}.")

    if __name__ == '__main__':
        app.run(port=5000)
    \```

2. **Run the server**:
    \```bash
    python app.py
    \```

3. **Test the webhook**:
    - The server will listen on `http://localhost:5000/webhook`. You can use tools like Postman or submit the form in your `index.html` to send POST requests to this endpoint.

#### Step 3: Update `VentureCommunist.json`

Update the webhook URL in `VentureCommunist.json` to point to your local or deployed Flask server:

```
{
  "webhooks": {
    "default": "http://localhost:5000/webhook"
  }
}
```

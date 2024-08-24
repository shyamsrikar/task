# Dashboard Widget Application

This project is a frontend assignment for trainees that involves creating a dynamic dashboard page. The dashboard allows users to add, remove, and search through widgets under various categories.

## Table of Contents

- [Features](#features)
- [Project Structure](#project-structure)
- [Installation](#installation)
- [Usage](#usage)
- [Deployment](#deployment)
- [Documentation](#documentation)
- [Contributing](#contributing)
- [License](#license)

## Features

- **Dynamic Dashboard**: Users can add and remove widgets under different categories.
- **JSON Data Structure**: Categories and widgets are defined in a JSON file.
- **State Management**: Utilizes Redux for managing the application's state.
- **Search Functionality**: Users can search through the list of widgets.

## Project Structure

- **`dashboardData.json`**: Defines the categories and widgets in the dashboard.
- **`widgetSlice.js`**: Manages the widgets' state using Redux.
- **`Dashboard.js`**: Renders the dashboard and handles widget addition and removal.
- **`App.js`**: The main component that integrates the dashboard with Redux.

## Installation

1. Clone the repository or download the project files.

    ```bash
    git clone https://github.com/yourusername/dashboard-app.git
    cd dashboard-app
    ```

2. Install the necessary dependencies.

    ```bash
    npm install
    ```

## Usage

1. Start the development server.

    ```bash
    npm start
    ```

2. Open your browser and navigate to `http://localhost:3000` to view the dashboard.

## Deployment

To deploy the application:

1. Zip the project files or push them to a repository on GitHub or another platform.

2. Share the link with others or deploy it to a web hosting service.

## Documentation

### JSON Structure

The `dashboardData.json` file defines the structure of the categories and widgets:

```json
{
  "categories": [
    {
      "id": 1,
      "name": "CSPM Executive Dashboard",
      "widgets": [
        {
          "id": 1,
          "name": "Widget 1",
          "text": "Random text for widget 1"
        },
        {
          "id": 2,
          "name": "Widget 2",
          "text": "Random text for widget 2"
        }
      ]
    }
  ]
}


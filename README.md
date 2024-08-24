
Requirements:
Dashboard Structure: Create a JSON file to define the categories and widgets.
Dynamic Widgets: Users should be able to add and remove widgets dynamically.
Widget Details: Each widget will have a name and some random text.
Add Widget Feature: Include a form to add new widgets to categories.
Remove Widget Feature: Provide a way to remove widgets from categories.
Search Functionality: Users should be able to search through the list of widgets.
Development: Use React or Angular, and a state management tool to handle the widgets.
Sample Code in React (with Redux for state management)
Step 1: Set Up the JSON Structure
Create a JSON file that defines categories and widgets:

json
Copy code
// dashboardData.json
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
Step 2: Initialize the React Project
bash
Copy code
npx create-react-app dashboard-app
cd dashboard-app
npm install redux react-redux
Step 3: Set Up Redux for State Management
Create a slice for managing widgets:

javascript
Copy code
// src/store/widgetSlice.js
import { createSlice } from '@reduxjs/toolkit';

const widgetSlice = createSlice({
  name: 'widgets',
  initialState: [],
  reducers: {
    setWidgets: (state, action) => {
      return action.payload;
    },
    addWidget: (state, action) => {
      const { categoryId, widget } = action.payload;
      const category = state.find(c => c.id === categoryId);
      if (category) {
        category.widgets.push(widget);
      }
    },
    removeWidget: (state, action) => {
      const { categoryId, widgetId } = action.payload;
      const category = state.find(c => c.id === categoryId);
      if (category) {
        category.widgets = category.widgets.filter(w => w.id !== widgetId);
      }
    }
  }
});

export const { setWidgets, addWidget, removeWidget } = widgetSlice.actions;
export default widgetSlice.reducer;
Step 4: Load the JSON Data
javascript
Copy code
// src/store/index.js
import { configureStore } from '@reduxjs/toolkit';
import widgetReducer, { setWidgets } from './widgetSlice';
import dashboardData from './dashboardData.json';

const store = configureStore({
  reducer: {
    widgets: widgetReducer
  }
});

store.dispatch(setWidgets(dashboardData.categories));

export default store;
Step 5: Create the Dashboard Component
javascript
Copy code
// src/components/Dashboard.js
import React from 'react';
import { useSelector, useDispatch } from 'react-redux';
import { addWidget, removeWidget } from '../store/widgetSlice';

const Dashboard = () => {
  const categories = useSelector(state => state.widgets);
  const dispatch = useDispatch();

  const handleAddWidget = (categoryId) => {
    const widgetName = prompt("Enter Widget Name:");
    const widgetText = prompt("Enter Widget Text:");
    const newWidget = { id: Date.now(), name: widgetName, text: widgetText };
    dispatch(addWidget({ categoryId, widget: newWidget }));
  };

  const handleRemoveWidget = (categoryId, widgetId) => {
    dispatch(removeWidget({ categoryId, widgetId }));
  };

  return (
    <div>
      {categories.map(category => (
        <div key={category.id}>
          <h2>{category.name}</h2>
          <button onClick={() => handleAddWidget(category.id)}>+ Add Widget</button>
          {category.widgets.map(widget => (
            <div key={widget.id}>
              <h3>{widget.name}</h3>
              <p>{widget.text}</p>
              <button onClick={() => handleRemoveWidget(category.id, widget.id)}>Remove</button>
            </div>
          ))}
        </div>
      ))}
    </div>
  );
};

export default Dashboard;
Step 6: Integrate the Dashboard in the App
javascript
Copy code
// src/App.js
import React from 'react';
import { Provider } from 'react-redux';
import store from './store';
import Dashboard from './components/Dashboard';

function App() {
  return (
    <Provider store={store}>
      <div className="App">
        <Dashboard />
      </div>
    </Provider>
  );
}

export default App;
Step 7: Run the Application
bash
Copy code
npm start
Final Steps:
Deploy: Zip the project and share it via GitHub or another method.
Documentation: Provide instructions on how to run the application locally.
Instructions for Running the Application Locally:
Clone the repository or unzip the project folder.
Run npm install to install dependencies.
Run npm start to start the development server.
Open http://localhost:3000 in your browser to view the dashboard.
This setup provides a basic structure to meet the requirements outlined in the assignment. You can customize and enhance the dashboard further according to the needs.

# Veriviz Structure

Below is a high-level breakdown of the Veriviz repository:

## Directory Layout

### **`frontend/`** 
  - A React-based interface. Sends requests to the backend to retrieve analysis 
    results from SEIF and Sylvia.
  - Pages like `Home.jsx`, `Upload.jsx`, `Visualizer.jsx` are typical.
  - Utlizes ReactJS and React Router, to learn more about ReactJS - [Click Here](https://react.dev/reference/react) and  to learn more about React Router, [Click Here](https://reactrouter.com/home) 

### **`backend/`** 
  - `server.js` is the main entrypoint of the backend and is run when the pod is deployed.
  - `backend/uploads` is where the uploaded files from the frontend will be ultimitly stored before being sent to the SEIF or Sylvia APIs 
  - Talks to **SEIF** and **Sylvia** depeding on the users choice.
  - Exposes endpoints that are designed for the frontend to send and recieve information.
  - Utlizes ExpressJS for RestFUL API endpoints to delegate tasks to SEIF and Sylvia APIs respectfully.

### **`.github/workflows/`** 
  - Houses CI/CD config (like `cicd.yml`) for automatic deployment to OKD. See [All About Deployment](Deployment/deployment_intro.md) for more information.


### How It Works

1. **`Frontend`** → user triggers “Analyze hardware design.”
2. **`Backend`** → receives request, calls SEIF or calls Sylvia.
3. **`SEIF`** or **`Sylvia`** APIs → recieve request from the **`backend`** and process the files → then return JSON to later be displayed.
4. **`Backend`** → recieves the JSON and sends it back to **`frontend`**.
5. **`Frontend`** → recieves the JSON results and displays them,



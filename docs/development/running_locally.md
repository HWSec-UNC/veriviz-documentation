# Running on your local machine

## Running Veriviz

1. After opening the devcontainer, open a new terminal and run `cd frontend`
2. Run `npm install` to verify everything is installed
3. Run `npm run dev`. Now the frontend is up and running on `http://localhost:5173/`.
!!! note "If step 3 is not working"
    If it is not running on localhost:5173 check your CLI for the correct port. Then navigate to `.devcontainer/devcontainer.json` and change this line ` "forwardPorts": [5173, 8000]` to  `"forwardPorts": [VITE_PORT_HERE, 8000]` where the `VITE_PORT_HERE` is the port where the app tried to run. Then navigate to `/frontend/vite.config.js` and change the line `port: 5173` to again, `port: VITE_PORT_HERE`. Rebuild the container through `ctrl + shft + p`(`cmnd + shft + p`for mac), and then typing Rebuild in container` and selecting that. **Do NOT commit these changes to the remote repository** but these changes sould fix your project locally.
4. Now we want to run the backend. Open a new terminal(diffrent than the one you used for the previous steps) `cd ../backend` in your terminal
5. Run `npm install` to verify everything is installed
6. Run `node server.js`. Now the backend is up and running on `https://localhost:8000/`. Note there is no display page for the root so visiting this on your browser, check the console for verification.
!!! note "If step 6 is not working"
    If it is not running on localhost:8000 check your CLI for the correct port. Then navigate to `.devcontainer/devcontainer.json` and change this line ` "forwardPorts": [5173, 8000]` to  `"forwardPorts": [5173E, NODE_PORT_HERE]` where the `NODE_PORT_HERE` is the port where the app tried to run. Rebuild the container through `ctrl + shft + p`(`cmnd + shft + p`for mac), and then typing Rebuild in container` and selecting that. **Do NOT commit these changes to the remote repository** but these changes sould fix your project locally.

!!! note "Security Vulenerabilities"
    When running `npm install`, if you see any messages in the CLI stating security vulnerabilities,
    run `npm audit fix`.

# Running Sylvia

1. Clone or Fork the Sylvia repository and open the dev container
2. 
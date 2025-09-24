**Global AI MIT Hackathon Project: Optimal Freight Route Planner**  
*Hackathon entry for the [Global AI MIT JHackathon](https://www.globalaihackathon.com/)*

**Team Members (École Polytechnique)**

- Mohamed Aloulou <mohamed.aloulou@polytechnique.edu>  
- Hippolyte Wallaert <hippolyte.wallaert@polytechnique.edu>  
- Antoine Maecheler <antoine.maecheler@polytechnique.edu>  
- Édouard Rabasse <edouard.rabasse@polytechnique.edu>  
---

## Project Overview

We have built an interactive application that computes the optimal freight transport route between two cities based on user-definable priorities: speed, cost, and environmental impact (CO₂ emissions).

- **Origins & Destinations:** Users select any two cities.  
- **Preferences:** Adjust sliders for time, price, and sustainability importance.  
- **Multi-Modal Network:** Supports road, air, and sea segments.  
- **Real-World Data:** Leverages geographical coordinates, transportation timetables, CO₂ emission estimates, and price data.  
- **Dynamic Updates:** Incorporates live traffic, weather, or other user-provided conditions to recalculate the best route in real time.

---

## Run the interface

### Getting started
Clone the repository and install dependencies:

1. Navigate to the project directory:
    ```bash
    cd <repo_name>
    ```

2.  This project depends on the `uv` CLI. Please ensure it’s installed—if not, install it as follows : 
- MacOS (Homebrew):
```bash
brew install uv
```

- Debian/Ubuntu:
```bash
# For Debian/Ubuntu-based systems
sudo apt update && sudo apt install uv


```
- Windows (Chocolatey):
```bash
choco install uv
```

3. Create & Sync Virtual Environment
    ```bash
    uv sync
    ```

### Running the interface


Run the backend server
```bash
   uv run uvicorn main:app --reload
```
Then in a new terminal, run the frontend:
```bash
    npm start
```
Note : Ensure Node.js and npm are installed. Download them from [Node.js official website](https://nodejs.org/).

## Use Claude via our custom MCP server
We added Claude for real-time change detection and to provide the user with the best route at any time. The user can input traffic information, weather conditions, and other factors that may affect the route. 

This functionality currently only works on macOS. Please make sure you’ve downloaded the Claude Desktop app (https://claude.ai/) and have an active subscription. Then install and run the MCP server via:

```bash
uv run mcp install csv_editor.py --name "Shipping MCP" --with-editable .
```

## Project Structure
### Backend
The first part of the project was gathering data and creating a database of cities and routes.
Initially, we picked 30 US cities and used open source APIs to gather data on their geographical coordinates, airports, and ports. We then generated a list of all possible routes between these cities, including road, air, and ship routes. The data was enriched with estimated travel times, distances, CO2 emissions, and prices.
This grid allows us to cover the US territory but should the user input a city that is not in the list, the program will add it to the database and generate the routes for it.


### Solver
The second part was translating the problem into a linear programming problem. We used gurobipy to create a model that minimizes the cost of transportation while respecting the constraints of time and CO2 emissions. The model takes into account the user's preferences for speed, price, and sustainability.
The solver uses the data from the database to find the optimal route between the two selected cities.

Then we compute the best alternative routes using the same model. The user can select the best route based on their preferences, and the program will provide the best alternative routes as well.

### Frontend
Then we developped a tool to visualize the results. The user can select the origin and destination cities, adjust the importance of time, cost, and CO2 emissions, and see the best route on a map. 

### Final Demo

The one-minute video for our final demo is available at https://www.youtube.com/watch?v=98FYwTaLDQA



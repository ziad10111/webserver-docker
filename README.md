# Dockerized NGINX Server Hosting a JavaScript Game

## Overview
This project demonstrates how to host a simple game built with HTML, CSS, and JavaScript on an NGINX server inside a Docker container. The game is called **Pig Game** and features an interactive dice-rolling experience for two players.

## Project Structure
The project consists of the following files:

- **Dockerfile**: Used to build the Docker image.
- **myapp/**: Contains the game files (HTML, JavaScript, CSS, and images).
  - `index.html`: Main HTML file.
  - `style.css`: Stylesheet for the game.
  - `script.js`: JavaScript logic for the game.
  - Dice images (e.g., `dice-1.png`, `dice-2.png`, etc.).

## Dockerfile
The `Dockerfile` is used to create a lightweight Docker image to host the game:

```dockerfile
FROM ubuntu:latest 
RUN apt-get update && apt-get upgrade -y
RUN apt-get install -y nginx

COPY myapp /var/www/html

EXPOSE 8080
CMD [ "nginx", "-g", "daemon off;" ]
```

### Explanation:
1. **Base Image**: Uses the latest Ubuntu image as the base.
2. **Install NGINX**: Updates the package lists, upgrades existing packages, and installs NGINX.
3. **Copy Files**: Copies the game files from the local `myapp` directory to NGINX's default document root (`/var/www/html`).
4. **Expose Port**: Exposes port `8080` to allow access to the game.
5. **Start NGINX**: Starts the NGINX server in the foreground.

## Setting Up and Running the Project

### Prerequisites
- Docker installed on your system.

### Steps
1. **Clone the Repository**:
   ```bash
   git clone https://github.com/<your-username>/<your-repo>.git
   cd <your-repo>
   ```

2. **Build the Docker Image**:
   ```bash
   docker build -t pig-game .
   ```

3. **Run the Container**:
   ```bash
   docker run -p 8080:8080 pig-game
   ```

4. **Access the Game**:
   Open a web browser and navigate to `http://localhost:8080` to play the game.

## Game Instructions
1. **Objective**: The first player to reach 100 points wins.
2. **Rules**:
   - Players take turns rolling a dice.
   - If a player rolls a 1, their current score resets to 0, and it's the next player's turn.
   - Players can "hold" to add their current score to their total score and pass the turn.
3. **Controls**:
   - **New Game**: Resets the game.
   - **Roll Dice**: Rolls the dice.
   - **Hold**: Saves the current score to the total.

## File Breakdown

### `index.html`
The main HTML file defines the game's structure and includes references to the stylesheet and JavaScript files.

### `script.js`
Contains the game's logic, including:
- Initializing game states.
- Handling dice rolls and turns.
- Switching players.
- Checking for a winner.

### `style.css`
Defines the visual appearance of the game, including layout, colors, and animations.

### Dice Images
PNG images representing dice faces from 1 to 6 are used to display the result of each roll.

## Customization
- To modify the game rules, edit the logic in `script.js`.
- To change the design, update `style.css`.

## Troubleshooting
- **Port Conflict**: If port `8080` is already in use, map the container to a different port using `-p`:
  ```bash
  docker run -p 9090:8080 pig-game
  ```
  Then access the game at `http://localhost:9090`.
- **Permission Issues**: Ensure the `myapp` folder and its contents are accessible to Docker.

## License
This project is licensed under the MIT License.

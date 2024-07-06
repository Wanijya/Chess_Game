# Custom Chess Game

This project is a real-time multiplayer chess game built using Express, Socket.io, and chess.js on the backend, and vanilla JavaScript with drag-and-drop functionality on the frontend.

## Features

- Real-time multiplayer gameplay
- Drag-and-drop interface for moving pieces
- Automatic role assignment (White, Black, Spectator)
- Game state synchronization across all connected clients
- Unicode representation of chess pieces

## Backend

The backend is responsible for managing the game state, handling player connections, and broadcasting moves to all connected clients.

### Dependencies

- `express`
- `http`
- `socket.io`
- `chess.js`

### Server Code Overview

1. **Import Dependencies**: Import `express`, `http`, `socket.io`, and `chess.js`.
2. **Initialize Server**:
    - Create an Express app instance.
    - Initialize an HTTP server with Express.
    - Instantiate Socket.io on the HTTP server.
3. **Game State Management**:
    - Create a `Chess` object instance using `chess.js`.
    - Initialize a `players` object to track socket IDs and roles (white/black).
    - Track the current player's turn.
4. **Express Configuration**:
    - Use the EJS templating engine.
    - Serve static files from the `public` directory.
5. **Routes**:
    - Define a route for the root URL and render the `index` template with the title "Custom Chess Game".
6. **Socket.io Events**:
    - Handle client connections and assign roles based on availability (white, black, spectator).
    - Send the initial board state using FEN notation.
    - Handle client disconnections and update the players' object.
    - Listen for "move" events, validate moves, update the game state, and broadcast moves and updated board states.

## Frontend

The frontend is responsible for rendering the chessboard, handling user interactions, and communicating with the backend using Socket.io.

### Dependencies

- `socket.io-client`
- `chess.js`

### Frontend Code Overview

1. **Socket.io Initialization**:
    - Establish a WebSocket connection to the server using Socket.io.
2. **Chess Game Initialization**:
    - Create an instance of the Chess class from `chess.js` to manage the game logic.
3. **DOM Elements**:
    - Select the HTML element with the ID "chessboard" to render the chessboard.
4. **Drag and Drop**:
    - Implement drag-and-drop functionality for moving chess pieces.
    - Pieces are draggable only if it's the player's turn.
    - Attach event listeners for drag start, drag end, drag over, and drop events.
5. **Rendering the Board**:
    - Generate the HTML representation of the chessboard based on the current game state.
    - Iterate over the board array and create square elements for each cell.
    - Create piece elements for occupied squares and append them to square elements.
    - Flip the board for the black player's view.
6. **Handling Moves**:
    - Handle player moves when dragging and dropping pieces.
    - Construct a move object containing the source and target squares in algebraic notation.
    - Emit a "move" event to the server via Socket.io.
7. **Unicode Chess Pieces**:
    - Return Unicode characters representing chess pieces based on their type.
8. **Socket.io Event Handlers**:
    - Listen for various events from the server such as player role assignment, spectator role assignment, board state updates, and opponent moves.
    - Update the local game state and render the board accordingly when receiving events.
9. **Initial Rendering**:
    - Call the `renderBoard` function initially to render the initial state of the chessboard.

## Running the Project

1. **Install Dependencies**:
    ```bash
    npm install
    ```

2. **Start the Server**:
    ```bash
    node app.js
    ```


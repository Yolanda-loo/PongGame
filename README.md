Pong: Tkinter Classic



A two-player Pong game built with Python and Tkinter, featuring a clean, intuitive UI and classic gameplay. Players control paddles to hit a ball back and forth, 
aiming to score by getting the ball past the opponent's paddle. First to 5 points wins!
Features

Clean UI: Start menu with instructions, game over screen with replay/quit options, and a dashed center line.
Scorekeeping: Displays scores prominently at the top.
Ball Physics: Smooth ball movement with paddle and wall collisions.
Customizable: Adjust paddle speed, ball speed, and paddle size via constants.
Tkinter-Based: Lightweight, no external dependencies beyond Python's standard library.


Installation

Install Python: Ensure Python 3.6+ is installed (python.org). Tkinter is included with standard Python installations.
Run the Game: Save the code as pong.py and run python pong.py.

How to Play

Start: Click the "Start" button on the menu.
Controls:
Player 1 (Left Paddle): W (up), S (down).
Player 2 (Right Paddle): Up Arrow (up), Down Arrow (down).


Objective: Hit the ball past the opponent's paddle to score. First to 5 points wins.
Game Over: Click "Replay" to start a new game or "Quit" to exit.

Customization
Modify these constants in pong.py to tweak the game:

PADDLE_SPEED: Paddle movement speed (default: 5 pixels/frame).
BALL_SPEED: Ball movement speed (default: 7 pixels/frame).
PADDLE_HEIGHT: Paddle size (default: 90 pixels).
MAX_SCORE: Points needed to win (default: 5).
Colors: Adjust BG_COLOR, PADDLE1_COLOR, PADDLE2_COLOR, etc., for visual customization.

Project Structure
pong/
├── pong.py              # Main game code
└── README.md            # This file

Technical Details

Language: Python 3 with Tkinter (standard library).
Game Loop: Uses root.after for ~60 FPS updates.
Physics: Basic collision detection for paddles and walls, with random ball direction on reset.
UI: Dark blue background, red/blue paddles, white ball, and clear Arial fonts for readability.
GitHub Appeal: Simple, dependency-free code with a modular class structure, ideal for beginner Tkinter projects.

Future Improvements

Add single-player AI mode.
Include sound effects (requires external libraries like pygame).
Support paddle spin for advanced ball control.
Add difficulty settings via a settings menu.

License
MIT License. Feel free to use, modify, and share!
Contact
For issues or suggestions, open a GitHub issue or reach out via londie970918@gmail.com

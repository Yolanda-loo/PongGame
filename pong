import tkinter as tk
import random
from tkinter import messagebox

class PongGame:
    def __init__(self, root):
        self.root = root
        self.root.title("Pong: Tkinter Classic")
        self.WIDTH = 800
        self.HEIGHT = 600
        self.PADDLE_WIDTH = 15
        self.PADDLE_HEIGHT = 90
        self.PADDLE_SPEED = 5
        self.BALL_SIZE = 10
        self.BALL_SPEED = 7
        self.MAX_SCORE = 5

        # Colors
        self.BG_COLOR = "#1e1e5f"  # Dark blue
        self.PADDLE1_COLOR = "#ff4040"  # Red
        self.PADDLE2_COLOR = "#4040ff"  # Blue
        self.BALL_COLOR = "#ffffff"  # White
        self.LINE_COLOR = "#ffffff"  # White

        # Game state
        self.score1 = 0
        self.score2 = 0
        self.game_state = "menu"
        self.ball_dx = self.BALL_SPEED * random.choice((1, -1))
        self.ball_dy = self.BALL_SPEED * random.choice((1, -1))

        # Create canvas
        self.canvas = tk.Canvas(self.root, width=self.WIDTH, height=self.HEIGHT, bg=self.BG_COLOR)
        self.canvas.pack()

        # Initialize game objects
        self.paddle1 = self.canvas.create_rectangle(
            50, self.HEIGHT // 2 - self.PADDLE_HEIGHT // 2,
            50 + self.PADDLE_WIDTH, self.HEIGHT // 2 + self.PADDLE_HEIGHT // 2,
            fill=self.PADDLE1_COLOR
        )
        self.paddle2 = self.canvas.create_rectangle(
            self.WIDTH - 50 - self.PADDLE_WIDTH, self.HEIGHT // 2 - self.PADDLE_HEIGHT // 2,
            self.WIDTH - 50, self.HEIGHT // 2 + self.PADDLE_HEIGHT // 2,
            fill=self.PADDLE2_COLOR
        )
        self.ball = self.canvas.create_oval(
            self.WIDTH // 2 - self.BALL_SIZE // 2, self.HEIGHT // 2 - self.BALL_SIZE // 2,
            self.WIDTH // 2 + self.BALL_SIZE // 2, self.HEIGHT // 2 + self.BALL_SIZE // 2,
            fill=self.BALL_COLOR
        )

        # Score display
        self.score_label = self.canvas.create_text(
            self.WIDTH // 2, 50, text="0  0", font=("Arial", 24), fill="white"
        )

        # Dashed center line
        for y in range(0, self.HEIGHT, 20):
            self.canvas.create_rectangle(self.WIDTH // 2 - 2, y, self.WIDTH // 2 + 2, y + 10, fill=self.LINE_COLOR)

        # Menu elements
        self.menu_label = self.canvas.create_text(
            self.WIDTH // 2, self.HEIGHT // 4, text="Pong: Tkinter Classic",
            font=("Arial", 36, "bold"), fill="white"
        )
        self.instructions = [
            self.canvas.create_text(self.WIDTH // 2, self.HEIGHT // 2, text="Player 1: W/S", font=("Arial", 16), fill="white"),
            self.canvas.create_text(self.WIDTH // 2, self.HEIGHT // 2 + 40, text="Player 2: Up/Down", font=("Arial", 16), fill="white"),
            self.canvas.create_text(self.WIDTH // 2, self.HEIGHT // 2 + 80, text="First to 5 wins!", font=("Arial", 16), fill="white")
        ]
        self.start_button = tk.Button(
            self.root, text="Start", font=("Arial", 16), command=self.start_game
        )
        self.start_button.place(x=self.WIDTH // 2 - 50, y=self.HEIGHT // 2 + 120, width=100)

        # Game over elements (hidden initially)
        self.game_over_label = None
        self.replay_button = None
        self.quit_button = None

        # Keyboard bindings
        self.root.bind("<KeyPress>", self.handle_input)
        self.root.focus_set()

        # Start game loop
        self.update_game()

    def start_game(self):
        self.game_state = "playing"
        self.start_button.place_forget()
        for text in self.instructions:
            self.canvas.delete(text)
        self.canvas.delete(self.menu_label)
        if self.game_over_label:
            self.canvas.delete(self.game_over_label)
            self.replay_button.place_forget()
            self.quit_button.place_forget()
        self.update_game()

    def reset_game(self):
        self.score1 = 0
        self.score2 = 0
        self.canvas.itemconfig(self.score_label, text="0  0")
        self.canvas.coords(
            self.paddle1, 50, self.HEIGHT // 2 - self.PADDLE_HEIGHT // 2,
            50 + self.PADDLE_WIDTH, self.HEIGHT // 2 + self.PADDLE_HEIGHT // 2
        )
        self.canvas.coords(
            self.paddle2, self.WIDTH - 50 - self.PADDLE_WIDTH, self.HEIGHT // 2 - self.PADDLE_HEIGHT // 2,
            self.WIDTH - 50, self.HEIGHT // 2 + self.PADDLE_HEIGHT // 2
        )
        self.reset_ball()
        self.start_game()

    def reset_ball(self):
        self.ball_dx = self.BALL_SPEED * random.choice((1, -1))
        self.ball_dy = self.BALL_SPEED * random.choice((1, -1))
        self.canvas.coords(
            self.ball,
            self.WIDTH // 2 - self.BALL_SIZE // 2, self.HEIGHT // 2 - self.BALL_SIZE // 2,
            self.WIDTH // 2 + self.BALL_SIZE // 2, self.HEIGHT // 2 + self.BALL_SIZE // 2
        )

    def handle_input(self, event):
        if self.game_state != "playing":
            return
        p1_coords = self.canvas.coords(self.paddle1)
        p2_coords = self.canvas.coords(self.paddle2)
        if event.keysym == "w" and p1_coords[1] > 0:
            self.canvas.move(self.paddle1, 0, -self.PADDLE_SPEED)
        if event.keysym == "s" and p1_coords[3] < self.HEIGHT:
            self.canvas.move(self.paddle1, 0, self.PADDLE_SPEED)
        if event.keysym == "Up" and p2_coords[1] > 0:
            self.canvas.move(self.paddle2, 0, -self.PADDLE_SPEED)
        if event.keysym == "Down" and p2_coords[3] < self.HEIGHT:
            self.canvas.move(self.paddle2, 0, self.PADDLE_SPEED)

    def update_ball(self):
        if self.game_state != "playing":
            return
        self.canvas.move(self.ball, self.ball_dx, self.ball_dy)
        ball_coords = self.canvas.coords(self.ball)
        p1_coords = self.canvas.coords(self.paddle1)
        p2_coords = self.canvas.coords(self.paddle2)

        # Ball collision with top and bottom
        if ball_coords[1] <= 0 or ball_coords[3] >= self.HEIGHT:
            self.ball_dy = -self.ball_dy

        # Ball collision with paddles
        if (ball_coords[0] <= p1_coords[2] and p1_coords[1] <= ball_coords[1] <= p1_coords[3]) or \
           (ball_coords[2] >= p2_coords[0] and p2_coords[1] <= ball_coords[1] <= p2_coords[3]):
            self.ball_dx = -self.ball_dx

        # Ball out of bounds
        if ball_coords[0] <= 0:
            self.score2 += 1
            self.canvas.itemconfig(self.score_label, text=f"{self.score1}  {self.score2}")
            self.reset_ball()
        elif ball_coords[2] >= self.WIDTH:
            self.score1 += 1
            self.canvas.itemconfig(self.score_label, text=f"{self.score1}  {self.score2}")
            self.reset_ball()

        # Check for game over
        if self.score1 >= self.MAX_SCORE or self.score2 >= self.MAX_SCORE:
            self.game_state = "game_over"
            winner = "Player 1" if self.score1 >= self.MAX_SCORE else "Player 2"
            self.game_over_label = self.canvas.create_text(
                self.WIDTH // 2, self.HEIGHT // 3, text=f"{winner} Wins! {self.score1} - {self.score2}",
                font=("Arial", 24, "bold"), fill="white"
            )
            self.replay_button = tk.Button(
                self.root, text="Replay", font=("Arial", 16), command=self.reset_game
            )
            self.quit_button = tk.Button(
                self.root, text="Quit", font=("Arial", 16), command=self.root.quit
            )
            self.replay_button.place(x=self.WIDTH // 2 - 100, y=self.HEIGHT // 2, width=80)
            self.quit_button.place(x=self.WIDTH // 2 + 20, y=self.HEIGHT // 2, width=80)

    def update_game(self):
        if self.game_state == "playing":
            self.update_ball()
        self.root.after(16, self.update_game)  # ~60 FPS

if __name__ == "__main__":
    root = tk.Tk()
    game = PongGame(root)
    root.mainloop()

# -Fernando
PAC man
import pygame
import sys
import random

# Initialize Pygame
pygame.init()

# Constants
WIDTH, HEIGHT = 600, 600
FPS = 60
PACMAN_RADIUS = 30
GHOST_RADIUS = 25

# Colors
BLACK = (0, 0, 0)
YELLOW = (255, 255, 0)
RED = (255, 0, 0)

# Create game window
screen = pygame.display.set_mode((WIDTH, HEIGHT))
pygame.display.set_caption("Pac-Man")

# Clock to control the frame rate
clock = pygame.time.Clock()

class Pacman:
    def __init__(self, x, y):
        self.x = x
        self.y = y
        self.radius = PACMAN_RADIUS
        self.angle = 0  # Mouth opening angle

    def draw(self):
        pygame.draw.circle(screen, YELLOW, (self.x, self.y), self.radius)
        mouth_rect = pygame.Rect(self.x - self.radius, self.y - self.radius, 2 * self.radius, 2 * self.radius)
        pygame.draw.pie(screen, BLACK, mouth_rect, self.angle, self.angle + 300)

class Ghost:
    def __init__(self):
        self.x = random.randint(GHOST_RADIUS, WIDTH - GHOST_RADIUS)
        self.y = random.randint(GHOST_RADIUS, HEIGHT - GHOST_RADIUS)
        self.radius = GHOST_RADIUS

    def draw(self):
        pygame.draw.circle(screen, RED, (self.x, self.y), self.radius)

# Create game objects
pacman = Pacman(WIDTH // 2, HEIGHT // 2)
ghost = Ghost()

# Game loop
while True:
    for event in pygame.event.get():
        if event.type == pygame.QUIT:
            pygame.quit()
            sys.exit()

    # Update
    pacman.angle += 5  # Animate Pac-Man's mouth

    # Draw
    screen.fill(BLACK)
    pacman.draw()
    ghost.draw()

    # Update display
    pygame.display.flip()

    # Cap the frame rate
    clock.tick(FPS)

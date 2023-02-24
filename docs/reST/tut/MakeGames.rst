
import pygame
import random

# Define the colors
BLACK = (0, 0, 0)
WHITE = (255, 255, 255)
RED = (255, 0, 0)
GREEN = (0, 255, 0)
BLUE = (0, 0, 255)

# Set the width and height of the screen
SCREEN_WIDTH = 800
SCREEN_HEIGHT = 600

# Set the speed of the player's car
PLAYER_SPEED = 5

# Initialize Pygame
pygame.init()

# Set the size of the screen
screen = pygame.display.set_mode((SCREEN_WIDTH, SCREEN_HEIGHT))

# Set the caption of the game window
pygame.display.set_caption("Racing Game")

# Load the images
player_car = pygame.image.load("player_car.png")
other_car = pygame.image.load("other_car.png")
coin = pygame.image.load("coin.png")
oil_slick = pygame.image.load("oil_slick.png")
roadblock = pygame.image.load("roadblock.png")

# Create the player's car
player_x = SCREEN_WIDTH / 2 - player_car.get_width() / 2
player_y = SCREEN_HEIGHT - player_car.get_height() - 50
player_rect = pygame.Rect(player_x, player_y, player_car.get_width(), player_car.get_height())

# Create the list of other cars
other_cars = []

# Create the list of coins
coins = []

# Create the list of obstacles
obstacles = []

# Create the font for the score
font = pygame.font.SysFont(None, 30)

# Set the starting score
score = 0

# Set the starting time
time = 60

# Set the level
level = 1

# Set the game state
game_over = False

# Set the clock
clock = pygame.time.Clock()

# The game loop
while not game_over:
    # Handle events
    for event in pygame.event.get():
        if event.type == pygame.QUIT:
            game_over = True

    # Move the player's car
    keys = pygame.key.get_pressed()
    if keys[pygame.K_LEFT] and player_x > 0:
        player_x -= PLAYER_SPEED
    if keys[pygame.K_RIGHT] and player_x < SCREEN_WIDTH - player_car.get_width():
        player_x += PLAYER_SPEED

    # Spawn other cars
    if random.randint(0, 100) < level:
        other_car_x = random.randint(0, SCREEN_WIDTH - other_car.get_width())
        other_car_y = -other_car.get_height()
        other_car_rect = pygame.Rect(other_car_x, other_car_y, other_car.get_width(), other_car.get_height())
        other_cars.append(other_car_rect)

    # Spawn coins
    if random.randint(0, 1000) < level:
        coin_x = random.randint(0, SCREEN_WIDTH - coin.get_width())
        coin_y = -coin.get_height()
        coin_rect = pygame.Rect(coin_x, coin_y, coin.get_width(), coin.get_height())
        coins.append(coin_rect)

    # Spawn obstacles
    if random.randint(0, 100) < level:
        obstacle_x = random.randint(0, SCREEN_WIDTH - roadblock.get_width())
        obstacle_y = -roadblock.get_height()
        obstacle_rect = pygame.Rect(obstacle_x, obstacle_y, roadblock

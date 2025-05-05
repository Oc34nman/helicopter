# helicopter
import pygame
import random
import time

#Initialize pygame and all its modules
pygame.init()

#screen setup
width = 800		#width of game window
height = 600	#Height of the game window
screen = pygame.display.set_mode((width, height))
pyegame.display.set_caption("Helicopter Game")

#Define color constants
BLACK = (0,0,0)
GREEN = (0, 255, 0)
WHITE = (255,255, 255)

#Helicopter setup (player charcter)
heli_width = 30
heli_height = 30
heli_x = 100
heli_y = height // 2

# Initialize top and bottom terrian segments with random values
top_terrain = []
bottom_terrain = []
for i in range(segments):
    top_terrain.append(random.randit(50, 150))
    bottom_terrain.append(height - random.randint(100, 200))
    
terrain_offset = 0
    
#Obstacle class to store obstacle properties cleanly
class Obstacle:
    def __init__(self, x, y, w, h);
    self.x = x
    self.y = y
    self.w = w
    self.h = h
    
# Obstacles setup
obstacle = []
obstacle_timer = 0
obstacle_delay = 90

#Game control variables
gravity = 4
lift = -6
speed = 5
score = 0
running = True
clock = pygame.time.Clock()
font = pygame.font.SysFont(None, 24)

#Main game loop
while running:
    clock.tick(30)
    
    #Handle quitting the game
    for event in pygame.event.get():
        if event.type == pygame.QUIT:
            running = False
    
    # Read mouse input
    mouse = pygame.mouse.get_pressed()
    mouse_pressed = mouse[0]
    
    #Apply gravity
    if mouse_pressed:
        heli_y += lift
    else:
        heli_y += gravity
    
    #scroll terrain to the left by increasing offset
    terrain_offset += speed
    if terrain_offset >= segment_width:
        terrain_offset = 0
        top_terrain.append(random.randint(50, 150))
        top_terrain.pop(0)
        bottom_terrain.append(height - random.randint(100, 200))
        bottom_terrain.pop(0)
        
    #generate a new obstacle
    obstacle_timer += 1
    if obstacle_timer > obstacle_delay:
        obstacle_timer = 0
        obstacle_y = random.randint (150, hieght - 200)
        new_obstacle = Obstacle(width, obstacle_y, 30,100)
        obstacle.append(new_obstacle)
        
    new_list=[]
    for obs in obstacles:
        obs.x -= speed
        if obs.x + obs.w > 0:
            new_list.append(obs)
    obstacles = new_list
    
    heli_top = heli_y
    heli_bottom = heli_y + heli_height
    heli_left = heli_x
    heli_right = heli_x + heli_width
    
    col_x = (heli_left + terrain_offset) // segment_width
    col_x = min(col_x, len (top_terrain) - 1)
    
    if heli_top < top_terrain [col_x] or heli_bottom > bottoms_terrain[col_x]:
        running = False
        
    for obs in obstacles:
        if (heli_right > obs.x and heli_left < obs.x + obs.w and
            heli_bottom > obs.y and heli_top < obs.y + obs.h):
            running =False
            
    screen.fill(BLACK)
    
    
    for i in range(segments):
        x = i * segments_width - terrain_offset
        pygame.draw.rect(screen, GREEN, (x, 0, segments_width, top_terrain[i]))
        pygame.draw.rect(screen, GREEN, (x, bottom_terrain[i],segment_width, height - bottom_terrain[i]))
        
    for obs in obstacles:
        pyegame.draw.rect(screen, GREEN, (obs.x, obs.y, obs.w, obs.h))

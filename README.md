# landscape_ICS_classwork
# Pygame Compund Shapes
import math
import pygame
from pygame.locals import K_ESCAPE, KEYDOWN, QUIT, MOUSEBUTTONDOWN


pygame.init()

WIDTH = 640
HEIGHT = 460
SIZE = (WIDTH, HEIGHT)

screen = pygame.display.set_mode(SIZE)
clock = pygame.time.Clock()

# ---------------------------
# Initialize global variables
day = (204, 229, 255)
night = (0, 0, 102)
cloud_x = 1
cloud_y = 0
sun_x = 0
sun_y = 45
window_1 = (233, 267, 50, 50)
window_2 = (340, 267, 50, 50)
sunny = (255, 255, 0)
moony = (192, 192, 192)
sun_color = sunny
yellow =(255, 255, 102)
background_color = day
white = (255, 255, 255)
window = white
# ---------------------------

running = True
while running:
    # EVENT HANDLING
    for event in pygame.event.get():
        if event.type == KEYDOWN:
            if event.key == K_ESCAPE:
                running = False
        elif event.type == QUIT:
            running = False
        elif event.type == MOUSEBUTTONDOWN:
            print(event.pos)

    # GAME STATE UPDATES
    #Sun/moon transition + cloud
    cloud_x += 5
    if background_color == day:
        if sun_x <= WIDTH:
            sun_x += 3
            moony = sunny
        elif sun_x >= WIDTH:
            sun_color = white
            background_color = night
            window = yellow
            sun_x = 0
    if background_color == night:
        if sun_x <= WIDTH:
            sun_x += 3
            moony = (192, 192, 192)
        elif sun_x >= WIDTH:
            sun_color = sunny
            background_color = day
            window = white
            sun_x = 0
    if cloud_x > WIDTH:
        cloud_x = 0
    cloud_y = math.sin(cloud_x/50) * 25 + HEIGHT//5
    sun_y = math.cos(sun_x/110) * 220 + HEIGHT//2
    # All game math and comparisons happen here

    # DRAWING
    screen.fill(background_color)
    pygame.draw.circle(screen, (sun_color), (sun_x, sun_y), 25)
    pygame.draw.circle(screen, (moony), (sun_x +7, sun_y -7), 6)
    pygame.draw.circle(screen, (moony), (sun_x -9, sun_y -1), 9)
    pygame.draw.circle(screen, (moony), (sun_x +6, sun_y +12), 7)
    pygame.draw.circle(screen, (255, 255, 255), (cloud_x, cloud_y), 25) 
    pygame.draw.circle(screen, (255, 255, 255), (cloud_x + 14, cloud_y + 6), 25)
    pygame.draw.circle(screen, (255, 255, 255), (cloud_x + 27, cloud_y - 18), 25)
    pygame.draw.circle(screen, (255, 255, 255), (cloud_x + 50, cloud_y + 1), 25)
    pygame.draw.rect(screen, ("#6e2c00"), (200, 240, 230, 200))
    pygame.draw.polygon(screen, ("#641e16"), [(200, 240), (430, 240), (312, 150)])
    pygame.draw.line(screen, ("#17202a"), (200, 240), (430, 240), 3)
    pygame.draw.line(screen, ("#17202a"), (312, 150), (450, 260), 10)
    pygame.draw.line(screen, ("#17202a"), (312, 150), (180, 260), 10)
    pygame.draw.rect(screen, (window), (window_1))
    pygame.draw.rect(screen, (window), (window_2))
    pygame.draw.rect(screen, (225, 0, 0), (285, 353, 50, 100))
    pygame.draw.circle(screen, ("#ffff00"), (326, 393), 5)
    pygame.draw.rect(screen, ("#009900"), (0, 440, 1000, 500))
    
    


    # Must be the last two lines
    # of the game loop
    pygame.display.flip()
    clock.tick(30)
    #---------------------------


pygame.quit()

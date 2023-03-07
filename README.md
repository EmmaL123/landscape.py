# landscape.py

import pygame
from pygame.locals import K_ESCAPE, KEYDOWN, QUIT

pygame.init()

WIDTH = 640
HEIGHT = 640
SIZE = (WIDTH, HEIGHT)

screen = pygame.display.set_mode(SIZE)
clock = pygame.time.Clock()

# ---------------------------
# Initialize global variables

# WATER
water_height = 220
dark_blue = (00,0,205)
water_surface = 420

# SKY
sky_blue = (153,251,252)
tiffany = (138,242,223)
emerald = (144,218,155)
yellow_green = (175,187,87)
dark_yellow = (192,168,61)
orange1 = (208,146,46)
orange2 = (222,121,46)
red = (232,92,60)

orange3 = (246,125,49)
orange4 = (254,158,39)
orange5 = (255,175,36)
yellow = (255,255,153)
pale_yellow = (250,251,157)
pale_green = (204,255,187)
turquoise = (173,254,221)
light_blue = (186,238,253)

sky = sky_blue

# SUN
sun_yellow = (255,255,0)
sun_x = 400
sun_y = 150
sun_radius = 65

# MOUNTAINS
dark_green = (34,139,34)
light_green = (50,205,50)

# BOAT
brown = (139,69,19)
white = (255,255,255)
grey = (220,220,220)
boat_x = 0
boat_y = 500

# SUN MOVEMENT
sun_down = True

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

    # GAME STATE UPDATES
    # All game math and comparisons happen here

    sky = sky_blue

    # BOAT MOVEMENT
    boat_x += 5
    if boat_x == WIDTH:
        boat_x = - boat_x

    # SUN MOVEMENT
    if sun_y == 150:
        sun_down = True
    if sun_y >= 420:
        sun_down = False
    if sun_down == True:
        sun_y += 2
    else:
        sun_y -= 2
    
    if sun_down == True:
        if sun_y >= 150 and sun_y < 184:
            sky = sky_blue
        elif sun_y >= 184 and sun_y < 218:
            sky = tiffany
        elif sun_y >= 218 and sun_y < 256:
            sky = emerald
        elif sun_y >= 256 and sun_y < 286:
            sky = yellow_green
        elif sun_y >= 286 and sun_y < 320:
            sky = dark_yellow
        elif sun_y >= 320 and sun_y < 354:
            sky = orange1
        elif sun_y >= 354 and sun_y < 388:
            sky = orange2
        elif sun_y >= 388 and sun_y <= 420:
            sky = red
    else:
        if sun_y >= 150 and sun_y < 177:
            sky = sky_blue
        elif sun_y >= 177 and sun_y < 204:
            sky = light_blue
        elif sun_y >= 204 and sun_y < 231:
            sky = turquoise
        elif sun_y >= 231 and sun_y < 258:
            sky = pale_green
        elif sun_y >= 258 and sun_y < 285:
            sky = pale_yellow
        elif sun_y >= 285 and sun_y < 312:
            sky = yellow
        elif sun_y >= 312 and sun_y < 339:
            sky = orange5
        elif sun_y >= 339 and sun_y < 266:
            sky = orange4
        elif sun_y >= 266 and sun_y < 393:
            sky = orange3
        elif sun_y >= 393 and sun_y <= 420:
            sky = red

    # DRAWING
    screen.fill(sky)  # SKY

    pygame.draw.circle(screen, (yellow), (sun_x, sun_y), sun_radius) # SUN

    pygame.draw.rect(screen, (dark_blue), (0, water_surface, WIDTH, water_height)) # WATER

    pygame.draw.polygon(screen, (light_green), ((130, water_surface), (320, 100), (500, water_surface))) # MIDDLE MOUNTAIN
    pygame.draw.polygon(screen, (dark_green), ((0, water_surface), (210, 200), (420, water_surface))) # LEFT MOUNTAIN
    pygame.draw.polygon(screen, (dark_green), ((300, water_surface), (470, 150), (WIDTH, water_surface))) # RIGHT MOUNTAIN

    pygame.draw.polygon(screen, (brown), ((boat_x,boat_y), (boat_x+200,boat_y), (boat_x+160,boat_y+80), (boat_x+40,boat_y+80))) # HULL
    pygame.draw.polygon(screen, (grey), ((boat_x+40,boat_y), (boat_x+100,boat_y), (boat_x+100,boat_y-100))) # LEFT SAIL
    pygame.draw.polygon(screen, (white), ((boat_x+100,boat_y-15), (boat_x+150,boat_y-15), (boat_x+100,boat_y-100))) # RIGHT SAIL

    pygame.display.flip()
    clock.tick(30)
    #---------------------------

pygame.quit()

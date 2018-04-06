import pygame        #provides what we need to make a game
import sys           #gives us the sys.exit function to close our program
import random        #can generate random positions for the pong ball
from pygame.locals import*

pygame.init()

gameSurface = pygame.display.set_mode((450,400))                    #open a new window width = 450, height=400
pygame.display.set_caption('Domingo Gonzales III\'s Neon Pong Game')     #set the title of the window
pygame.mouse.set_visible(0)

GREEN    = (0,200,0)
BLUE     = (0,0,128)
PURPLE   = (102,0,102)
BLACK    = (0,0,0)           #changed white to black
NEONBLUE = (132,188,213)
ORANGE   = (255,122,66)

rect1x=20
rect1y=100        #draw the game surface, two rectangles. One at position 20, 100, 30 pixes wide and 150 tall
rect2x=400        #the other rectangle and 400, 100, with the same measurements
rect2y=100
rect3x=150
rect3y=20
rect4x=150
rect4y=300

gameSurface.fill(BLACK)
pygame.draw.rect(gameSurface, NEONBLUE,(rect1x, rect1y,30,150)) #added NEONBLUE as a color and changed rectangles frpm green
pygame.draw.rect(gameSurface, NEONBLUE,(rect2x, rect2y,30,150))
pygame.draw.rect(gameSurface, NEONBLUE,(rect3x, rect3y,150,30)) #added two horizontal rectangles
pygame.draw.rect(gameSurface, NEONBLUE,(rect4x, rect4y,150,30))

#put the ball on a random place on the screen
ballx=random.randint(200,300)
bally=random.randint(100,150)
pygame.draw.circle(gameSurface, GREEN,(ballx, bally),20)        #changed ball color to green
pygame.display.update()

FPS=60                              #speed ball up from 20 fps
fpsClock=pygame.time.Clock()
pygame.key.set_repeat(1,1)          #this will allow you to press and hold keys on the keyboard

#game loop
while True:
    for event in pygame.event.get():

        oldballx=ballx
        oldbally=bally

        if event.type==KEYDOWN:     #pressing q will quit the program

            if event.key == K_q:
                pygame.quit()
                sys.exit()
            if event.key == K_SPACE:      #pressing space will turn the ball orange until next event.key of an kind
                pygame.draw.circle(gameSurface, ORANGE,(ballx, bally),20)
            if event.key == K_RIGHT:      #the right arrow key
                ballx=ballx+1             #this moves the ball. Turn the old ball location white then create a new ball at the new location simulating movement
                pygame.draw.circle(gameSurface, BLACK,(oldballx, oldbally),20) 
                pygame.draw.circle(gameSurface, GREEN,(ballx, bally),20)
            if event.key == K_LEFT:       #the left arrow key
                ballx=ballx-1
                pygame.draw.circle(gameSurface, BLACK,(oldballx, oldbally),20)
                pygame.draw.circle(gameSurface, GREEN,(ballx, bally),20)
            if event.key == K_UP:         #the up arrow key                   #these two if statements plus oldbally allow the ball to move up and down as well
                bally=bally-1
                pygame.draw.circle(gameSurface, BLACK,(oldballx, oldbally),20)
                pygame.draw.circle(gameSurface, GREEN,(ballx, bally),20)
            elif event.key == K_DOWN:     #the down arrow key
                bally=bally+1
                pygame.draw.circle(gameSurface, BLACK,(oldballx, oldbally),20)
                pygame.draw.circle(gameSurface, GREEN,(ballx, bally),20)

        if ballx==70:
            pygame.draw.rect(gameSurface, PURPLE,(rect1x, rect1y,30,150))   #if the ball reaches the rectangle on the left side turn it purple
        if ballx==380:
            pygame.draw.rect(gameSurface,PURPLE,(rect2x, rect2y,30,150))    #if the ball reaches the rectangle on the right side turn it purple
        if bally==70:
            pygame.draw.rect(gameSurface, PURPLE,(rect3x, rect3y,150,30))   #if the ball reaches the rectangle on the top side turn it purple
        if bally==280:
            pygame.draw.rect(gameSurface,PURPLE,(rect4x, rect4y,150,30))    #if the ball reaches the rectangle on the bottom side turn it purple
            
        pygame.display.update()       
    
    fpsClock.tick(FPS)     
            
pygame.display.update()

# cookie-clicker
#gopher mash
#written by Dr. Mo, 11/10/2020
import pygame
import math #needed for square root function



pygame.init()#initializes Pygame
print(pygame.font.get_fonts())
pygame.display.set_caption("Cookie Clicker")#sets the window title
screen = pygame.display.set_mode((400,400))#creates game screen

print(pygame.font.get_fonts())
#player variables
xpos = 0
ypos = 0
mousePos = (xpos, ypos) #variable mousePos stores TWO numbers
numClicks = 0
isBig = False
#circle variables: circX and circY are the coordinates of the center (where it's drawn), and the radius is how big it is
circX = 200
circY = 200
radius = 100

pic = pygame.image.load("cookie.png")
rect = pic.get_rect(topleft=(100,100))
pic2 = pygame.image.load("cookie2.png")
rect2 = pic2.get_rect(topleft=(90,90))

font = pygame.font.Font('freesansbold.ttf',32)
text1 = font.render('score:', False, (0, 200, 200))
text2 = font.render(str(int(numClicks)) ,1, (0, 200, 200))
#gameloop###################################################
while True:
#event queue (bucket that holds stuff that happens in game and passes to one of the sections below)
    event = pygame.event.wait()

    if event.type == pygame.QUIT: #close game window
        break

    if event.type == pygame.MOUSEBUTTONDOWN: #check if clicked
      if math.sqrt((circX - mousePos[0])**2 + (circY - mousePos[1])**2)<radius:
        numClicks+=1
      print("CLICK")

    if event.type == pygame.MOUSEMOTION: #check if mouse moved
        mousePos = event.pos #refreshes mouse position
        print("mouse position: (",mousePos[0]," , ",mousePos[1], ")")
        if math.sqrt((circX - mousePos[0])**2 + (circY - mousePos[1])**2)<radius:
          isBig = True
        else:
          isBig = False
 
#render section---------------------------------------------

    screen.fill((255, 255, 255)) #wipe screen (without this, things smear)
    if isBig == False:
      screen.blit(pic,rect)
    else:
      screen.blit(pic2,rect2)

    text2 = font.render(str(int(numClicks)) ,1, (0, 200, 200))
    screen.blit(text1, (10,10))
    screen.blit(text2, (110, 10))
    #pygame.draw.circle(screen, (200, 0, 200), (circX,circY), radius)
    print("clicks:", numClicks) #uncomment this once collision is set up
        
    pygame.display.flip()
    

#end game loop##############################################

pygame.quit()




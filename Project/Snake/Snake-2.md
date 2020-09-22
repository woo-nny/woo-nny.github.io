---
layout: page
title: 뱀꼬리 2일차
description: >
  뱀꼬리
comments: true
hide_description: true
---

## 뱀꼬리 2일차

### J - 화면 밖 이동시 Game Over, 먹이 랜덤 생성
```python
import pygame
import time 
import random
from datetime import datetime
from datetime import timedelta

pygame.init() # pygame 초기화
SCREEN_WIDTH = 400 # 스크린 가로
SCREEN_HEIGHT = 300 # 스크린 세로
screen = pygame.display.set_mode((SCREEN_WIDTH,SCREEN_HEIGHT )) # 화면 크기
font = pygame.font.SysFont("consolas",20)
# RGB 색깔 기존 변수
BLACK= ( 0,  0,  0)
WHITE= (255,255,255)
BLUE = ( 0,  0,255)
GREEN= ( 0,255,  0)
RED  = (255,  0,  0)
BLOCK_SIZE = 20
pygame.display.set_caption("J-Dragon Snake") # 게임 제목
done =False
clock=pygame.time.Clock() # FPS 화면을 초당 몇 번 출력 하겠는가?
flag =None
block_position = [0, 0]  # 블록의 위치 (y, x)
food_y = random.randint(0,15)
food_x = random.randint(0,20)
food_position=[food_y,food_x] # 먹이 위치
last_moved_time_block = datetime.now()
last_moved_time_food = datetime.now()



def draw_background(screen): #게임 배경 그린다
    background = pygame.Rect((0,0),(SCREEN_WIDTH,SCREEN_HEIGHT))
    pygame.draw.rect(screen,WHITE,background)
def draw_block(screen,color,position): #position 위치에 color 색깔의 블록 그린다
    block = pygame.Rect((position[1]*BLOCK_SIZE,position[0]*BLOCK_SIZE),(BLOCK_SIZE,BLOCK_SIZE)) # y,x좌표
    pygame.draw.rect(screen,color,block)
def printText(msg,color = 'BLACK', pos=(50,50)): #메시지 출력
    textSurface = font.render(msg,True,pygame.Color(color),None)
    textRect = textSurface.get_rect()
    textRect.topleft = pos

    screen.blit(textSurface,textRect)

while not done: # 무한 반복
    clock.tick(10) # 프레임 10,30,60 적당 높을 수록 cpu 사용량 증가
    for event in pygame.event.get(): # 게임 이벤트 발생 여부 확인
        printText("Please press any key.",'WHITE') #처음 시작 하려면 아무 키 입력
        if event.type == pygame.KEYDOWN: # 키를 누르면 flag TURE
            flag =True
        elif event.type == pygame.QUIT: # 이벤트가 quit 클릭 시
            done = True # 무한반복 나감
    if flag == True:
        if block_position[0]<0 or block_position[0]>14 or block_position[1]<0 or block_position[1]>19: # 영역 밖으로 갈 시 Game over
            printText('Game Over','BLACK')
        else:
            pressed = pygame.key.get_pressed() #pressed =  키
            if pressed[pygame.K_RIGHT]: # 오른쪽
                block_position[1] += 1
                # print("Right",block_position)
            elif pressed[pygame.K_LEFT]: # 왼쪽
                block_position[1] -= 1   
                # print("LEFT",block_position)
            elif pressed[pygame.K_UP]: # 위쪽
                block_position[0] -= 1
                # print("UP",block_position)
            elif pressed[pygame.K_DOWN]: # 아래쪽
                block_position[0] += 1  
                # print("DOWN",block_position)
            if timedelta(seconds=1) <= datetime.now() - last_moved_time_block:
                block_position[1] += 1 #오른쪽
                last_moved_time_block = datetime.now()
            if timedelta(seconds=10) <= datetime.now() - last_moved_time_food: # 먹이 10초가 지나면 새로운 곳에 먹이 생성
                food_y = random.randint(0,15)
                food_x = random.randint(0,20)
                food_position=[food_y,food_x]
                last_moved_time_food = datetime.now()
            draw_background(screen)
            draw_block(screen, GREEN, block_position) #뱀
            draw_block(screen,RED,food_position) # 먹이
    pygame.display.flip()
pygame.QUIT
```

### Dragon - 마우스 클릭에 따라 초록점이 움직임, 일정선을 지나가면 gameover가 뜨게 만듬, 랜덤으로 먹이가 생기게 만듬
```python
import pygame, sys
import random
from datetime import timedelta, datetime
import time


pygame.init()   
ScreenSize = (800,800)                 
screen = pygame.display.set_mode(ScreenSize) # 화면크기 설정  
pygame.display.set_caption('Snake Game')         # 윈도우 타이틀 설정


balck = (0,0,0)
white = (255,255,255)
red = (255,0,0)
green = (0,255,0)
blue = (0,0,255)

font = pygame.font.Font('freesansbold.ttf', 32)
text = font.render('Game Over', True, green, blue)

X = 101 # 마우스 X좌표
Y = 101 # 마우스 Y좌표
change_X = 101 #변화된 좌표
change_Y = 101 #변화된 좌표

feed_X = random.randint(100,700)
feed_Y = random.randint(100,700)

height = 10
snake_height_lis = pygame.draw.rect(screen, green, [X,Y,10,height])
Interval = timedelta(seconds=10)
lasttime = datetime.now()

flag = False

while True:  

    for event in pygame.event.get():
        if event.type == pygame.QUIT: 
            pygame.quit()
            sys.exit()
        elif event.type == pygame.MOUSEMOTION:
            a,b = pygame.mouse.get_pos() # 마우스 움직임에 따른 X,Y좌표
            if a > X and abs(a - X) > abs(b - Y):
                change_X = X + 10
            elif a < X and abs(a - X) > abs(b - Y):
                change_X = X - 10
            elif b > Y and  abs(a - X) < abs(b - Y):
                change_Y = Y + 10
            elif b < Y and abs(a - X) < abs(b - Y):
                change_Y = Y - 10
        elif event.type == pygame.MOUSEBUTTONDOWN:
            if change_X != X or change_Y != Y:
                X = change_X
                Y = change_Y

    if Interval < datetime.now() - lasttime:
        feed_X = random.randint(100,700)
        feed_Y = random.randint(100,700)
        lasttime = datetime.now()
    

    screen.fill(white)
    pygame.draw.lines(screen, red, True,[(100,100),(100,700),(700,700),(700,100)],5)
    pygame.draw.rect(screen, green, [X,Y,10,height])
    pygame.draw.rect(screen, balck, [feed_X,feed_Y,5,5])
    if X < 100 or X > 700 or Y < 100 or Y > 700:
        textRect = text.get_rect()
        textRect.center = (ScreenSize[0] // 2, ScreenSize[1] // 2)
        screen.blit(text,textRect)
    
            
    pygame.display.flip()
```
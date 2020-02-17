---
layout: page
title: 뱀꼬리 3일차
description: >
  뱀꼬리
comments: true
hide_description: true
---

## 뱀꼬리 3일차

### J - 먹이를 먹을 시 뱀 크기 증가, 게임 벽면 및 뱀 스스로 자기 몸에 접촉시 게임 종료

```python
import pygame
import time 
import random
from datetime import datetime
from datetime import timedelta

pygame.init() # pygame 초기화
SCREEN_WIDTH = 500 # 스크린 가로
SCREEN_HEIGHT = 500 # 스크린 세로
BLOCK_SIZE = 20
screen = pygame.display.set_mode((SCREEN_WIDTH,SCREEN_HEIGHT )) # 화면 크기
font = pygame.font.SysFont("consolas",20)
# RGB 색깔 기존 변수
BLACK= ( 0,  0,  0)
WHITE= (255,255,255)
BLUE = ( 0,  0,255)
GREEN= ( 0,255,  0)
RED  = (255,  0,  0)

pygame.display.set_caption("J-Dragon Snake") # 게임 제목
done =False
clock=pygame.time.Clock() # FPS 화면을 초당 몇 번 출력 하겠는가?
last_turn_time = datetime.now()
DIRECTION_ON_KEY = {
    pygame.K_UP : 'north',
    pygame.K_DOWN :'south',
    pygame.K_LEFT : 'west',
    pygame.K_RIGHT : 'east'
}
block_direction = 'east'
game_over=True
def draw_background(screen): #게임 배경 그린다
    background = pygame.Rect((0,0),(SCREEN_WIDTH,SCREEN_HEIGHT))
    pygame.draw.rect(screen,WHITE,background)
def draw_block(screen,color,position): #position 위치에 color 색깔의 블록 그린다
    block = pygame.Rect((position[1]*BLOCK_SIZE,position[0]*BLOCK_SIZE),(BLOCK_SIZE,BLOCK_SIZE)) # y,x좌표
    pygame.draw.rect(screen,color,block)
# def printText(msg): #메시지 출력
#     textSurface = font.render(msg,True,BLACK,BLUE)
#     textRect = textSurface.get_rect()
#     textRect.center = (50,50)
#     screen.blit(textSurface,textRect)
class Snake: #뱀
    color = GREEN # 뱀 색
    def __init__(self):
        self.position = [(9,6),(9,7),(9,8),(9,9)]
        self.direction = 'north' #뱀 처음 방향
    def draw(self,screen): # 뱀 그리기
        for position in self.position:
            draw_block(screen,self.color,position)
    def move(self): # 뱀 움직임
        head_position = self.position[0] # 뱀 머리 위치
        y,x = head_position
        if self.direction == 'north': #방향 위쪽
            self.position = [(y - 1, x)] + self.position[:-1]
        elif self.direction == 'south': # 방향 아래쪽
            self.position = [(y + 1, x)] + self.position[:-1]
        elif self.direction == 'west': # 방향 왼쪽
            self.position = [(y, x - 1)] + self.position[:-1]
        elif self.direction == 'east': # 방향 오른쪽
            self.position = [(y, x + 1)] + self.position[:-1]
        # print(self.position[0])
    def turn(self,direction):
        self.direction= direction
    def grow(self): # 먹이 먹을시
        tail_positon = self.position[-1] #꼬리 위치
        y,x = tail_positon
        if self.direction == 'north':
            self.position.append((y - 1, x))
        elif self.direction == 'south':
            self.position.append((y + 1, x))
        elif self.direction == 'west':
            self.position.append((y, x - 1))
        elif self.direction == 'east':
            self.position.append((y, x + 1))
class food: # 먹이
    color = RED # 먹이 색
    def __init__(self,position=(5,5)):
        self.position = position # 먹이 위치
    def draw(self,screen): #먹이 그림
        draw_block(screen,self.color,self.position)
class GameBoard: # 게임판

    def __init__(self):
        self.Snake =Snake()
        self.food = food()
    def draw(self,screen): #게임판 그리기
        self.Snake.draw(screen)
        self.food.draw(screen)
    def process_turn(self): # 게임 한판
        self.Snake.move()
        a,b=self.Snake.position[0]
        if self.Snake.position[0] == self.food.position: # 뱀 머리가 먹이 위치와 같을 경우
            self.Snake.grow()
            self.put_new_food()
        if self.Snake.position[0] in self.Snake.position[1:]: #뱀 머리가 몸에 닫을 경우
            game_over=True
            return game_over
        if a <= 0 or a >= 24 or b <= 0 or b >= 24: # 좌표 a,b 게임판을 벗어날 경우
            game_over=True
            return game_over
    def put_new_food(self): # 새로운 먹이 놓는 것
        self.food = food((random.randint(0,20),random.randint(0,20)))
        for position in self.Snake.position:
            if self.food.position == position:
                self.put_new_food()
                break
game = GameBoard()
TURN_INTERVAL = timedelta(seconds=0.3)
while True: # 무한 반복
    clock.tick(60) # 프레임 10,30,60 적당 높을 수록 cpu 사용량 증가
    for event in pygame.event.get(): # 게임 이벤트 발생 여부 확인
        if event.type == pygame.KEYDOWN: # 키를 누르면 flag TURE
            if event.key in DIRECTION_ON_KEY:
                game.Snake.turn(DIRECTION_ON_KEY[event.key])
        if event.type == pygame.QUIT: # 이벤트가 quit 클릭 시
            pygame.QUIT
    if TURN_INTERVAL < datetime.now() - last_turn_time:
        if game.process_turn():
            text = font.render('Game Over', T+rue, BLACK, BLUE)
            textRect = text.get_rect()
            textRect.center = (250,250)
            screen.blit(text,textRect)
            game.draw(screen)
            pygame.display.flip()
            time.sleep(2)
            break
        else:
            last_turn_time = datetime.now()
            draw_background(screen)
            game.draw(screen)
            pygame.display.flip()
```

### Dragon - 먹이를 먹을시 뱀 증가, 게임 종료 조건 추가

```python
import pygame, sys
from pygame.locals import *
import random
from datetime import timedelta, datetime
import time

#뱀 클래스
class Snake:
    def __init__(self): # 뱀생성
        self.position = [[130,130]]
        self.direction = "under" # 자동으로 움직이는 방향
    # 시간의 흐름에 따른 기본적인 움직임과 마우스 클릭에 따른 움직임을 정해주는 함수
    def automove(self):
        X, Y = self.position[0]
        if self.direction == "right":
            self.position = [[X+10,Y]] + self.position[:-1]
        elif self.direction == "left":
            self.position = [[X-10,Y]] + self.position[:-1]
        elif self.direction == "over":
            self.position = [[X,Y+10]] + self.position[:-1]
        else :
            self.position = [[X,Y-10]] + self.position[:-1]
    # 마우스 클릭에 따라 어느 방향으로 얼마만큼 이동할지 판단해주는 함수.
    def movement(self, a,b):
        X, Y = self.position[0]
        if a >= X and abs(a - X) >= abs(b - Y):
            self.direction = "right"
        elif a <= X and abs(a - X) >= abs(b - Y):
            self.direction = "left"
        elif b >= Y and  abs(a - X) <= abs(b - Y):
            self.direction = "over"
        elif b <= Y and abs(a - X) <= abs(b - Y):
            self.direction = "under"
    # 먹이를 먹어 커지는 경우
    def grow(self):
        if (feed.feed_X - 10 <= snake.position[0][0] <= feed.feed_X + 10 
        and feed.feed_Y - 10 <= snake.position[0][1] <= feed.feed_Y + 10):
            feed.change_position()
            X,Y = self.position[-1]
            if self.direction == "right":
                self.position.append([X-10,Y])
            elif self.direction == "left":
                self.position.append([X+10,Y])
            elif self.direction == "over":
                self.position.append([X,Y-10])
            else :
                self.position.append([X,Y+10])
    # 죽는 경우
    def die(self):
        if self.position[0] in self.position[1:] or (snake.position[0][0] < 100 or snake.position[0][0] > 350 
        or snake.position[0][1] < 100 or snake.position[0][1] > 350):
            textRect = text.get_rect()
            textRect.center = (ScreenSize[0] // 2, ScreenSize[1] // 2)
            return screen.blit(text,textRect)

class Feed:
    def __init__(self):
        self.feed_X = random.randint(100,350)
        self.feed_Y = random.randint(100,350)
    def change_position(self):
        self.feed_X = random.randint(100,350)
        self.feed_Y = random.randint(100,350)
        
class get_click:
    def __init__(self):
        self.X = 150
        self.Y = 140
    def getpoint(self):
        a, b = pygame.mouse.get_pos()
        self.X = a
        self.Y = b




pygame.init()   
ScreenSize = (800,800)
screen = pygame.display.set_mode(ScreenSize) # 화면크기 설정  
pygame.display.set_caption('Snake Game')         # 윈도우 타이틀 설정


black = (0,0,0)
white = (255,255,255)
red = (255,0,0)
green = (0,255,0)
blue = (0,0,255)

font = pygame.font.Font('freesansbold.ttf', 32)
text = font.render('Game Over', True, green, blue)

snake = Snake()
feed = Feed()
click = get_click()

Interval = timedelta(seconds=10)
lasttime = datetime.now()
sec = datetime.now()
sec_interval = timedelta(seconds=1)


pygame.K_PAUSE
while snake.die() == None:  
    Change_Flag = False
    for event in pygame.event.get():
        if event.type == pygame.QUIT: 
            pygame.quit()
            sys.exit()
        elif event.type == pygame.MOUSEBUTTONDOWN:
            click.getpoint()
            Change_Flag = True
    

    if Interval < datetime.now() - lasttime:
        feed.feed_X, feed.feed_Y = random.randint(100,350), random.randint(100,350)
        lasttime = datetime.now()
    if datetime.now() - sec > sec_interval or Change_Flag:
        snake.movement(click.X,click.Y)
        snake.automove()
        sec = datetime.now()
    snake.grow()


    screen.fill(white)
    pygame.draw.lines(screen, red, True,[(100,100),(100,350),(350,350),(350,100)],5)
    for X,Y in snake.position:
        pygame.draw.rect(screen, green, [X,Y,10,10])
    pygame.draw.rect(screen, black, [feed.feed_X,feed.feed_Y,10,10])
    snake.die()
    
            
    pygame.display.flip()

```
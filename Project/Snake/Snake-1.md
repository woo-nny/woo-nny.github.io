---
layout: page
title: 뱀꼬리 1일차
description: >
  뱀꼬리
comments: true
hide_description: true
---

## 뱀꼬리 1일차

### J - 키보드 입력으로 이동 하는 사각형
```python
import pygame
import time 

pygame.init() # pygame 초기화
SCREEN_WIDTH = 400 # 스크린 가로
SCREEN_HEIGHT = 300 # 스크린 세로
screen = pygame.display.set_mode((SCREEN_WIDTH,SCREEN_HEIGHT )) # 화면 크기
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
block_position = [0, 0]  # ❶ 블록의 위치 (y, x)
def draw_background(screen): #게임 배경 그린다
    background = pygame.Rect((0,0),(SCREEN_WIDTH,SCREEN_HEIGHT))
    pygame.draw.rect(screen,WHITE,background)
def draw_block(screen,color,position): #position 위치에 color 색깔의 블록 그린다
    block = pygame.Rect((position[1]*BLOCK_SIZE,position[0]*BLOCK_SIZE),(BLOCK_SIZE,BLOCK_SIZE)) # y,x좌표
    pygame.draw.rect(screen,color,block)

while not done: # 무한 반복
    clock.tick(10) # 프레임 10,30,60 적당 높을 수록 cpu 사용량 증가
    for event in pygame.event.get(): # 게임 이벤트 발생 여부 확인
        if event.type == pygame.KEYDOWN: # 키를 누르면 flag TURE
            flag =True
        elif event.type == pygame.QUIT: # 이벤트가 quit 클릭 시
            done = True # 무한반복 나감
    
    if flag == True:
        pressed = pygame.key.get_pressed() #pressed =  키
        if pressed[pygame.K_RIGHT]: # 오른쪽
            block_position[1] += 1 
            print("RIGTH")
        elif pressed[pygame.K_LEFT]: # 왼쪽
            block_position[1] -= 1   
            print("LEFT")
        elif pressed[pygame.K_UP]: # 위쪽
            block_position[0] -= 1
            print("UP")
        elif pressed[pygame.K_DOWN]: # 아래쪽
            block_position[0] += 1  
            print("DOWN")
    draw_background(screen)
    draw_block(screen, GREEN, block_position)
    pygame.display.flip()
pygame.QUIT
```

### Dragon - 마우스 입력으로 이동하는 사각형
```python
import pygame, sys
from pygame import *

pygame.init()   
size = (400,300)                 
screen = pygame.display.set_mode(size) # 화면크기 설정  
pygame.display.set_caption('Snake Game')         # 윈도우 타이틀 설정
balck = (0,0,0)
white = (255,255,255)
red = (255,0,0)
green = (0,255,0)
blue = (0,0,255)
X = 10 # 마우스 X좌표
Y = 10 # 마우스 Y좌표
height = 10
snake_height_lis = []
clock = pygame.time.Clock()
flag = False

while True:  
    clock.tick(30)
    for event in pygame.event.get():
        if event.type == pygame.QUIT: 
            pygame.quit()
            sys.exit()
        elif event.type == pygame.MOUSEBUTTONDOWN:
            height += 10
        elif event.type == pygame.MOUSEMOTION:
            X,Y = pygame.mouse.get_pos() # 마우스 움직임에 따른 X,Y좌표
            

    screen.fill(white)
    pygame.draw.rect(screen, green, [X,Y,10,height])
            
    pygame.display.flip()
```
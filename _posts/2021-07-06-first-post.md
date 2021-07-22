---
title:  "프로세스 모니터링 관련 명령어"
excerpt: "까먹었을 때 다시 보기위한 글"

categories: 
  - linux
tags:
  - [linux, command]

toc: true
toc_sticky: true
 
date: 2021-07-22
---


## ps

현재 실행되는 프로세스들의 리스트를 출력
{: .notice} 

<p align="center"><img src="https://user-images.githubusercontent.com/71758210/126618734-11c2c545-f2da-4f7f-80a1-61f017c77c9a.png"></p>
<br>
백그라운드에 실행되는 모든 프로세스 목록 : ps aux
{: .notice} 
<center><img src="https://user-images.githubusercontent.com/71758210/126618551-895a2089-0436-4cda-99b5-f1e787c56e0e.png"/></center>
<br>
apache라는 프로세스 목록만 보고 싶을 때 : ps aux | grep apache
{: .notice}
<center><img src="https://user-images.githubusercontent.com/71758210/126618949-d038048a-9dc6-4636-9d46-098ebe3cf78d.png"/></center>
<br>

PID로 특정 프로세스를 종료시킬 때: sudo kill pid번호
{: .notice}
<br>

## top

현재 실행되는 프로세스들의 리스트를 출력 2버전
{: .notice} 
sudo top을 치면 아래와 같이 프로세스 목록들이 나온다.
<center><img src="https://user-images.githubusercontent.com/71758210/126619711-53b7d77b-e763-4736-abbc-ee4194e3c4d4.png"/></center>
<br>
나갈때는 ctrl+c를 누르면 된다.


<br>

## htop

현재 실행되는 프로세스들의 리스트를 출력 3버전
{: .notice} 
<center><img src="https://user-images.githubusercontent.com/71758210/126619914-0cb0a08e-60ed-4e11-87f8-9735918fc6fe.png"/></center>
<br>

sudo htop을 쳤는데 해당 명령어를 찾을 수 없다고 하면 htop이 설치되어있지 않은 것이다.

그럴 때는, 
sudo apt-get install htop
으로 htop을 설치한다. 



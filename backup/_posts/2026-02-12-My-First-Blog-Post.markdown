---
layout: post
title: "나의 첫 블로그 포스트"
date: 2026-02-12 00:00:00 +0900
categories: 연습
---

# Priority Queue💫

## PQ(Priority Queue) Structure

-   PQ는 queue 와 달리 선입선출 구조(FIFO)이 아닌 저장할 데이터의 우선순위를 지정하여, 해당 기준으로 배출하는 개념(ADT)이다.
-   PQ를 구현 방법으로는 일반적으로 PQ는 Heap(2진트리, Indexed)의 형태로 구현되며, array나 list 형태의 자료구조를 사용해도 되기하나 Heap에 비해 삭제/삽입 수행능력이 떨어짐으로, 추천하진 않는다.
-   적용 분야 : OS의 Task 스케줄링, 네트워크 트래픽 제어 등

## Heap 구조 직접 구현한 PQ

### Heap(2진트리)

```
//추후 정리
```

### Heap(Indexed)

```
//추후 정리
```

## STL Example

### 선언

-   기본 자료형 선언 방식
 
    ```c++
    #include 
    <queue> using namespace std; bool comp(const pair<int,int>& a , const pair<int,int>& b){//사용자 정의 기준 
        if(a.first < b.first){//fist 값 기준 최대힙 
            return true;
        }

        if(a.first == b.first){
            if(a.second > b.second){//second 값기준 최소힙 
                return true;
            }
        } 
        return false;
    } //priority_queue - 기본 자료형 사용 case 
    
    priority_queue<int,vector<int>,less<int>> pq1;//최대힙 구조 // 값이 제일 큰게 제일 먼저 POP     
    priority_queue<int,vector<int>,greater<int>> pq2;//최소힙 구조 // 값이 제일 작은게 먼저 POP //사용자 정의 기준(comp)를 이용하여 저장 
    priority_queue<pair<int,int>,vector<pair<int,int>>,cmp> pq3;
    ```

-   사용자 정의 자료형 선언 방식 //20231110 pro 문제 :(
   
    ```c++
    #include <queue> using namespace std;

    struct Sample{ 
        int mx,my,mz; 
        Sample(int x,int y,int z) : mx(x),my(y),mz(z){}//구조체 생성자 
    };

    struct cmp { 
        bool operator()(const Sample& a, const Sample& b) 
        { 
            if(a.mx < b.mx){ 
                return true;
            } 
            if(a.mx == b.mx){//x값이 같을 경우 
                if(a.my > b.my){ //y값을 가지고 최소힙
                    return true; 
                } 
            }
            return false; 
        }
    }; //priority_queue -구조체 사용 case 
        
    priority_queue<Sample,vector<Sample>,cmp> pq4;
    ```

### 사용

    ```c++
        //top 데이터 반환 명령(이진 트리 구조 일 경우 : root 노드, 이진 힙 구조 일 경우 : 0번 배열)
        pq.top();

        //PQ의 데이터 삽입 명령 - 삽입 시 정렬기준에 맞게 위치 파악 후 삽입
        pq.emplace(data);//call by reference
        pq.push(data);//call by value

        //top 데이터 삭제 명령
        pq.pop();

        //PQ 데이터 empty여부 확인
        pq.empty();

        //PQ 데이터 사이즈 확인
        pq.size();
    ```
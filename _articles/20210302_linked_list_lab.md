---
id: 2
title: "Lab 1: Linked List Lab"
subtitle: "C로 Doubly Linked List 구현하기"
date: "2021.02.27"
tags: "시스템 프로그래밍, 자료구조"
---

CS230: System Programming의 첫 번째 과제는 [Linked List Lab](https://cp-git.kaist.ac.kr/cs230/cs230/-/tree/main/labs/lab1)이다. 자료구조와 알고리즘을 공부할 때 가장 기초적인 개념이며 구현은 쉬우나 포인터에 대한 이해를 필요로 한다는 점에서 수업의 프롤로그로 적합하다고 생각한다. Lab 1: Linked List Lab에서는 연결 리스트를 구현함으로써, C에 대해 친숙해지고 포인터에 대한 간단한 이해를 기대할 수 있을 것이다.

## 연결 리스트란?

연결 리스트(Linked List)는 데이터의 집합을 저장하기 위해 사용되는 데이터 구조이다.   
연결리스트는 다음의 속성을 갖는다.

- 연속되는 항목들이 포인터로 연결된다.
- 마지막 항목은 NULL을 포인트한다.
- 프로그램이 수행되는 동안 크기가 커지거나 작아질 수 있다.
- (시스템 메모리가 허용하는 한) 필요한 만큼 길어질 수 있다.
- 메모리 공간을 낭비하지 않는다(하지만 포인터를 위한 추가의 메모리를 필요로 한다).

자료구조를 공부할 때 직접적으로 코드를 구현하기 전에, 추상 데이터형(ADT, Abstract Data Type)으로 표현해보는 것이 중요하다. 자료구조의 무결성과 설계 시 치밀함을 위해서이다.

__연결 리스트의 주요 연산들__  
- 삽입: 항목을 리스트에 추가한다.
- 삭제: 지정된 위치의 항목을 리스트로부터 삭제하며 리턴한다.

__연결 리스트의 보조적 연산들__  
- 리스트 삭제: 리스트의 모든 항목을 삭제한다(리스트도 삭제).
- 개수 세기: 리스트의 항목 개수를 리턴한다.
- 리스트의 끝으로부터 n번째 항목 찾기 등

### 왜 연결 리스트를 사용하는가?: 배열 vs 연결 리스트

연결 리스트를 왜 사용하는가에 대해 알아보려면 먼저 배열과 어떤 차이점이 있는지 살펴보는 것이 유용하다.  
배열은 각 항목을 저장하는 데 메모리 블록을 할당한다. 배열의 항목은 인텍스를 첨자로 사용하여 _일정한 시간_으로 접근할 수 있다.

* 배열의 항목에 접근하는 데 왜 일정한 시간이 걸리는가?
배열의 항목에 접근하기 위해서는 항목의 주소가 배열의 기본 주소로부터의 오프셋으로 계산되고 한 번의 곱셈 연산으로 항목의 주소를 구하기 위해 기본 주소에 더해져야 할 값이 계산된다. 처음에 데이터 형에 따른 항목의 크기가 계산되고, 그것이 항목의 인덱스에 곱해져서 기본 주소에 더해질 값이 된다.  
이 과정에 한 번의 곱셈과 한 번의 덧셈이 필요하고, 두 연산이 일정한 시간을 요구하므로 배열 접근은 일정한 시간에 수행된다고 할 수 있다.

__배열의 장점__
- 간단하고 사용하기 쉽다
- 항목에의 접근이 빠르다(일정한 시간을 요구한다)
- 배열은 연속된 메모리 블록으로 정의되므로 배열의 항목들은 물리적으로 근처에 위치한다; 이는 CPU 캐싱 기법에 유리하다.

__배열의 단점__
- 고정된 크기: 배열의 크기는 정적이다.
- 한 블록의 할당: 배열 할당 시 전체 배열을 위한 메모리를 얻지 못할 때도 있다.
- 복잡한 위치 기반 삽입: 주어진 위치에 항목을 삽입하려면 기존의 항목을 이동해야 할 수도 있다.

__연결 리스트의 장점__
- 일정한 시간으로 확장이 가능하다. 또한 메모리의 복사나 재할당 없이 항목 추가가 가능하다.  
(저장 공간의 동적 할당이 가능)

__연결 리스트의 단점__
- 개별 항목에 접근하는 데 걸리는 시간이 길다. 배열의 경우 랜덤 접근이 가능하므로 O(1)의 시간이 걸리지만, 연결 리스트의 경우에는 O(n)의 시간이 걸린다.
- 데이터의 저장과 인출에 부담이 더해진다.
- 때로 연결 리스트는 변경하기가 어렵다. (마지막 항목이 삭제되면, 가장 끝에서 하나 전의 항목의 포인터가 NULL을 가리키도록 변경되어야 한다. 이 말은, 끝에서 하나 전의 항목을 찾아 그 포인터가 NULL을 가리키게 하기 위해 리스트가 탐색되어야 한다는 것이다. 이는 연결 리스트의 구현을 변경함으로써 해결할 수 있다.)
- 추가적인 참조 포인터를 위한 메모리 공간이 낭비된다.

## 이중 연결 리스트

이중 연결 리스트(Doubly Linked List)의 장점은, 리스트의 특정 노드로부터 양방향으로 탐색할 수 있다는 것이다. 단일 연결 리스트의 노드는 바로 전 노드를 가리키는 포인터를 얻기 전까지는 삭제될 수 없다. 하지만 이중 연결 리스트에서는 이전 노드의 주소를 모르더라도 노드를 삭제할 수 있다. 대신 다음과 같은 투자가 필요하다:  
- 각 노드가 포인터를 하나씩 더 필요로 하기 때문에 저장 공간이 더 필요하다.
- 삽입, 삭제 연산이 조금 더 오래 걸린다. (포인터 연산이 더 많아지므로)

### 이중 연결 리스트의 구현
```c
struct DLLNode {
  int data;
  struct DLLNode *next;
  struct DLLNode *prev;
}
```

### 이중 연결 리스트의 삽입
이중 연결 리스트에 삽입하는 경우는 세 가지가 있다.
- 새 노드를 '머리' 노드 포인터 앞에 삽입하기
- 새 노드를 '꼬리' 노드 포인터 뒤에 삽입하기
- 새 노드를 리스트 중간에 삽입하기

```c
void DLLInsert(struct DLLNode **head, int data, int position) {
  int k = 1;
  struct DLLNode *temp, *newNode;
  newNode = (struct DLLNode *) malloc(sizeof(struct DLLNode));
  if(!newNode) { //메모리 에러 확인, 할당되지 않으면 실행
    printf("Memory Error"); return;
  }
  newNode->data = data;
  if(position == 1) { // 리스트 가장 앞에 노드를 삽입
    newNode->next = *head;
    newNode->prev = NULL;
    *head->prev = newNode;
    *head = newNode;
    return;
  }
  temp = *head;
  while((k < position-1) && temp->next!=NULL) {
    temp = temp->next;
    k++;
  }
  if(temp->next == NULL) { // 리스트 가장 끝에 노드를 삽입
    newNode->next = temp->next;
    newNode->prev = temp;
    temp->next = newNode;
  }
  else {  // 리스트 중간에 노드를 삽입
    newNode->next = temp->next;
    newNode->prev = temp;
    temp->next->prev = newNode;
    temp->next = newNode;
  }
  return;
}
```
시간 복잡도: O(n). 최악의 경우에 리스트 가장 끝에 노드를 삽입해야 한다.  
공간 복잡도: O(1). 하나의 임시 변수(temp)만 생성하기 때문이다.

### 이중 연결 리스트의 노드 삭제
연결 리스트의 노드 삽입과 같이 삭제에도 세 가지 경우가 있다.

```c
void DLLDelete(struct DLLNode **head, int position) {
  struct DLLNode *temp, *temp2, temp = *head;
  int k=1;
  if(*head == NULL) {
    printf("List is empty"); return;
  }
  if(position == 1) {
    *head = *head->next;
    if(*head != NULL)
      *head->prev = NULL;
    free(temp);
    return;
  }
  while((k < position - 1) && temp->next!=NULL) {
    temp = temp->next;
    k++;
  }
  if(temp->next == NULL) {  // 리스트 맨 마지막 노드 삭제하기
    temp2 = temp->prev; //  temp2: 새로운 리스트 맨 마지막 노드
    temp2->next = NULL;
    free(temp);
  }
  else {  // 리스트 중간 노드 삭제하기
      temp2 = temp->prev;
      temp2->next = temp->next;
      temp->next->prev = temp2;
      free(temp);
  }
  return;
}

```
시간 복잡도: O(n), 크기 n인 리스트 전체를 탐색하므로
공간 복잡도: O(1), 하나의 임시 변수만을 만들기 때문에






### References

나라심하 카루만치(2014). 다양한 예제로 학습하는 데이터 구조와 알고리즘: 문제 해결법부터 개선법까. 인사이트

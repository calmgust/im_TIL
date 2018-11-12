# Data Structure



## 1. 알고리즘



#### 알고리즘이란?

* 어떠한 문제를 해결하기 위한 여러 순차적인 동작들의 모임
* 유한성을 가진다 (언젠가는 끝나야 한다)
* 의사코드 (pseudo code)로 표현되는 경우가 많다
* 특정언어에 구속되진 않는다



#### 알고리즘의 중요성

알고리즘은 프로그램의 성능에 큰 영향을 미친다

알고리즘을 설계할 때 고려해야 할 가장 중요한 두 가지 요소는 다음과 같다

1. **Time Complexity** = 알고리즘을 수행하는데 걸리는 시간
2. **Space Complexity** = 알고리즘을 수행하는 데 필요한 공간





## 2. 자료구조



#### 자료구조란?



데이터를 어떤 공간에 어떻게 저장할 것인지 설계되어 있는 것

JavaScript의 Array, Object는 대표적인 자료구조의 예



적절한 자료구조를 선택하는 것이 좋은 알고리즘을 작성하는 첫 단계





---



### Queue



![2018-10-31 11 29 11](https://user-images.githubusercontent.com/40155174/47762538-79eb4380-dd00-11e8-9281-6f48a45b185e.png)



![2018-10-31 11 29 19](https://user-images.githubusercontent.com/40155174/47762550-8374ab80-dd00-11e8-8634-7c5cfecc2dc6.png)



<u>***우선순위가 필요한 모든 곳에서 사용***</u>

ex) 종이컵, 휴지...



```javascript
init (size)
  s = new Array(size);
```



```javascript
enqueue (val)
  s[index] = val;
  index++;
```



```javascript
dequeue ()
  returnVal = s[0]
  move all elements
  return returnVal;
```





---



### Stack



![2018-10-31 11 36 22](https://user-images.githubusercontent.com/40155174/47762736-3513dc80-dd01-11e8-9df5-c7a4383f372f.png)



**Stack 사용 예**

* 전자계산기 구현
* 미로 찾기
* 자연어 처리
* 컴퓨터 메모리 관리





---



Introduction to Data Structure 2에서는

* Linked List
* Tree
* Graph
* Hash Table



----



### Linked List





**Linked List 사용 예**

* 웹사이트에서의 이동 (go back / go forward)
* 인간의 뇌 (잃어버린 기억 E를 찾는 방법: A => B => C => D => E)
* computer low level memory management



### Linked List (YL)



<u>**Arrays**</u>

* Fixed size
* Inefficient insertions and deletions
* Random access / efficient indexing
* memory waste



<u>**Linked List**</u>

* Dynamic size
* Efficient insertions and deletions
* **No** random access
* **No** waste memory



object 전체를 없애고 싶을 때 => null

object의 프로퍼티를 없애고 싶을 때 => delete



---



### Tree





**Tree 사용 예**

* 라우터 알고리즘
* Binary Space Partition
* 정렬 알고리즘 (BST)
* 계층 구조 (hierarchical or non-linear) unlike array, linked list, stack, queue





---



### Tree, BST (Binary Search Tree)



왼쪽은 작은 값 / 오른쪽은 큰 값



탐색 알고리즘이 유명

bst 안에서 찾는다



**Binary Search Tree 사용 예**

* 정렬 / 검색 알고리즘
* 데이터베이스 인덱스
* JPEG 인코더
* spreadsheet





---



### Graph



일방향 - Directed Graph

양방향 - Undirected Graph



**Graph 사용 예**

* Navigation System (Map)
* Social Networks



거리?

Weighted Edges

example: map / navigation





---



### Hash Table





* hash function을 거치면 index값이 나옴
* 예를 들어서 index = key % 10 하게 되면
* 다음에 그 키로 접근할 때 위의 식으로 바로 접근 가능



어떠한 값을 넣어도 인덱스를 준다?

output으로 input을 알아내기 어려움



* index가 겹치게 된다면?
* 이를 회피하기 위한 회피 알고리즘이 존재 (콜리션 핸들링)



*Separate chaining*

*Opening Addressing*

=> 해시가 건강하게 만들어졌다면 다음 index는 비어있을 것

=> 전체 array를 찾는 것 보다 훨씬 효율적



찾는 것은 빠르지만...

**Hash Table 단점**

* 데이터를 정렬된 순서로 retrieve하는 것에 엄청난 비용이 발생 (순서를 정렬해주지 않는다)
* O(1)이지만 hash function evaluation 이 오래 걸릴 수 있음 (찾는 것은 빠르지만 계산이 복잡해서 오래 걸릴 수 있다)
* 구현 및 사용이 어려움



**Hash Table 사용 예**

* 인증
* 검색 (주소록)
* 프로그래밍 언어 e.g. object in javascript




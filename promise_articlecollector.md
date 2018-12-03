# Promise & Article collector



Chatterbox server에서의 데이터 저장은 in-memory 영역에서만 

<u>***in-memory***: memory가 해제되면(= 프로그램이 종료되면) 데이터가 사라진다.</u>



#### 어떻게 데이터를 보존하지? => Data persistence





### Data Storage Techniques

...and how a Database can simplify your life



##### Node로 주소록 만들기

* 직접 만들어 보는 주소록 콘솔 프로그램
* 기능
  * UI
  * 저장
  * 검색
* 만들 수 있나요?
* 어떤 코어 모듈이 필요한가요?
* 저장과 검색은 어떤 식으로 해야 할까요?
* 저장은 왜 필요할까요?



*Node는 서버가 꺼지면 데이터가 소멸*

*해결책: JSON 파일로 저장* 



**저장**

=> data의 persistence(영속성)을 보장해주기 위해서

**검색**

=> memory에서 (slow file IO => 느리기 때문에)

**DS**

=> 해시테이블 (배열이 안되는 이유 => 느리기 때문에)

**UI**

=> 키보드 **입력** / 터미널 **출력**





### Data persistence







---



데이터를 파일로 저장하는 것 이외

#### 웹에서 resource를 가져오는 등의 다양한 작업들은?



***callback pattern***: JavaScript의 비동기(asynchronous) 작동 원리를 잘 표현 / callback은 코도의 가독성을 떨어뜨리는 원인





---



Promise는 비동기 함수의 표현을 보다 낫게 만들 수 있다

ES7에 추가된 async / await keyword는 비동기 과정을 마치 순차적, 동기적(synchronous)인 코드처럼 표현할 수 있다.



#### Promise / async / await
파이썬 언어의 고급 기능 및 구조 part1
================
Instruction
---------
>이 페이지에서 소개하는 파이썬의 기능 및 구조들은
>상황에 따라 유용하고 효율적인 솔루션을 제공해준다고 생각합니다.
>
>자신이 이해하기 용이하다고 생각한 순서로 목차를 구성하였습니다.
>
>이 페이지에 구성한 목차대로 한 번에 공부할 것을 추천드립니다.
목차
---
### 0. 매직 메서드
### 1. Iterator 함수 - Iterable
### 2. Generator 함수 - Yield, Xrange
### 3. FirstClass 함수
### 4. Closure 함수
### 5. Coroutine 함수
### 6. Decorator 함수
### 7. Property - Access modifier (접근제어자)
### 출처
***

# 0. 객체, 인스턴스 매직 메서드
>파이썬에서는 모든 것이 클래스이다.
>객체는 클래스(정의된 틀)로부터 생성된다.

>메서드 : 클래스 안에 정의된 함수
>매직 메서드 : 특별한 기능을 제공하는 함수

#### 객체와 인스턴스
* numerical : 1, 3.14, -30.225
* 문자형 : 'abc', "my name is obsidian"
* tuple : ('minister', 0.05)
* list : ['ice_cream', 'bbq']
* dictionary : {'account1', 4.412 }

위의 항목들을 예로 들면, 우변은 좌변의 인스턴스이다.
int는 클래스이고 무수히 많은 인스턴스를 가질 수 있다.
-5, -4, -3, -2, -1, 0, 1, 2, 3, 4, 5, 6, ..., N 중 1은 수 많은 인스턴스 중 한 예이다.
__isinstance__ 함수를 통해 확인 가능하다.    

#### 데이터 타입은 클래스의 일종
파이썬에서 데이터 타입이 클래스에 포함되는지 알고 싶다면,

>__mro(method resolution order)__함수를 통해 확인 가능하다.
>method resolution order는 함수의 결정 순서라는 뜻이다.
>mro를 사용하면,  해당 클래스의 상속 순서를 리스트로 반환한다.

'상속'은 파이썬뿐 아니라 OOP를 지원하는 언어들이 제공하는 기능들 중 하나다.
__mro()__를 사용하면 누구로부터 상속받는지 추적해 나갈 수 있다.

파이썬의 자료형에 mro를 적용하면, 마지막에 object라는 원형 자료형이 출력된다.
>__object__는 모든 자료형의 원형 자료형이다.
>모든 자료형( 내장 자료형, 사용자 정의 자료형 )은 __object__의 자식 클래스이다.
>이는 프로그래머가 명시하지 않아도 내부적으로 설정된다.

* 출처에 따르면, bool은 int의 자식 클래스라고 한다.         
                       
#### 매직 메서드
>____init____ :  대표적인 매직 메서드, 생성자
>클래스의 인스턴스(객체)가 생성될 때, 파이썬 인터프리터에 의해 자동으로 호출됨

>____call____ : 함수 호출 때 매번 사용되는 매직 메서드
>함수 호출시 함수 호출 이름 + ()를 붙이는 이유
>()는 해당 클래스에 정의된 매직 메서드 ____call____을 호출한다.

>a = "banana"
>b = "talk"
>print(a+b) -> bananatalk

문자열이 +연산으로 연결되는 경우도 매직 메서드가 적용된 경우이다.
이는 파이썬 문자열 class에 내부적으로 정의되어있다.

파이썬의 함수는 'function' 클래스의 객체이고, 아래의 코드를 예로 들면, 

			f = myFunction()
			f()
			
f 라는 변수에 myFunction이라는 function 클래스의 인스턴스를 바인딩 한다.
여기서 ____call____ 매직 메서드를 호출하는 행위를 함수 호출이라고 부른다.

**즉, 함수 호출 = 해당 함수의 ____call____ 매직 메서드를 호출하는 행위**   
   

	class Book:
		def __getattribute__(self, item):
			print(item, "객체에 접근하였습니다.")
	b1 = Book()
	b.book 
	
>book 객체에 접근하였습니다.

>. = ____getattribute____ : 객체 접근 매직 메서드

***

# 1. Iterator 함수 - Iterable
>Iterate : '반복하다, 반복 적용하다'라는 사전적 의미를 가지고 있다.
>Iterable : '반복가능한'
>Iterator : 반복 가능한 객체로 Iterable하다.
   
* Python내에서 Iterable한 객체 타입은 여러가지가 있다.
  예를 들어, list, dict, set, str, bytes, tuple, range 등이 있다. 
 
* 프로그램 로직을 작성하면서 객체 내에서 순회할 때,
위와 같은 객체 내에서 순회한 경험이 있을 것이다.

* 내장 next() 메소드로 데이터에 순차 접근 가능하다.

* 매직 메서드 or 내장함수를 통해 객체를 생성 가능하다.

		__iter__() : 매직 메서드
		__next__() : 매직 메서드
		iter() : 내장함수

* Iterable -> Iterator ? 
    No. 
	list 자료형의 경우, list는 iterable하지만, next()메소드를 적용할 수 없다.
	
	TypeError: list object is not an iterator 에러가 뜨고, 에러의 원인은 
	list가 Iterator에 포함되지 않는 자료형이기 때문이다.
	
* 그렇다면 지금까지 list나 tuple 같은 자료형에서 어떻게 for문으로 순회가 가능했는가?
* Python에서 임시로 list를 iterator로 자동 변환해주었기 때문에 가능했다.
* Iterable은 **for loop 순회** 이외에, **Iterbale 객체를 함수 인자로 받는 내부 함수**에서 쓰인다.
* zip(), map()과 같이 sequence 특징을 가지는 작업에 사용된다. 

***

# 2. Generator 함수 - Yield     
>Generator 함수는 Iterator를 생성하는 함수이다.
>일반 함수와 달리, **Yield 구문**을 가지고 있다는 것이 특징이다. 

#### 일반 함수 vs Yield 포함 함수

일반 함수 
1. 사용이 종료되면 결과값을 호출부로 반환
2. 함수를 종료시킨다.
3. 메모리에서 clear한다.

Yield 포함 함수
1. 함수 실행 중 , **yield** 구문을 읽는다.
2. 함수는 **일시 정지 상태**가 된다.
3. 반환 값을 next()를 호출한 쪽으로 전달한다.
4. 이후, 함수에서 사용되던 local변수, instruction pointer 등,
	함수 내부에서 쓰이던 데이터들이 메모리에 유지된다.


#### Generator 사용 예
>Generator를 쓰려면 **Yield를 포함**시키거나 
>간략한 Generator expression : **()**를 쓰거나			

		
>0~9 사이의 정수 중 홀수를 list object, generator object로 각각 생성한다.

>>list object로 생성할 때	
>>
>>	[ i for i in xrange(10) if i % 2 ] 
 Result : [1,3,5,7,9]
>>- 0~ 9까지 순회하며 2로 나눈 나머지가 0이면 False, 1이면True이므로,  True인 값들만 리스트에 등록된다.
>>- xrange 기능은 python2에서 제공되던 기능이다.
>>- python3부터는 range, xrange가 통합되었다.
>>- xrange와 range의 차이도 generator의 맥락에 포함된다고 생각하
>>므로 range, xrange, generator도 글의 끝에서 비교를 할 것이다.
						
>>generator object로 생성할 때	
>>    
>>     ( i for i in xrange(10) if i % 2)-> 
Result : <generator object <genexpr> at 0x000002D15E298BA0>
	
#### Generator 동작 방식
§ 여기서 generator함수는 'generator'라는 이름의 일반 함수이다.


	def generator (n):
			 i = 0
			while i < n:
				yield i
				i += 1
						
	for x in generator(5):
			print x
		
  
**결과**
						
0
1
2
3
4 
						
**동작 순서**												
1. for문이 시작된다.
						
2. generator 함수의 파라미터에 5가 전달된다.

3. generator 함수의 n에 5가 전달된 상태에서 , i  = 0이 된다.
			
4. while 문을 돌다가 yield를 만나면 generator 함수가 **일시 중지 상태**가 된다.
						
5. yield를 통해, i = 0 값을 generator함수를 호출한 구문으로 **반환**한다. 
						
6. return기능과 유사하게 반환했으나, 함수 내의 명령어 포인터, 로컬 변수 등의 데이터는 유지된다.( **함수의 내부 상태가 유지된다고 표현** )
						
7. x에 0이 저장되고 0을 출력한다.
						
8. for문에 의해 다시 generator 함수가 호출된다,
						
9. generator함수의 처음부터 시작되는 것이 아니라, 
						중단된 yield 지점부터 다시 시작된다.
						
10. i += 1 이 실행되어 i =1이 된다.
						
11. 아직 i < n 이므로 while문 내에서 yield가 실행된다.
	
12. yield로 인해 함수 실행이 일시중단되고, i = 1값을 반환한다.
	
13. x = 1이 대입되고,  1을 출력한다.
	
	...반복...
	
>yield 및 generator 함수의 핵심은 **일시중지 - 반환 - 함수 내부상태 유지**
	
#### Generator의 효용

>시스템 자원인 메모리를 점유하는 방식, 크기 면에서 
generator expression는 list comprehension과 차이점을 나타낸다.

* memory를 효율적으로 사용할 수 있다.

		import sys
		sys.getsizeof( [i for i in range(100) if i % 2] )	  #  list
		sys.getsizeof(  ( i for i in range(100) if i% 2 )  )  #  generator
list와 generator에서의 메모리 사이즈를 각각 비교해보면,
list는 사이즈가 커질 수록 메모리 사용량이 늘어난다.
반면, generator 는 항상 동일한 메모리 사이즈를 점유한다.
	
메모리 점유에 차이가 나는 이유는 작동 방식이 다르기 때문이다.
	
리스트는 list 안에 속한 모든 데이터를 적재한다.
제너레이터는 next()메소드를 통해 값에 접근할 때마다 순차적으로 메모리에 적재한다.
	
list의 값이 작은 경우에는 차이가 미미할 수 있다.
**하지만, 적당히 큰 규모의 값을 다룰 때,
 generator가 list 보다 메모리를 적게 사용한다.**
	
	
*  Lazy evaluation  : 계산 결과 값이 필요할 때까지 계산을 늦추는 효과

		def sleep_func(x):
				print("sleep")
				time.sleep(1)
				return x
	
	
		# list 버전
		list = [ sleep_func(x) for x in range(5) ]
	
		for i in list:
			print i
	
	
		# generator 버전
		gen = ( sleep_func(x) for x in range (5) )
		
		for i in gen:
			print i
**결과**
	<리스트 버전>
	sleep...
	sleep...
	sleep...
	sleep...
	sleep...
	0
	1
	2
	3
	4
		
	<제네레이터 버전>
	sleep...
	0
	sleep...
	1
	sleep...
	2
	...
	
	
**동작방식**
* list버전
1. for 문을 돌기 전에 list를 생성하는 과정에서 sleep_func()을 5번 호출한다.
2. for 문을 돌면서 만들어진 리스트, [0,1,2,3,4], 에 대해 순회하면서 출력한다.

* generator 버전
1.  generator를 생성한다.
2. for 문이 수행 될 때 하나씩 sleep_func()을 수행하며 값을 불러온다.
		
		
**수행 시간이 긴 연산을 한 번에 수행하지 않고, 필요한 순간까지 늦출 수 있다.**
	
		
#### Generator, range,  xrange(python2)

이전에 언급했던 xrange는 비록 python3 이후, 
range로 통합되었지만 동작 방식은 Generator와 비교해 볼 필요가 있다.
		

* range(start, stop, step)
		- start : list 시작
		- stop : list 끝
		- step : 증가값
		- **생성 타입 : list**
* xrange
		- **생성 타입: xrange**
	    - **수정이 불가능 함**
		- **순차적 접근**
		- **지정한 데이터 크기에 상관없이 memory 할당량이 일정하다**
* generator
		- **지정한 데이터 크기에 상관없이 memory 할당량이 일정하다**

그렇다면, generator는 쓰면서 xrange는 왜 없어졌을까?

메모리 할당량을 일정하게 배정하는 규칙은 같으나,
generator의 yield는 "함수의 상태 유지" 덕분에 비동기 기능을 가능하게 한다.
그러면서 xrange의 메모리 효율적 프로그래밍을 가능하게 하기 때문이 아닐까 싶다.
		

# 출처
* **[everything-is-class-in-python](https://gist.github.com/shoark7/fb388e6494350442a2d649a154f69a3a)**
* **[위키독스-레벨업파이썬-클래스-매직메서드](https://wikidocs.net/83755)**
* **[ㅍㅍㅋㄷ](https://bluese05.tistory.com)**


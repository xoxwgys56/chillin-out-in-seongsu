파이썬 언어의 고급 기능 및 구조 part2
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
### 5. Decorator 함수
### 6. Coroutine 함수
### 7. Property - Access modifier (접근제어자)
### 출처
***

# 3. FirstClass 함수
#### First-class citizen (일급 객체)
* OOP에서 일급 객체는 다음의 조건을 만족하는 객체를 의미한다.
1. 변수 혹은 데이터 구조를 안에 담을 수 있어야 한다.
2. 매개변수로 전달할 수 있어야 한다.
3. 리턴값으로 사용될 수 있어야 한다.

그렇다면, 파이썬의 함수는 위 조건에 해당이 될까?

해당 된다.

프로그래머는 함수를 제작할 때, 
파이썬의 def class의 인스턴스(객체)로써 선언을 한다.

파이썬 언어 특성상, 선언된 함수 또한 객체이다.

1번 조건을 검증하기 위해서는, 
임의의 변수에 모 함수의 리턴값을 담는다.
(변수가 가리키는 메모리 = 함수가 가리키는 메모리) 이면, 1번 조건이 검증된다.
변수 뿐 아니라, 리스트, 딕셔너리의 자료구조에도 할당할 수 있다.

2번 조건을 검증하기 위해서는, 
임의의 또 다른 함수의 parameter에 타겟 함수를 대입할 수 있는지를 검사한다.
이 또한, 가능하다.

3번 조건을 검증하기 위해서는, 
함수 자체를 리턴값으로 사용하거나, 함수를 함수 내에서 선언 가능해야한다.

	def get_order (order_id):
    def printer():
        print(f"This is {order_id}")
    
    return printer

	order = get_order("1129")
	order()
	
**결과**
This is 1129
***
# 4. Closure 함수
#### 클로저 함수의 정의
>외부함수의 변수를 참조할 수 있도록 어딘가에 저장하는 함수.
#### 클로저 함수의 조건
* 어떤 함수의 내부 함수일 것
* 그 내부 함수가 외부 함수의 변수를 참조할 것
* 외부 함수가 내부 함수를 리턴할 것

클로저 함수의 조건은 어렵지 않다. 대략 아래와 같은 구조에서 쓸 수 있다.

	def calculate_something(value):
			new_value = value + 100
			def print_value():
					print(new_value)
			return print_value
	
	f =	calculate_something(50)
	f()

**결과**
150
 
 print_value함수는 Closure 함수가 되기 위한 조건을 충족하고 있다.
 1. print_value함수는 calculate_something이라는 외부 함수의 내부함수이다.
 2. print_value라는 내부함수는 외부 함수의 new_value라는 변수를 참조한다.
 3. calculate_something이라는 외부함수가 내부함수 print_value를 리턴한다.

이렇게 print_value는 클로저 함수가 되었지만, 정의에 따라
외부 함수의 변수를 참조할 수 있도록 어딘가에 저장한다면,
**왜 외부 함수의 변수를 참조해야하며, 어디간에 저장해야할까?**
라는 의문이 들었다.
**왜 외부 함수의 변수가 필요할까?**

#### 클로저 함수의 효용
위 실행 과정을 하나씩 따라가보면, 클로저 함수가 필요한 시점이 발생한다.
1. calculate_something 함수가 실행되면,
2. value에 50이 대입되고 new_value는 150이 된다.
3. print_value함수가 new_value 변수 참조
4. print_value함수 리턴
[함수의 호출 과정에 따라 calculate_something 함수는 메모리에서 해제되어야 정상 ]
[내부함수인 print_value까지 해제되어야 정상]
6. f 함수가 print_value함수를 참조
7. f 변수 실행 (print_value 함수 실행)
8. f변수는 150출력

![[python_advanced_clojureF.png]]
<br>
<br>





>어떻게 6,7,8에서 new_value를 참조할 수 있을까?
*  new_value변수와 print_value 함수의 **환경**을 저장하는 **클로저**가 
**동적으로** 생성되었음.
*  f가 실행될 때, 클로저를 참조하여 값을 출력
*  f변수에 print_value 함수가 할당될 때 생성됨.

#### 클로저의 정체
* 실제 클로저가 저장되는 위치 : ____closure____[0].cell_contents
* 클로저의 자료형 : **Tuple**
* 모든 함수 객체가 가지고 있음.
* 클로저 생성 조건 미달성시 : None값
* 달성시 : 값 할당.

#### 
***
# 5. Decorator 함수
> * Decorator 함수는 꾸며주는 함수다. (Decorate  : '꾸미다')

> * 꾸미고자하는 대상 함수를 앞 혹은 뒤에 
부가적인 구문을 추가함으로써 꾸민다.

> * Decorator는 함수는 대상 함수의 앞뒤에 반복적으로 붙는 
구문들을 실행해야할 때 유용하다.

> * Decorator는 **Nested function, class 형태**로 나타낼 수 있다.

#### Decorator - Nested function version
예를 들어,다음과 같은 코드가 있다.

	import datetime
	
	def main_function_1():
	
		print datetime.datetime.now()
		print "MAIN FUNCTION 1 START"
	 	print datetime.datetime.now()

	def main_function_2():
	
		print datetime.datetime.now()
		print "MAIN FUNCTION 2 START"
		print datetime.datetime.now()

	def main_function_3():
		print datetime.datetime.now()
		print "MAIN FUNCTION 3 START"
		print datetime.datetime.now()	
		
각 함수는 function1, function2 등 1씩 증가하며 함수 
시작시간, 종료 시간을 출력한다.

	print("MAIN FUNCTION %d START", N)

부분의 앞 뒤로, 시작 시간 출력과 종료 시간 출력이 반복되는 것을 알 수 있다.

decorator를 적용하면 다음과 같이 깔끔하게 수정된다.

	import datetime
	
	def datetime_decorator(func):
		def decorated():
			print datetime.datetime.now()
			func()
			print datetime.datetime.now()
		return decorated
		
	@datetime_decorator
	def main_function_1():
		print("MAIN FUNCTION 1 START")
		
	
	@datetime_decorator
	def main_funtion_2():
		print("MAIN FUNCTION 2 START") ...
		

* 데코레이터는 함수의 앞 뒤에서 꾸며주지만, 함수의 중간에 끼어들지는 못한다.
* 데코레이터는 함수 뿐 아니라, 클래스의 형태로도 구현할 수 있다.		

데코레이터를 적용하는 방법은 다음과 같다.

1. 데코레이터를 타겟 함수에 적용하려면, 데코레이터 함수를 먼저 정의해야한다.

2. 데코레이터 함수의 인자 위치에는 타겟 함수가 들어간다.

3. 데코레이터 함수 내부에 함수를 선언하여 추가 작업을 작성한다.

4. 추가 작업이 작성된 함수를 return 해주면 된다.

2, 3, 4 번이 가능한 이유는, 파이썬의 함수는 **FirstClass함수** 이기 때문이다.


<br>
<br>

#### Decorator, class버전
class형태로 Decorator를 사용하기 위해서는 
클래스 안에 매직메서드 ____call____()를 정의해주어야한다. 

	class DatetimeDecorator : 
		def __init__(self, f):
				self.func = f
		def __call__(self, *args, **kwargs):
				print(datetime.datetime.now())
				self.func(*args, **kwargs)
				print(datetime.datetime.now())
				
	class MainClass:
		@DatetimeDecorator
		def main_function_1():
			print("Main Function 1 start")
		
		@DatetimeDecorator
		def main_function_2():
			print("Main Function 2 start")
			
		...
		
		mymain = MainClass()
		mymain.main_function_1()
		mymain.main_function_2()
Decorator를 class로 작성할 때에도 마찬가지로 
타겟 함수 위에 @로 구문을 시작하는 것은 변하지 않는다.


#### Decorator  : 타겟 함수의 위치와 파라미터
데코레이터의 Nested 함수, class버전 공통으로 주목해야할 것 이 있다.
*  **@데코레이션 함수** 가 선언되는 위치 
*  **데코레이션 함수의 파라미터**
*  **타겟함수의 위치**이다.

이 3가지 조건이 맞아떨어질 때 데코레이터 함수로 작용할 수 있다.

우선 데코레이션 함수가 선언된 본체를 보면, 인자가 존재한다.
@데코레이션 함수의 위치는 타겟 함수의 바로 앞에 위치하는데,
나는 이해를 돕기 위해, 비록 괄호는 없지만 
**@데코레이션 함수(타겟 함수)**의 형태로 이해했다.

데코레이션 함수의 파라미터로 타겟 함수가 들어간다면,
데코레이터 함수가 인스턴스화 될 때, 타겟 함수를 참조하여
매직메서드 __init__의
self.func = f(타겟함수)를 설명할 수 있고
매직메서드 __call__의
self.func(*args, **kwargs)를 설명할 수 있다.



#### 참고:  args, kwargs

*   *args, **kwargs는 포인터가 아니다.
* args는  arguments, kwargs는 keyword arguments의 줄임말이다.
 
* args는 여러 개의 인자를 함수로 받고자 할 때 쓰인다.
args의 타입은 **Tuple 형태**이기 때문이다.

* kargs 는 키워드=특정값 형태로 함수를 호출할 수 있다. {키워드,특정값}
 kargs의 타입은 **딕셔너리 형태** 이기 때문이다.
 
#### *args의 경우

	def print_order( *order_id ):
			print( type( order_id ) )
			print( order_id )
			# do some job
	
	print_order('1234')
	
**결과**
<class 'tuple'>
('1234',)

args에 대한 위의 예제 결과를 보면 확인할 수 있듯이, args의 타입은 튜플이며,
print( odre_id )를 했을 때, 튜플 형태로 출력되는 것을 알 수 있다.
튜플 자료형이므로, 복수의 값을 입력할 수 있다.
때문에,

	print_oder('1234','5678')
을 실행했을 때에는, ( '1234', '5678', ) 이라고 출력된다.
<br>

#### **kwargs의 경우

	def print_order(**kwargs):
		for key, value in kwargs.items():
			print("order_id : {0}, order_name :  {1}".format(key,value))
	
	print_order(id = 'macdonald') 

**결과**
order_id : id, order_name : macdonald
<br>

#### 함수의 변수 순서
>def print_order ( 일반 변수, *변수, **변수 )

->지키지 않을 시, syntax에러가 발생한다.
<br>
***

# 출처
* **[티베트 고원](https://blog.naver.com/PostList.naver?blogId=ikarte666)**
* **[ㅍㅍㅋㄷ](https://bluese05.tistory.com)**
* **[위키독스](https://wikidocs.net/3106)**


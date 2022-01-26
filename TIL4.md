#### PYTHON 클래스

* **Class**

  * **개념**:

    객체: 클래스에 의해 만들어진 독립된 객체

    인스턴스: 클래스 입장에서 소속된 객체

  * **기본**

    클래스 만들기: 

    ```class
    class <Class명>:
    	def <함수명>(self, <입력값1>, <입력값2>, ...):
    		실행문
    ```

    *실행문에서 입력값을 호출할 때는 self.<입력값1> 으로 해줘야 함

    *클래스 안에서 구현된 함수는 매서드(Method)라고 부름

    객체 설정: 

    ```class
    <객체명> = <Class명>()
    ```

  * **생성자(Constructor)**

    개념: 클래스 객체를 생성할 때 자동으로 호출되는 초기값

    방법: 

    ```class
    class <Class명>:
    	def __init__(self, <입력값1>, <입력값2>, ...)
    	self.<입력값1> = <입력값1>
    	self.<입력값2> = <입력값2>
    	...
    ```

    *Class명은 관례적으로 대문자로 시작한다

  * **상속**

    개념: 특정 클래스를 만들 때, 다른 클래스의 기능을 물려받는 것

    용도: 

    1. 기존 클래스를 변경하지 않고 기능을 추가하거나 

       ```class
       class <자식 Class명>(<부모 Class명>):
       	추가할 매서드
       ```

    2. 오버라이딩(Overriding): 기존 클래스 매서드를 수정할 때 *매서드 이름은 동일

       ```class
       class <상속되는 Class명>(<상속하는 Class명>):	수정할 매서드
       ```

       예시:

       1. 일반 매서드 수정

          ```overriding
          class Calc:
          	def __init__(self, first, second):
          		self.first = first
          		self.second = second
          	def div(self):
          		result = self.first/self.second
          		return result
          		
          class ChildCalc(Calc):
          	def div(self):
          		if self.second == 0:
          			return 0
          		else:
          			return self.first/self.second 
          ```

       2. 상속자 수정

          ```overriding
          class Car:
            def __init__(self, wheel, engine):
              self.wheel = wheel
              self.engine = engine
          		
          class Truck(Car):            
            def __init__(self, wheel, engine, luggage):                    
              super().__init__(wheel, engine)
              self.luggage = luggage   
          ```

          

  * **클래스 변수**

    개념: 클래스에서 선언한 변수

    방법: 

    1. 만들기

       ```클래스 변수
       class Class명:
       	Class변수 = 자료 
       ```

    2. 사용하기

       단독으로 사용

       ```Class 변수
       > Class명.Class변수
       자료
       ```

       객체 변수를 통해 사용 

       ```클래스 변수
       > a = Class명()
       > b = Class명()
       
       > print(a.Class변수)
       자료
       > print(b.Class변수)
       자료
       ```

    특징:

    1. 클래스 변수는 객체 변수에 공유됨. 따라서 `객체 변수.클래스 변수`는 모두 ID주소가 같고 클래스변수를 변경하면 함께 변경됨

       

* **Exception**

  **개념**: 예외 상황을 처리하는 방법 중 하나로, 일반적으로 error를 exception 처리해 프로그램이 멈추는 것을 막기 위해 이용

  **종류**: 시스템에서 제공하는 exception을 모아놓은 최상위 클래스 Exception에서 상속해서 사용

  1. python에서 기본적으로 제공하는 exception

  2. 사용자가 지정하는 exception

     

  * **try문**

    **개념**: 발생할 error를 exception으로 처리해 프로그램이 계속 돌아가도록 하는 것

    **방법**: 

    1. 특정 error를 exception으로 처리하는 경우

       ```try
       try: 
           명령1
       except <error명> as e:
           print(e)
       ```

       [1] 명령1을 수행하다 [2] 지명된 error가 발생하면 error를 exception 처리해 변수 e에 할당 [3] 실행을 멈추지 말고 e를 출력

    2. 모든 error를 exception으로 처리하는 경우

       ```try
       try: 
           명령1
       except Exception as e:
           print(e)
       ```

       [1] 명령1을 수행하다 [2] error가 발생하면 error를 exception 처리해 변수 e에 할당 [3] 실행을 멈추지 말고 e를 출력

    3. exception이 아닌 실행문도 함께 처리하는 경우

       ```else
       try: 
           명령1
       except Exception as e:
           print(e)
       else: 
           명령3
       ```

       [1] 명령1을 수행하다 [2] error가 발생하면 error를 exception 처리해 변수 e에 할당 [3] 실행을 멈추지 말고 e를 출력 [4] error가 발생하지 않을 경우 명령3를 수행

    4. exception 발생 여부와 상관 없이 처리하는 실행문이 필요할 경우

       ```else
       try: 
           명령1
       except Exception as e:
           print(e)
       finally: 
           명령3
       ```

       [1] 명령1을 수행하다 [2] error가 발생하면 error를 exception 처리해 변수 e에 할당 [3] 실행을 멈추지 말고 e를 출력 [4] error 발생 여부와 상관 없이 명령3를 수행

       

  * **raise**

    **개념**: exception을 강제로 발생시키기 위해 사용

    

    **방법**: exception 처리할 특정 조건을 실행하면 raise를 실행

    ```raise
    if <조건문>:
    	raise <지정한 exception>
    ```

    **예시**: 임의로 exception을 지정하기 

    ```example
    class MyError(Exception):	             
    	print('바보라고 부르지마')     #[4]            
    	     	     	     	     	             
    def say_nick(nick):
    	if nick == '바보'
    		raise MyError()         #[2]
    	else:
      	print(nick)
    	
    try: 
    	say_nick('바보')           #[1]
    except Exception as e:
    	print(e)                  #[3]
    ```

    [1] say_nick('바보')를 실행하면 [3] Exception을 할당한 변수 e를 출력하기 위해 [2] Exception을 상속한 MyError 클래스를 참고해 [4] '바보라고 부르지마!' 를 출력

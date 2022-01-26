#### PYTHON 라이브러리

* **Module**

  **개념**: 작업할 때 다양한 기능을 쓰게 되는데 하나의 작업 파일에 너무 많은 기능이 들어가면 관리 차원에서 어려움. 따라서 여러 기능을 분류해 모듈에 넣어놓고 작업 파일에서는 필요한 기능을 불러와 작업을 진행

  **참고**: 모듈 안에서는 기능을 이용하지 않기 때문에 작업 파일에서만 실행을 할 수 있도록 사용하는 명령어

  ```double underbar
  if __name__ == "__main__" : 
  	<그 모듈 내 기능>
  ```

  

  * **IMPORT**

    **개념**: 모듈에서 작업 파일로 기능을 불러오는 것

    **방법**: 다음의 명령어를 파일의 상단에 입력

    1. 모듈만 지정하는 경우 *이 경우에 작업하면서 경로를 알려줘야 함

       ```import
       import <모듈명>
       ```

    2. 모듈과 기능을 모두 지정하는 경우

       ```import
       from <모듈명> import <기능명>
       ```

    3. 모듈을 지정하고 기능을 한 번에 전부 긁어오는 경우

       ```import
       from <모듈명> import *
       ```

    

    **조건**: 다음이 모두 충족 되어야 위의 명령어만으로 import 가능

    1. 같은 가상환경에 안에서 작업이 되었다
    2. 같은 파일 트리 디렉토리에 있는가
    3. 시스템 path(OS에서 제공) 디렉토리에 있는가
    4. python path(python에서 제공) 존재하는 가 

    

    **활용**: 다음의 방법을 통해 다른 곳에 있는 모듈을 import 가능

    1. 모듈의 위치를 파악해 직접 지정

       ```import
       from <위치/경로명>.<모듈명> import <기능명>
       ```

    2. 시스템 path를 통해 강제로 모듈을 추가

       ```import
       sys.path.append(<모듈이 있는 파일 디렉토리 주소>)
       ```

    3. 환경변수를 강제로 추가

       ```import
       set PYTHONPATH = <모듈이 있는 파일 디렉토리 주소>
       ```

  

* **외부 라이브러리 활용**

  * **sys 모듈**

    **개념**: python 인터프리터가 제공하는 변수와 함수를 직접 제어할 수 있게 해줌

    | 명령어                                   | 의미                                         | 입력   |
    | ---------------------------------------- | -------------------------------------------- | ------ |
    | `import sys`                             | sys 모듈 import                              | 파일   |
    | `sys.argv[n]`                            | n번 인자: argument                           | 파일   |
    | `print(sys.argv)`                        | n번 인자 확인 *자료형: list                  | 파일   |
    | `python <작업 파일> <인자1> <인자2> ...` | 인자 list에 사용자가 임의로 설정한 인자 추가 | 터미널 |
    | `sys.exit`                               | 강제로 스크립트 종료                         | 파일   |
    | `sys.path`                               | 사용할 수 있는 모듈들의 경로  *자료형 = list | 파일   |
    | `print(sys.path[0])`                     | 현재 작업하고 있는 파일이 위치한 디렉토리    | 파일   |
    | `sys.path.append(<경로>)`                | 경로 추가                                    | 파일   |

    **예시**: 

    ``` sys
    import sys
    
    try: 
        if sys.argv[1] == 'call':
            print(sys.argv[1])
        elif sys.argv[1] == 'exit':
            sys.exit()                
        elif sys.argv[1] == 'path':
            print(sys.path)
        elif sys.argv[1] == 'append_path':
            sys.path.append(sys.argv[2])
            print(sys.path)
        else:
            print('Not Support')       
    except Exception as e:
        print(e)
    
    print('끝')
    ```

    터미널에 `python <현재 작업하는 파일명> <인자1> <인자2> ... `를 입력했을 때 출력하는 결과는 다음과 같다

    1. <인자1>가 'call' 이면 ' 프린트해라

    2. <인자1>가 'exit' 이면 프로그램을 강제로 종료해라

    3. <인자1>가 'path' 이면 현재 이 파일에서 사용 가능한 모듈들의 경로를 출력해라

    4. <인자1>가 'append_path' 이면  경로에 <인자2>를 추가해라 

    5. 그 외의 상황엔 'Not Support'를 출력해라

    6. 예외 사항은 알려라

    7. '끝'을 출력해라

       

  * **Pickle 모듈**

    **개념**: 객체의 형태를 그대로 유지하면서 파일에 저장하고 불러올 수 있게 해주는 모듈

    **방법**: 

    1. 파일 생성하기: 변수에 할당한 객체를 그대로 파일에 저장

       ```
       import pickle
       with open('pickle_test.txt', 'wb') as f:  
          data = {1: 'python', 2: 'javascript'}
          pickle.dump(data, f) 
       ```

    2. 파일 읽기: : 변수에 할당한 객체를 그대로 출력

       ```pickle
       import pickle
       with open('pickle_test.txt', 'rb') as f:
           data = pickle.load(f)                  
           print(data)
       ```

    

  * **os 모듈**

    **개념**: 환경 변수나 디렉토리, 파일 등의 os 자원을 제어할 수 있게 해주는 모듈

    **방법**: 

    | 명령어                            | 의미                                |
    | --------------------------------- | ----------------------------------- |
    | `import os`                       | os 모듈을 import                    |
    | `os.environ`                      | 시스템의 환경 변수 값을 출력        |
    | `os.environ['PATH']`              | PATH 환경 변수 내용                 |
    | `os.chdir(<경로>)`                | 현재 디렉토리 위치를 <경로>로 변경  |
    | `os.getcwd()`                     | 현재 디렉토리 위치 출력             |
    | `os.system('<시스템 명령어>')`    | 시스템 명령어 호출                  |
    | `os.popen('<시스템 명령어>')`     | 시스템 명령어의 결과값을 받기       |
    | `os.mkdir(<파일명>)`              | 디렉토리를 만든다                   |
    | `os.rmdir(<파일명>)`              | 디렉토리를 지운다                   |
    | `os.rename(<파일명1>, <파일명2>)` | <파일명1> 파일을 <파일명2>로 바꾼다 |
    | `os.unlink(<파일명>)`             | 파일을 지운다                       |

    **CF) 시스템 명령어**:

    | 명령어 | 의미                        |
    | ------ | --------------------------- |
    | `ls`   | 현재 디렉토리의 상태를 출력 |

    

  * **shutil 모듈**

    **개념**: 파일을 복사해주는 모듈

    **방법**: 

    | 명령어                                   | 의미                                       |
    | ---------------------------------------- | ------------------------------------------ |
    | `import shutil `                         | shutil 모듈을 import                       |
    | `shutil.copy("<파일명1>", "<파일명2>") ` | <파일명1>의 사본을 만들어 <파일명2>로 저장 |

  

  * **glob 모듈**

    **개념**: 디렉토리에 있는 파일들을 list로 출력

    **방법**: 

    | 명령어                | 의미                               |
    | --------------------- | ---------------------------------- |
    | `import glob`         | glob 모듈을 import                 |
    | `glob.glob("<위치>")` | <위치>에 존재하는 파일 리스트 출력 |

    

  * **tempfile 모듈**

    **개념**: 파일을 임시로 만들어서 사용할 때 이용하는 모듈

    **방법**:

    | 명령어                               | 의미                                         |
    | ------------------------------------ | -------------------------------------------- |
    | `import tempfile `                   | Temfile 모듈을 import                        |
    | `<변수> = tempfile.mkstemp() `       | 중복되지 않는 임시 파일을 만들어 변수에 할당 |
    | `<변수> = tempfile.TemporaryFile() ` |                                              |
    | `<변수>.close `                      |                                              |

    

  * **time 모듈**

    **개념**: 시간 관련된 모듈

    **방법**:

    | 명령어              | 의미                                      |
    | ------------------- | ----------------------------------------- |
    | `import time `      | time 모듈을 import                        |
    | `time.time() `      | UTC를 사용해 현재 시간을 실수 형태로 출력 |
    | `time.localtime() ` | 현재 연, 월, 일, 시, 분, 초의 형태로 출력 |
    | `time.asctime() `   | 'Sat Apr 28 20:50:20 2001'                |
    | `time.ctime() `     | 'Sat Apr 28 20:56:31 2001'                |
    | `time.strftime() `  | 형식 시정                                 |
    | `time.sleep() `     | 일정한 시간 간격을 두고 루프를 실행       |

    **time.sleep 예시**:

    ```time.sleep
    import time
    for i in range(10):
        print(i)
        time.sleep(1)
    ```

    [strftime 코드 모음](https://strftime.org/)

    

  * **calendar 모듈**

    **개념**: 파이썬에서 달력을 볼 수 있게 해주는 모듈

    **방법**:

    | 명령어                            | 의미                                      |
    | --------------------------------- | ----------------------------------------- |
    | `import calendar `                | Calendar 모듈을 import                    |
    | `calendar.prcal(<년>) `           | <년>에 해당하는 달력 출력                 |
    | `calendar.prmonth(<년>, <월>) `   | 현재 연, 월, 일, 시, 분, 초의 형태로 출력 |
    | `time.weekday(<년>, <월>, <일>) ` | 요일 정보 출력                            |
    | `time.monthrage(<년>, <월>) `     | <년>, <월>의 1일의 요일 정보와 일수 출력  |

    *요일 정보

    | 월   | 화   | 수   | 목   | 금   | 토   | 일   |
    | ---- | ---- | ---- | ---- | ---- | ---- | ---- |
    | 0    | 1    | 2    | 3    | 4    | 5    | 6    |

    

  * **random 모듈**

    **개념**: 난수(규칙이 없는 임의의 수)를 발생시키는 모듈

    **방법**:

    | 명령어                          | 의미                                   |
    | ------------------------------- | -------------------------------------- |
    | `import random `                | random 모듈을 import                   |
    | `random.random(<시작>, <끝>) `  | <시작>과 <끝> 사이의 실수 중 난수 출력 |
    | `random.randint(<시작>, <끝>) ` | <시작>과 <끝> 사이의 정수 중 난수 출력 |
    | `random_pop(<list>) `           | <list>의 요소를 무작위로 출력          |
    | `random_shuffle(<list>) `       | <list>의 요소의 순번을 무작위로 배정   |

    **random_pop 예시**: 

    ```time.sleep
    def random_pop(data):
        num = random.randint(0, len(data)-1)
        return data.pop(num)                   
    
    data = [1, 2, 3, 4, 5]
    
    while data:
    		print(data)
        print(random_pop(data))
    ```

    

  * **webbrowser 모듈**

    **개념**: 자신의 시스템에서 사용하는 기본 웹 브라우저를 자동으로 실행하는 모듈

    **방법**:

    | 명령어                         | 의미                     |
    | ------------------------------ | ------------------------ |
    | `import webbrowser `           | webbrowser 모듈을 import |
    | `webvrowser.open_new(<주소>) ` | <주소>를 연다            |

    

* * 

    

# 가비지 컬렉션 (Garbage Collection)
[BIG:C:강동욱] 중간과제

# 1. 가비지 컬렉션의 정의 및 특징
- 가비지 컬렉션(Garbage Collection, GC)은 프로그래밍 언어의 메모리 관리 방법 중 하나이다.
- 가비지 컬렉션은 동적으로 메모리를 할당받은 객체 중 더 이상 필요하지 않은 객체의 메모리를 프로그램이 주기적으로 제거해주도록 하는 역할을 한다.  
- 가비지 컬렉션을 사용하지 않는 경우에는 개발자가 명시적으로 메모리 해제를 해주어야한다. 하지만 필요없는 메모리를 해제 해주지 않으면 메모리 누수(memory leak)가 발생하고, 사용 중이던 메모리를 해제하는 경우에는 프로그램이 중단되거나 데이터가 손실될 수 있다. 따라서 C나 C++ 같은 저수준 언어와 달리 Python, Java, JavaScript, C# 등의 언어에서는 개발자가 메모리 관리에 신경쓰지 않도록 가비지 컬렉션이 사용된다.

# 2. 가비지 컬렉션 동작 메커니즘(Python) 
- Python에서 가비지 컬렉션은 레퍼런스 카운트(Reference Counting) 방식을 사용하여 메모리를 관리한다.
- Python의 객체가 참조되는 횟수인 레퍼런스 카운트는 객체가 참조될 때마다 1씩 증가하고 참조가 사라질 때마다 1씩 감소된다.
- Python의 가비지 컬렉션은 레퍼런스 카운트가 0인 객체를 실시간으로 감지하여 더 이상 사용되지 않는 것으로 간주하고 메모리에서 해제한다.
- 순환 참조가 발생하는 경우 레퍼런스 카운트 방식에서는 레퍼런스 카운트가 0이 아니기 때문에 객체가 메모리에서 해제되지 않는다.

# 3. 가비지 컬렉션 예제(Python)
1. 가비지 컬렉션이 제대로 동작되는 경우
```python
class Student:

    def __init__(self, name):
        self.name = name
        print(f"Student 객체 {self.name} 생성")

    def __del__(self):
        print(f"Student 객체 {self.name} 해제")


student = Student("강동욱")
student = Student("파이썬")

# 출력 결과
# Student 객체 강동욱 생성
# Student 객체 파이썬 생성
# Student 객체 강동욱 해제

# 설명
# student = Student("강동욱")에서 student 변수에 name이 "강동욱"인 Student 객체가 생성된다.
# student = Student("파이썬")에서 student 변수에 name이 "파이썬"인 Student 객체가 생성된다.
# name이 "강동욱"인 객체는 더 이상 참조되지 않는 상태가 되었기 때문에 가비지 컬렉션에 의해 해제되고,
# __del__ 소멸자 메서드에 의해서 "Student 객체 강동욱 해제"가 출력되는 것을 통해 가비지 컬렉션이 제대로 동작하는 것을 알 수 있다.
```
   
2. 가비지 컬렉션이 제대로 동작되지 않는 경우
```python
class Student:

    def __init__(self, name, stuNum):
        self.name = name
        self.stuNum = stuNum
        print(f"Student 객체 {self.name}, {self.stuNum} 생성")

    def __del__(self):
        print(f"Student 객체 {self.name}, {self.stuNum} 해제")


student1 = Student("강동욱", "201945092")
student2 = Student("파이썬", "123456789")
student1.stuNum = student2
student2.stuNum = student1

student1 = Student("홍길동", "456789123")

# 출력결과
# Student 객체 강동욱, 201945092 생성
# Student 객체 파이썬, 123456789 생성
# Student 객체 홍길동, 456789123 생성

# 설명
# student1 = Student("강동욱", "201945092")에서 Student 객체가 생성된다.
# student2 = Student("파이썬", "123456789")에서 Student 객체가 생성된다.
# student1.stuNum = student2, student2.stuNum = student1 에서 객체들 간에 서로 참조하는 순환 참조 형성
# student1 = Student("홍길동", "456789123")에서 Student 객체를 student1 변수에 생성 하였으나,
# name이 "강동욱"인 객체가 이미 순환 참조를 형성하였기 때문에, 가비지 컬렉션이 작동하지 않고 소멸자 또한 실행되지 않았음. 따라서 메모리 누수가 발생한다.
```

***
참고 : https://wikidocs.net/13969 (점프 투 파이썬 docs)

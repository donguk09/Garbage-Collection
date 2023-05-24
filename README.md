# 가비지 컬렉션 (Garbage Collection)
[BIG:C:강동욱] 중간과제

# 1. 가비지 컬렉션의 정의 및 특징
- 가비지 컬렉션(Garbage Collection, GC)은 프로그래밍 언어의 메모리 관리 방법 중 하나이다.
- 가비지 컬렉션은 동적으로 메모리를 할당받은 객체 중 더 이상 필요하지 않은 객체의 메모리를 프로그램이 주기적으로 제거해주도록 하는 역할을 한다.  
- 가비지 컬렉션을 사용하지 않는 경우에는 개발자가 명시적으로 메모리 해제를 해주어야한다. 하지만 필요없는 메모리를 해제 해주지 않으면 메모리 누수(memory leak)가 발생하고, 사용 중이던 메모리를 해제하는 경우에는 프로그램이 중단되거나 데이터가 손실될 수 있다. 따라서 C나 C++ 같은 저수준 언어와 달리 Python, Java, JavaScript, C# 등의 언어에서는 개발자가 메모리 관리에 신경쓰지 않도록 가비지 컬렉터가 사용된다.


# 2. 가비지 컬렉션 예제(python)
1. 가비지 컬렉션이 제대로 동작되는 경우
```python

```
   
2. 가비지 컬렉션이 제대로 동작되지 않는 경우
```python

```

***
참고 : https://wikidocs.net/13969 (점프 투 파이썬 docs)

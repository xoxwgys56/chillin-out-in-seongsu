# title

2021-06-10, [Dan](https://github.com/xoxwgys56)

> python 기초 문법에 대해 다룹니다. python3.8.5 기준

## 변수 선언

```python
name = 'Daewon'
# 파이썬은 인터프리터에 의해 동적으로 해석됩니다.
# 선언된 변수는 string type을 가집니다.

print(type(name))
# <class 'str'>
```

## 함수 선언

반복되어 사용되는 기능은 함수로 만들어 사용하는 것이 좋습니다.  
함수는 아래와 같이 선언합니다.

```python
def function(param):
    pass
```

`변수 선언`부에서 작성한 코드를 함수로 구현하겠습니다.  

```python
def print_type(bar):
    print(type(bar))

print_type('Daewon')
# <class 'str'>
print_type(123)
# <class 'int'>
```

이 곳에서는 함수 이름을 `print_type`으로 작성했습니다. 만약 `print`로 만들면 어떻게 될까요?

```python
def print(bar):
    print(type(bar))

print('Daewon')
# Traceback (most recent call last):
#   File "<stdin>", line 1, in <module>
#   File "<stdin>", line 2, in print
#   File "<stdin>", line 2, in print
#   File "<stdin>", line 2, in print
#   [Previous line repeated 996 more times]
# RecursionError: maximum recursion depth exceeded while calling a Python object
```

`print`함수가 `print`함수를 부르고 다시 `print`함수를 부릅니다. 계속해서 부르다가 `maximum`을 초과해서 불러 에러가 발생했습니다.

---

## References

- [python official tutorial](https://docs.python.org/3/tutorial/)
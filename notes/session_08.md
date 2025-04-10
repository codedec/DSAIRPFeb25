# Functions in Python

## Built-in Functins

## Custom Functions
```python
def greet():
  return "Good morning"
greet()
```

```python
def add(a,b):
  c = a+b
  return c
z = add(2,4)
print(z)
```
### Function arguments
### Default arguments
```python
def add(a,b=10):
  c = a+b
  return c

z = add(2)
print(z)
```
### kwargs

### Function return values

```python
def simple_arithmetic(a,b):
  return a+b, a-b, a*b, a/b

tsum, tdiff, tmul, tdiv = simple_arithmetic(10,5)
print(tsum, tdiff, tmul, tdiv)
```
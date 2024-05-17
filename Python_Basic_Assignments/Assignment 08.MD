1. Is the Python Standard Library included with PyInputPlus?

Ans. No, PyInputPlus is a third party module and it is not included with Python Standard Library,so you must install it separately using pip. 


```python
pip install pyinputplus
```

    Requirement already satisfied: pyinputplus in c:\users\urosh\anaconda3\lib\site-packages (0.2.12)
    Requirement already satisfied: pysimplevalidate>=0.2.7 in c:\users\urosh\anaconda3\lib\site-packages (from pyinputplus) (0.2.12)
    Requirement already satisfied: stdiomask>=0.0.3 in c:\users\urosh\anaconda3\lib\site-packages (from pyinputplus) (0.0.6)
    Note: you may need to restart the kernel to use updated packages.
    

2. Why is PyInputPlus commonly imported with import pyinputplus as pyip?

Ans. pyip is alias of PyInputPlus. Whenever we want to call PyInputPlus function we can type pyip instead of typing PyInputPlus, this optionally makes our code shorter.


```python
import pyinputplus as pyip
pyip.inputStr()
```

    Roshan
    




    'Roshan'



3. How do you distinguish between inputInt() and inputFloat()?

Ans. The inputInt() function accepts an integer value and returns integer value ,  
     The inputFloat() function accepts integer/floating point value and returns floating value.



```python
import pyinputplus as pyip
pyip.inputInt()
pyip.inputFloat()
```

    7
    7.8
    




    7.8



4. Using PyInputPlus, how do you ensure that the user enters a whole number between 0 and 99?

Ans. In input function we can set the range to min = 0 and max = 99 to ensure the user enters a whole number between 0 and 99.


```python
pyip.inputInt(min = 0,max = 99)
```

    88
    




    88



5. What is transferred to the keyword arguments allowRegexes and blockRegexes?

Ans. We can also use regular expression to specify whether an input is allowed or not. The allowRegexes and BlockRegexes keyword arguments take a list of regular expression strings to determine what the pyinnputplus function will accept or reject.


```python
response = pyip.inputNum(allowRegexes = [r'(I|V|X|L|C|D|M)+',r'zero']) # it allows roman letters as numbers 
```

    X
    


```python
response = pyip.inputNum(blockRegexes = [r'[02468]$'])# it blocks even numbers
```

    2
    This response is invalid.
    3
    

6. If a blank input is entered three times, what does inputStr(limit=3) do?

Ans. If a blank input is entered three times, it will throw RetryLimitExecption.


```python
response = pyip.inputStr(limit = 3)
```

    
    Blank values are not allowed.
    
    Blank values are not allowed.
    
    Blank values are not allowed.
    


    ---------------------------------------------------------------------------

    ValidationException                       Traceback (most recent call last)

    ~\anaconda3\lib\site-packages\pyinputplus\__init__.py in _genericInput(prompt, default, timeout, limit, applyFunc, validationFunc, postValidateApplyFunc, passwordMask)
        166         try:
    --> 167             possibleNewUserInput = validationFunc(
        168                 userInput
    

    ~\anaconda3\lib\site-packages\pyinputplus\__init__.py in <lambda>(value)
        242 
    --> 243     validationFunc = lambda value: pysv._prevalidationCheck(
        244         value, blank=blank, strip=strip, allowRegexes=allowRegexes, blockRegexes=blockRegexes, excMsg=None,
    

    ~\anaconda3\lib\site-packages\pysimplevalidate\__init__.py in _prevalidationCheck(value, blank, strip, allowRegexes, blockRegexes, excMsg)
        249         # value is blank but blanks aren't allowed.
    --> 250         _raiseValidationException(_("Blank values are not allowed."), excMsg)
        251     elif blank and value == "":
    

    ~\anaconda3\lib\site-packages\pysimplevalidate\__init__.py in _raiseValidationException(standardExcMsg, customExcMsg)
        221     if customExcMsg is None:
    --> 222         raise ValidationException(str(standardExcMsg))
        223     else:
    

    ValidationException: Blank values are not allowed.

    
    During handling of the above exception, another exception occurred:
    

    RetryLimitException                       Traceback (most recent call last)

    ~\AppData\Local\Temp\ipykernel_3572\3533114902.py in <module>
    ----> 1 response = pyip.inputStr(limit = 3)
    

    ~\anaconda3\lib\site-packages\pyinputplus\__init__.py in inputStr(prompt, default, blank, timeout, limit, strip, allowRegexes, blockRegexes, applyFunc, postValidateApplyFunc)
        245     )[1]
        246 
    --> 247     return _genericInput(
        248         prompt=prompt,
        249         default=default,
    

    ~\anaconda3\lib\site-packages\pyinputplus\__init__.py in _genericInput(prompt, default, timeout, limit, applyFunc, validationFunc, postValidateApplyFunc, passwordMask)
        186                 else:
        187                     # If there is no default, then raise the timeout/limit exception.
    --> 188                     raise limitOrTimeoutException
        189             else:
        190                 # If there was no timeout/limit exceeded, let the user enter input again.
    

    RetryLimitException: 


7. If blank input is entered three times, what does inputStr(limit=3, default='hello') do?

Ans. When we use limit keyword argument and also pass default keyword argument then the function returns default value instead of raising an exception.


```python
response = pyip.inputStr(limit = 3, default = "hello")
response
```

    
    Blank values are not allowed.
    
    Blank values are not allowed.
    
    Blank values are not allowed.
    




    'hello'




```python

```

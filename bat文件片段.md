```
@echo off
setlocal ENABLEDELAYEDEXPANSION
for /l %%i in (0,1,7) do (
	set ss=ip%%i.txt
	pocsuite -r poc.py -f !ss! -v 2 > res%%i.txt
	@echo !ss!
)
```


```
@echo off
setlocal enabledelayedexpansion
for /l %%i in ( 39, -1 ,10 ) do (
	set /a n=%%i-10
    	echo !n!
)
```

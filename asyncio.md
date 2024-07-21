[[python]] [[библиотеки]]

1) Выполнение кода, пока другие операции работают в фоне
```python
import asyncio 
from util import delay 

async def hello_every_second(): 
	for i in range(2):
		await asyncio.sleep(1) 
	print("пока я жду, исполняется другой код!") 
	
async def main():
	first_delay = asyncio.create_task(delay(3))
	second_delay = asyncio.create_task(delay(3)) 
	
	await hello_every_second() 
	await first_delay 
	await second_delay
```
```
засыпаю на 3 с
засыпаю на 3 с
пока я жду, исполняется другой код!
пока я жду, исполняется другой код!
сон в течение 3 с закончился
сон в течение 3 с закончился
```

2) Снятие задачи
```python
import asyncio
from asyncio import CancelledError 
from util import delay

async def main():
	long_task= asyncio.create_task(delay(10))
	
	seconds_elapsed = 0
	while not long_task.done():
		print('Задача не закончилась, следующая проверка через секунду.') 
		await asyncio.sleep(1)
		
		seconds_elapsed = seconds_elapsed + 1 
		if seconds_elapsed == 5:
			long_task.cancel()
		
		try:
			await long_task
		except CancelledError:
			print('Наша задача была снята')
	
asyncio.run(main())
```

3) Задание тайм-аута для задачи с помощью wait_for

```python
import asyncio
from util import delay 

async def main(): 
	delay_task = asyncio.create_task(delay(2))
	try:
		result = await asyncio.wait_for(delay_task, timeout=1)
		print(result)
	except asyncio.exceptions.TimeoutError:
		print('Тайм-аут!')
		print(f'Задача была снята? {delay_task.cancelled()}')

asyncio.run(main())
```
```
засыпаю на 2 с
Тайм-аут!
Задача была снята? True
```

4) 

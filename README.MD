Этот темплейт используется для разработки Telegram ботів с использованием библиотеки [`aiogram v3.0+`](https://github.com/aiogram/aiogram/tree/dev-3.x).

### Для того, чтобы начать использовать:
1. Скопируйте `.env.dist` в `.env` и заполните необходимые данные.
2. Создайте новые хендлеры.
3. **Docker:**
   1. Вы можете сразу запустить проект с Docker, а если у вас его нет, то [загрузите и установите](https://docs.docker.com/get-docker/).
   2. Запустите проект из команды `docker-compose up`
4. **Без Docker:**
   1. Создайте [venv](https://docs.python.org/3/library/venv.html)
   2. Установите зависимости из requirements.txt: `pip install -r requirements.txt`
   3. Запустите проект из команды `python3 bot.py`


### Як робити та реєструвати хендлери:
Створюєте модуль `you_name.py` у папці `handlers`.

Створюєте роутер у `you_name.py`.
```python
from aiogram import Router
user_router = Router()
```
Можна робити декілька роутерів в одному модулі, та на кожний з них навішувати хендлери.
Можна реєструвати хендлери декораторами:
```python
@user_router.message(commands=["start"])
async def user_start(message):
    await message.reply("Вітаю, звичайний користувач!")
```

Заходимо у файл `bot.py` і додаємо всі роутери в нього:
```python
from tgbot.handlers.admin import admin_router
from tgbot.handlers.echo import echo_router
from tgbot.handlers.user import user_router

...

async def main():
   
   ...

    for router in [
        admin_router,
        user_router,
        ...,
        echo_router,

    ]:
        dp.include_router(router)
```

### Туторіали з aiogram v3
Відосів поки що немає, але @Groosha вже почав робити [свій підручник](https://groosha.2038.io/telegram-tutorial-2/).

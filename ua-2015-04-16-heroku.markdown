---
layout: default
title: Розгортання Rails Girls на Heroku
permalink: heroku
---

# Розгортання проекту на Heroku

*Created by Terence Lee, [@hone02](https://twitter.com/hone02)*

### Встановлення інструментів Heroku та налаштування доступу

Для початку необхідно встановити [Heroku Toolbelt](https://devcenter.heroku.com/articles/getting-started-with-ruby#set-up) та [зареєструватись](https://signup.heroku.com/dc) на сервісі Heroku.
Далі у командному рядку слід виконати наступну команду, у відповідь на запрошення ввести ім'я новоствореного користувача та пароль:

~~~
heroku login
~~~

__ТРЕНЕР__: Розповісти про переваги використання Heroku на противагу традиційним сервісам.

### Підготуємо проект

#### Система контролю версій (VCS - Version Control System)

Зараз нам потрібно додати проект у систему контролю версій. Для цього слід виконати в командному рядку наступну послідовність команд:

~~~
git init
echo "public/uploads" >> .gitignore
echo "tmp" >> .gitignore
echo "logs" >> .gitignore
git add .
git commit -m "initial commit"
~~~

__ТРЕНЕР__: Зараз є хороша можливсть поговорити про системи контролю версій та, зокрема, git. Також варто пояснити про файл `.gitignore` та його вміст, а також чому не потрібно завантажувати деякі файли в репозиторій.

#### Зміна конфігурації бази даних

Перш за все, нам потрібно, щоб на Heroku працювала база даних. Heroku та твоє локальне середовище використовують зовсім різні бази даних (локально - SQLite; на Heroku - PostgreSQL), тому потрібно внести певні зміни у файл Gemfile. Необхідно замінити цей рядок

~~~
gem 'sqlite3'
~~~

на наступний фрагмент:

~~~
group :development do
  gem 'sqlite3'
end
group :production do
  gem 'pg'
end
~~~

Далі слід виконати команду `bundle install --without production`, щоб завантажити та встановити необхідні бібліотеки.

__ТРЕНЕР__: Тут можна поговорити про різні реляційні бази даних, а також розповісти про особливу роль БД PostgreSQL у середовищі Heroku.


#### Додаємо rails_12factor

Далі нам потрібно додати бібліотеку `rails_12factor` до Gemfile, щоб мати змогу розгорнути проект на Heroku.

Цей gem змінює конфігурацію Rails проекту для сумісності з Heroku. Наприклад, змінюється спосіб ведення лог-файлів та конфігурація статичних ресурсів (малюнки, CSS стилі, скрипти JavaScript) - так, щоб враховувались особливості середовища Heroku.

Будь ласка, заміни цей фрагмент

~~~
group :production do
  gem 'pg'
end
~~~

на наступний:

~~~
group :production do
  gem 'pg'
  gem 'rails_12factor'
end
~~~

Після цього виконай команду `bundle install` та додай змінені файли в репозиторій:

~~~
git commit -a -m "Added rails_12factor gem"
~~~

__ТРЕНЕР__: Можна поговорити про логування та інші особливості роботи з Heroku.


### Розгортання проекту

#### Створення нового додатка на Heroku

Для створення нового Heroku додатка потрібно виконати в терміналі команду `heroku create`. В результаті вийде щось типу цього:

~~~
Creating sheltered-refuge-6377... done, stack is cedar
http://sheltered-refuge-6377.herokuapp.com/ | git@heroku.com:sheltered-refuge-6377.git
Git remote heroku added
~~~

Тут "sheltered-refuge-6377" - автоматично згенерована назва Heroku додатка. Можна вказати і свою назву, але вона має бути унікальною (скоріше за все, назви "railsgirls" та "helloworld" вже хтось використав до тебе, тому доведеться придумати щось оригінальніше).

#### Публікуємо код

Тепер потрібно завантажити готовий код проекту у репозиторій Heroku (все решта буде зроблено автоматично). Для цього треба виконати в терміналі команду `git push heroku master`; результат буде виглядати приблизно так:

~~~
Initializing repository, done.
Counting objects: 101, done.
Delta compression using up to 2 threads.
Compressing objects: 100% (91/91), done.
Writing objects: 100% (101/101), 22.68 KiB | 0 bytes/s, done.
Total 101 (delta 6), reused 0 (delta 0)

-----> Ruby app detected
-----> Compiling Ruby/Rails
-----> Using Ruby version: ruby-2.0.0
-----> Installing dependencies using 1.6.3
       Running: bundle install --without development:test --path vendor/bundle --binstubs vendor/bundle/bin -j4 --deployment
       Fetching gem metadata from https://rubygems.org/..........
...
-----> Launching... done, v1
       http://sheltered-refuge-6377.herokuapp.com/ deployed to Heroku
~~~

Коли з'явиться рядок "Launching... done", це означає, що твій додаток опублікований. Ура!

#### Міграція бази даних

Далі слід мігрувати базу даних - щось подібне ти вже робила на локальному середовищі. Зараз ця команда виглядатиме так: `heroku run rake db:migrate`.

### Затамувавши подих, запускаємо!

Тепер можна спробувати зайти на адресу програми і подивитись результат у браузері. Адреса (URL) буде виглядати якось так: <http://sheltered-refuge-6377.herokuapp.com/> (звісно, замість ідентифікатора 'sheltered-refuge-6377' буде щось інше). Ще один цікавий спосіб - виконати в терміналі команду `heroku open`, і браузер сам відкриється на потрібній сторінці.


# Використання Gravatar

*Created by Catherine Jones*

**Цей туторіал передбачає, що у вас уже створений додаток Ideas та додана аутентифікація користувачів.**

### Важливо!

Необхідно мати e-mail адресу зареєстровану на Gravatar. Якщо у вас немає її перейдіть на [gravatar.com](http://en.gravatar.com/) і зареєструйтеся.

## *1.* Додамо Gravtastic gem

Відкриваємо gemfile та під `devise` gem додамо
~~~
gem 'gravtastic'
~~~
у терміналі виконуємо:
~~~
bundle install
~~~
Ми встановили gravtastic gem. Не забудь перезапустити rails сервер.

## *2.* Установка Gravatar 

Відкриваємо `app/models/user.rb`, і додаємо
~~~
include Gravtastic
gravtastic
~~~
одразу ж після першого рядка.

## *3.* Налаштування Gravatar

Відкриємо `app/views/layouts/application.html.erb` і у
~~~
<% if user_signed_in? %>
~~~
секції, але перед  
~~~
<% else %>
~~~
додамо
~~~
<%= image_tag current_user.gravatar_url %>
~~~
Тепер відкрий у браузері додаток і ввійди у свій профайл використовуючи той e-mail, який пов'язаний із Gravatar. Ти маєш побачити свій Gravatar.

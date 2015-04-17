
# Додаємо можливість реєстрації користувачів

*Created by Piotr Steininger, [@polishprince](https://twitter.com/polishprince)*

*Updated by Ernesto Jimenez, [@ernesto_jimenez](https://twitter.com/ernesto_jimenez)*

**Цей крок передбачає, що у вас уже є створений додаток Ideas.**

## *1.* Додаємо devise gem

Відкриємо `Gemfile` і додамо ці рядки
~~~
gem 'devise'
~~~
у консолі запустимо
~~~
bundle install
~~~
щоб встановити gem. **Не забудь перезапустити Rails сервер**.

## *2.* Встановлення пристрою у додатку

Запустимо у терміналі: 
~~~
rails g devise:install
~~~

## *3.* Налаштування пристрою

Перевіримо, чи у нас описані url опції за замовчуванням. Відкриємо `config/environments/development.rb` та додамо:
~~~
   config.action_mailer.default_url_options = { :host => 'localhost:3000' }
~~~
перед словом `end`.

Відкриємо `app/views/layouts/application.html.erb` і додамо:
~~~
<% if notice %>
  <p class="alert alert-success"><%= notice %></p>
<% end %>
<% if alert %>
  <p class="alert alert-danger"><%= alert %></p>
<% end %>
~~~
над рядками
~~~
   <%= yield %>
~~~
Відкриємо `app/views/ideas/show.html.erb` і видаляємо рядок:
~~~
<p id="notice"><%= notice %></p>
~~~
робимо те саме у файлі `app/views/comments/show.html.erb`. 

## *4.*Встановлюємо модель користувача 

Ми використаємо bundled generator script для того, щоб створити модел користувача.
~~~
   rails g devise user
   rake db:migrate
~~~
**Тренер:**Пояснити що ми створили. 

## *5.* Ствоюємо першого користувача

Тепер коли у нас усе встановлено, ми можемо створити першого користувача. Now that you have set everything up you can create your first user. Пристрій автоматично створює всі роути, щоб створити новий аккаунт, ввійти чи вийти з додатку. 

Переконаємося, що rails сервер увімкнений, відкрий [http://localhost:3000/users/sign_up](http://localhost:3000/users/sign_up) та створи новий профайл користувача.

## *6.*Додамо посилання для авторизації та реєстрації

Все, що нам залишилось зробити, це додати відповідні посилання або повідомення у верхньому правому кутку про те,що користувач увійшов у свій профайл.

Змінимо файл `app/views/layouts/application.html.erb` додаємо:
~~~
<p class="navbar-text pull-right">
<% if user_signed_in? %>
  Logged in as <strong><%= current_user.email %></strong>.
  <%= link_to 'Edit profile', edit_user_registration_path, :class => 'navbar-link' %> |
  <%= link_to "Logout", destroy_user_session_path, method: :delete, :class => 'navbar-link'  %>
<% else %>
  <%= link_to "Sign up", new_user_registration_path, :class => 'navbar-link'  %> |
  <%= link_to "Login", new_user_session_path, :class => 'navbar-link'  %>
<% end %>
~~~
прямо над рядками
~~~
<ul class="nav">
  <li class="active"><a href="/ideas">Ideas</a></li>
</ul>
~~~
Також потрібно, щоб користувач переходив на сторінку авторизації, якщо він ще не увійшов у свій профайл. Для цього відкриваємо  `app/controllers/application_controller.rb` і додаємо:
~~~
  before_action :authenticate_user!
~~~
після `protect_from_forgery with: :exception`.

Відкрий браузер та спробуй увійти і вийти із профайлу.

**Тренер:** Розкажи про `user_signed_in?` та `current_user`. Чим вони корисні?

## Що далі?

* Додамо додаткові поля до моделі користувача 
* Додамо зв'язки між користувачами та ідеями 
* Встановимо обмеження для користувачів 



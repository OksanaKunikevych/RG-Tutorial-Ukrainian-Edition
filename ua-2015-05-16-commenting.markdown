---
layout: default
title: Функціональність роботи з коментарями для додатку Rails Girls
permalink: commenting
---
# Додаємо коментування
*Created by Janika Liiv, [@janikaliiv](https://twitter.com/janikaliiv)*

Зараз ми реалізуємо можливість додавання коментарів до ідей у твоїй першій програмі.

Всі інструкції з початкового налаштування середовища Rails та побудови основної функціональності програми можна знайти [тут](/app).

## 1. Створюємо scaffold для коментарів

Потрібно створити scaffold для сутності 'коментар', що містить: ім'я коментатора, власне коментар (текст), ну і посилання на ідею, якої стосується даний коментар.

~~~
rails g scaffold comment user_name:string body:text idea_id:integer
~~~

This will create a migration file that lets your database know about the new comments table. Run the migrations using
Ця команда створить, зокрема, сценарій *міграції*, що "повідомить" базу даних про те, що створюється нова таблиця з коментарями. Цю міграцію треба виконати, запустивши в терміналі команду

~~~
rake db:migrate
~~~

## 2. Додаємо зв'язки між моделями

Ще треба зробити так, щоб Rails програма знала про зв'язки між моделями (ідеї та коментарі).
До однієї ідеї можна створити декілька коментарів, отже, в даному випадку буде співвідношення один-до-багатьох (одна ідея - багато коментарів).

Відкрий файл `app/models/idea.rb` та одразу після рядка

~~~
class Idea < ActiveRecord::Base
~~~

додай

~~~
has_many :comments
~~~

Моделі 'коментар' також потрібно вказати, що вона належить до 'ідеї' (звісно, що так - коментар не може існувати сам по собі). Отже, відкрий файл `app/models/comment.rb` та після рядка

~~~
class Comment < ActiveRecord::Base
~~~

додай

~~~
belongs_to :idea
~~~

## 3. Малюємо форму для додавання нового коментаря та показуємо коментарі до ідей

Відкрий файл app/views/ideas/show.html.erb та після `image_tag`

~~~
<%= image_tag(@idea.picture_url, :width => 600) if @idea.picture.present? %>
~~~

додай

~~~
<h3>Comments</h3>
<% @comments.each do |comment| %>
  <div>
    <strong><%= comment.user_name %></strong>
    <br />
    <p><%= comment.body %></p>
    <p><%= link_to 'Delete', comment_path(comment), method: :delete, data: { confirm: 'Are you sure?' } %></p>
  </div>
<% end %>
<%= render 'comments/form' %>
~~~

У контролері `app/controllers/ideas_controller.rb` до екшена 'show' після рядка

~~~
@idea = Idea.find(params[:id])
~~~

додай цей фрагмент коду:

~~~
@comments = @idea.comments.all
@comment = @idea.comments.build
~~~

Також відкрий файл `app/views/comments/_form.html.erb` та після

~~~
  <div class="field">
    <%= f.label :body %><br />
    <%= f.text_area :body %>
  </div>
~~~

додай рядок

~~~
<%= f.hidden_field :idea_id %>
~~~

і ще видали кілька зайвих рядків:

~~~
<div class="field">
  <%= f.label :idea_id %><br>
  <%= f.number_field :idea_id %>
</div>
~~~

Це все. Тепер поряд з самою ідеєю можна побачити коментарі до неї, а також форму для створення нових коментарів та видалення існуючих.
Вітаю, ще один важливий крок зроблено!

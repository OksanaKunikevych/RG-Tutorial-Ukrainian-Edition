
# Додамо дизайну за допомогою HTML & CSS

*Created by Alex Liao, [@alexliao](http://bannka.com/alex)*

Тепер наш додаток уже працює, але все ще виглядає не дуже красиво. Давай додамо трохи дизайну, щоб він виглядав як професійний вебсайт. Маленький спойлер: вкінці наш додаток має виглядати приблизно ось [так](http://railsgirlsapp.herokuapp.com/ideas).

## *1.*Змінюємо вигляд додатка

Відкриємо `app/assets/stylesheets/application.css`, замінимо рядок
~~~
{% highlight html %}
body { padding-top: 100px; }
{% endhighlight %}
~~~
на рядок
~~~
{% highlight html %}
body { padding-top: 60px; }
{% endhighlight %}
~~~
Також, видалимо файл `app/assets/stylesheets/scaffolds.css.scss` тому, що нам не потрібно стилю за замовчуванням,який генерує Rails.

Тепер онови сторінку [http://localhost:3000/ideas](http://localhost:3000/ideas). Поки великих змін ти ще не побачиш, але це підготовка для наступних кроків.

## *2.*Налаштовуємо навігацію по сайту

Будемо вважати, що "idea" - це найважливіший об'єкт на сайті, тому потрібно створити кнопку "New Idea" на панелі навігації. 

Відкриваємо `app/views/layouts/application.html.erb`, під рядками
~~~~
{% highlight erb %}
<li class="active"><a href="/ideas">Ideas</a></li>
{% endhighlight %}
~~~
додаємо
~~~
{% highlight erb %}
<li ><%= link_to 'New Idea', new_idea_path %></li>
{% endhighlight %}
~~~
## *3.*Дизайн списку ідей

Давай зробимо так, щоб наш список виглядав красиво. Для цього нам потрібно замінити табличний макет сторінки на div макет. 

**Тренер:** Трішки інформації про table vs div.

Відкриємо `app/views/ideas/index.html.erb` у текстовому редакторі та замінимо всі рядки на: 
~~~
{% highlight erb %}
<h1>Listing ideas</h1>

<% @ideas.in_groups_of(3) do |group| %>
  <div class="row">
    <% group.compact.each do |idea| %>
      <div class="col-md-4">
        <%= image_tag idea.picture_url, width: '100%' if idea.picture.present?%>
        <h4><%= link_to idea.name, idea %></h4>
        <%= idea.description %>
      </div>
    <% end %>
  </div>
<% end %>
{% endhighlight %}
~~~
**Тренер:** Пояснити що означає новий код вище і розказати трохи про Bootstrap 12 grids layout. 

Оновлюємо сторінку! Гарно, правда ж? Тепер створимо трохи більше контенту на нашій сторінці. Натисни на кнопку "New Idea" і створи більше ідей з красивими картинками і описом. У сучасному веб-дизайні є такий принцип: контент - це найкраща прикраса веб-додатку. 
## *4.*Дизайн сторінки опису ідей 
Натиснемо на заголовок ідеї та перейдемо на нову сторінку з описом ідеї. Поки це досі scaffold з дизайном, який генерується автоматично Rails. Давай зробимо його гарнішим. 

Відкриваємо `app/views/ideas/show.html.erb` у текстовому редакторі та заміняємо всі рядки на:
~~~
{% highlight erb %}
<p id="notice"><%= notice %></p>

<div class="row">
  <div class="col-md-9">
    <%= image_tag(@idea.picture_url, width: '100%') if @idea.picture.present? %>
  </div>

  <div class="col-md-3">
    <p><b>Name: </b><%= @idea.name %></p>
    <p><b>Description: </b><%= @idea.description %></p>
    <p>
      <%= link_to 'Edit', edit_idea_path(@idea) %> |
      <%= link_to 'Destroy', @idea, data: { confirm: 'Are you sure?' }, method: :delete %> |
      <%= link_to 'Back', ideas_path %>
    </p>
  </div>
</div>
{% endhighlight %}
~~~

**Тренер:** Пояснення, що означає код вище.

## Що далі?

* Використаймо щойно набуті навики та змінимо дизайн для форми додавання нової ідеї.
* Додамо або змінимо дизайн додатка за нашим бажанням. Add more design to the pages as you wish
* Перейдемо до інших туторіалів, щоб дізнатись більше про Rails


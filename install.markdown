
# Установка необхідних програм для Rails Girls

Для створення додатків на Ruby On Rails необхідно встановити деякі програми на твій комп'ютер.

Обери інструкцію, що підходить для твоєї операційної системи. Не панікуй, якщо виникнуть якісь проблеми: повідом нам, і ми вирішимо їх разом.

* [Setup for OS X](#setup-for-os-x)
* [Setup for Windows](#setup-for-windows)
* [Setup for Linux](#setup-for-linux)
* [Alternative Installment for all OS](#virtual-machine)


<hr />

## Setup for OS X


### *1.* Якщо у тебе OS X версії 10.6, 10.7, or 10.8:
Завантаж RailsInstaller для своєї версії OS X:

* [RailsInstaller for 10.7 and 10.8](http://railsinstaller.s3.amazonaws.com/RailsInstaller-1.0.4-osx-10.7.app.tgz) <span class="muted">(325MB)</span>
* [RailsInstaller for 10.6](http://railsinstaller.s3.amazonaws.com/RailsInstaller-1.0.4-osx-10.6.app.tgz) <span class="muted">(224MB)</span>

Двічі натисни на завантажений файл і він установиться у поточну папку. Відкрий розархівований файл `RailsInstaller-1.0.4-osx-10.7.app` або `RailsInstaller-1.0.4-osx-10.6.app` і слідуй інструкції установки. Відкриється нове вікно з README файлом з 'Rails Installer OS X'. Будь ласка, **не виконуй** інструкції у цьому файлі.

Якщо версія Rails не була найновішою, ти можеш просто оновити її набравши у терміналі:

~~~
gem update rails --no-ri --no-rdoc
~~~

Для того, щоб переконатись, що все працює запустимо команду сторення додатка

~~~
rails new railsgirls
~~~

### *2.* Встановимо текстовий редактор

Для воркшопу ми рекомендуємо тестовий редактор Atom.

* [Завантажити та встановити Atom](https://atom.io/)

Якщо ти використовуєш Mac OS X 10.7 чи старішу версію, ти можеш використати інший текстовий редактор [Sublime Text 2](http://www.sublimetext.com/2).

### *3.* Оновлення браузера

Відкрий [whatbrowser.org](http://whatbrowser.org) та онови свій браузер, якщо у тебе не остання версія. 


Це все! Тепер у тебе все необхідне для створення свого першого додатку на Ruby on Rails:)

<hr />

## Setup for Windows

### *1.* Встановлюємо Rails

Завантаж [RailsInstaller](https://s3.amazonaws.com/railsinstaller/Windows/railsinstaller-3.1.0.exe) і запусти його. Слідуй інструкціям та встанови RailsInstaller.

Відкрий `Command Prompt with Ruby on Rails` і набери:

~~~
rails -v
~~~

Якщо версія Rails менша ніж 4, онови Rails за допомогою команди:

~~~
gem update rails --no-ri --no-rdoc
~~~

Для того, щоб переконатись, що все працює запустимо команду

~~~
rails new railsgirls
cd railsgirls
rails server
~~~

## Можливі помилки

### Gem::RemoteFetcher error

Якщо при запуску `rails new railsgirls` чи `gem update rails` виникає ця помилка:

~~~
Gem::RemoteFetcher::FetchError: SSL_connect returned=1 errno=0 state=SSLv3 read
server certificate B: certificate verify failed (https://rubygems.org/gems/i18n-
0.6.11.gem)
~~~

Це означає, що у тебе старіша версія Rubygems і необхідно вручну оновити її вказуючи версію Rubygems

~~~
gem -v
~~~

Якщо версія нижча ніж `2.2.3` необхідно оновити її вручну:


Спочатку завантажимо [ruby-gems-update gem](https://github.com/rubygems/rubygems/releases/download/v2.2.3/rubygems-update-2.2.3.gem). Перемісти файл у `c:\\rubygems-update-2.2.3.gem` і запусти його:

~~~
gem install --local c:\\rubygems-update-2.2.3.gem
update_rubygems --no-ri --no-rdoc
gem uninstall rubygems-update -x
~~~

Перевіримо версію rubygems

~~~
gem -v
~~~

Перконайся, що вона вища ніж `2.2.3`. Ще раз запусти команду, яка до того видавала помилку.


### 'x64_mingw' is not a valid platform` Error

Інколи при запуску `rails server` виникає помилка:
`'x64_mingw' is not a valid platform` 

Тоді необхідно трохи відредагувати `Gemfile`:

Подивись в кінець файлу. Ти побачиш схожі рядки:
`gem 'tzinfo-data', platforms: [:mingw, :mswin, :x64_mingw]`. Якщо у тебе є рядок з `:x64_mingw`,тоді видали `:x64_mingw`  Вкінці повиннен бути лише рядок:
`'tzinfo-data', platforms: [:mingw, :mswin]`

Після змін введи в командному рядку `bundle update`.

### *2.* Встановлюємо текстовий редактор

Для цього воркшопу ми рекомендуємо текстовий редактор Atom.

* [Download Atom and install it](https://github.com/atom/atom/releases/latest)
  * Завантажимо архів atom zip для windows та розархівуємо його.
  * Скопіюємо папку у Program Files.
  * Запускаємо atom у папці


### *3.* Оновлення браузера

Відкрий [whatbrowser.org](http://whatbrowser.org) та онови свій браузер, якщо у тебе не остання версія. 

Це все! Тепер у тебе все необхідне для створення свого першого додатка на Ruby on Rails:)
<hr />

## Setup for Linux

### *1.* Установка Rails


Для того, щоб установити Ruby on Rails необхідно просто скопіювати команду для твого дистрибутива Linux (Ubuntu чи Fedora), вставити команду у термінал та набравшись терпіння спостерігати, як пролітають команди на моніторі. 

#### Для Ubuntu:

~~~
bash < <(curl -sL https://raw.github.com/railsgirls/installation-scripts/master/rails-install-ubuntu.sh)
~~~

Якщо ти будеш використовувати RVM установку з gnome-terminal, то тут ти знайдеш детальніше як це зробити: [RVM documentation](http://rvm.io/integration/gnome-terminal).

#### Для Fedora:

~~~
bash < <(curl -sL https://raw.github.com/railsgirls/installation-scripts/master/rails-install-fedora.sh)
~~~

Для того, щоб переконатись, що все працює запустимо команду сторення додатка

~~~
rails new railsgirls
cd railsgirls
rails server
~~~


### *2.* Встановлення текстового редактора

Для воркшопу ми рекомендуємо текстовий редактор Sublime Text.

* [Download Sublime Text and install it](http://www.sublimetext.com/2)


### *3.* Оновлення браузера

Відкрий [whatbrowser.org](http://whatbrowser.org) та онови свій браузер, якщо у тебе не остання версія. 

Це все! Тепер у тебе все необхідне для створення свого першого додатку на Ruby on Rails:)

<hr />


## Virtual Machine

Замість установки всіх програм на свій ноутбук ти можеш встановити середовище програмування на віртуальній машині.Тут детальніше про налаштування віртуального середовища: [Virtual machine]({% post_url 2014-03-24-alternative-dev-environment %}).

<hr />


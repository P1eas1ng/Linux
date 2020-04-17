# Linux. Конспект по курсу LPIC 105.1.
## Часть 1. Что такое файлы профилей и зачем они нужны.
Так в большом существует много количество большое количество профилей и эти профиле срабатывают относительно того пользователя под которым они запущены. У нас есть глобальные настройки пользователя и есть пользовательские. Пользовательские лежат в каталоге пользователя в символе ~  ~/.bashrc  если нам вдруг нужно получить а или записать некоторые aliasы, то тогда мы можем там записать альянсы, можно выписать функции и всё остальное. Реализация функций это в общем-то замена команд которые мы могли бы использовать. Но просто удобнее их использовать когда мы заменяем некоторые нужные и длинные команды. В папке /etc/ находится файл папка профиля глобального профиля Linux. 
В начале запуска системы и входа пользователя, linux грузит файл /etc/bash.bashrc и выполняет скрипты из /etc/profile.d/ .Файл bash.bashrc - определяет поведение командной строки и отвечает за глобальный профиль пользователя. Этот файл запускает различные псевдонимы и глобальные функции. в папке /etc/ лежит папка profile.d и эти скрипты будут запускаться при входе пользователя в систему. В нашей папке пользователя home или root лежат настройки того пользователя, под которым запущен linux. В папке пользователя лежит файл .bashrc и .profile. Файл .profile содержит настройки конкретного пользователя. Там лежит несколько переменных и он зависит от .bashrc. В .bashrc лежит файловая история, обновление, псевдонимы, настройки цветовой оболочки. В ней лежат все настройки профиля. Есть файл .bash_logout и там находятся настройки для выхода пользователя из системы. А так же у нас есть папке /etc/skel, в которой находятся настройки системы и файлы. И каждый новый пользователь, который будет создан, получит эти файлы в домашний каталог. Туда можно добавить файлы и они будут автоматически добавлены в каталог нового пользователя.
## Часть 2 и 3. Псевдонимы и функции.
Псевдонимы и функции определяются во всех этих файлах профилей пользователей. Псевдонимы по-другому называют aliasы. Итак, как же создавать aliasы и функции? 
Во-первых,aliasы и функции лучше всего создавать для конкретного пользователя, то есть в папке пользователя /home/$USER/ в файле /home/$USER/.bashrc, но кроме root пользователя. Его настройки лежат в другом месте, то есть в папке /root/ в файле /root/.bashrc. 
Псевдонимы и функции нужны чтобы упростить пользование командами. Например, есть утилита fdisk и она запускается только так: 
```bash
sudo fdisk
``` 
И чтобы не писать лишние слова типа sudo, люди придумали псеводнимы(alias). Как же их создать?  
Alias создается прописыванием команды 
```bash
la='ls -a'
``` 
в /home/$USER/.bashrc, где la -это псевдоним, а ls -a - это команда, которой вы хотите сделать псевдоним.
Приведу пример с sudo fdisk:
```bash
fdisk='sudo fdisk'
``` 
Alias Отличается от функции тем, что alias - это текст для вызова команды с ключами, а функция - это текст для выхова скрипта из нескольких команд.
Создание функций немного отличается от создания aliasов.
Функция создается так:
```bash
function Hello(){
echo 'I am awake for: ';
uptime -p;
}
``` 
Данная функция скажет: 'I am awake for: time', где time - это результат выполнения команды uptime -p, при которой выводится время, которое работает система с начала запуска.
#### Есть еще одно использование функции:
В функцию можно тоже передавать ключи.
```bash
function Hello(){
echo Hello my dear $1;
}
```
И при запуске этой функции с передачей значении имени, она напишет: Hello  my dear $1, где $1 - имя того пользователя, которого вы введете.
То есть если я введу 
```bash
Hello User
``` 
Я получу ответ : Hello my dear User.
Аргументы в функцию можно передавать сколько угодно, но видны они в функции будут только через $1, $2, $3, ... .
Но есть еще и аргумент $0, который передает в функцию название функции.
## Часть 4. Переменные.
В общем в оболочке есть огромное кол-во различных вещей:
Переменные, переменные среды, команды.
В общем, все по порядку:
Переменные - раотают только в пределах текущей оболочки.
Переменные среды - работают во всех дочерних процессах.
Команды действий с переменными:
```bash
set /// Вывод всех переменных и функций.
unset /// Удаление переменных.
export /// Превращение переменной в переменную среды.
env /// Вывод переменных среды.
``` 
Еще есть переменная Path.
В ней содержится путь к исполняемым файлам.

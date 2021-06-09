## Laboratory work II

Данная лабораторная работа посвещена изучению систем контроля версий на примере **Git**.

```bash
$ open https://git-scm.com
```

## Tasks

- [x] 1. Создать публичный репозиторий с названием **lab02** и с лиценцией **MIT**
- [x] 2. Сгенирировать токен для доступа к сервису **GitHub** с правами **repo**
- [x] 3. Ознакомиться со ссылками учебного материала
- [x] 4. Выполнить инструкцию учебного материала
- [x] 5. Составить отчет и отправить ссылку личным сообщением в **Slack**

## Tutorial

```sh
# Устанавливаем переменную имя пользователя
$ export GITHUB_USERNAME=tishchka
# Устанавливаем переменную почтового ящика
$ export GITHUB_EMAIL=katya.t0505@gmail.com
# Устанавливаем переменную токена
$ export GITHUB_TOKEN=****************************************
# Создаем команду открытия текстового редактора subl
$ alias edit=subl
```

```sh
# Перемещаемся в рабочую директорию
$ cd ${GITHUB_USERNAME}/workspace
# Исполняем команду из файла scripts/activate
$ source scripts/activate
```

```sh
# Создаем директорию .config в tishchka
$ mkdir ~/.config
# mkdir: cannot create directory ‘/home/gndavydov/.config’: File exists
# Директория была уже создана в 1-ой лаба
# Записали следующие настройки в файл config/hub
$ cat > ~/.config/hub <<EOF
github.com:
- user: ${GITHUB_USERNAME}
  oauth_token: ${GITHUB_TOKEN}
  protocol: https
EOF
# Устанавливаем протокол https, по которому будут передаваться данные
$ git config --global hub.protocol https
```

```sh
# Создаем директорию projects/lab02 и переходим в нее
$ mkdir projects/lab02 && cd projects/lab02
# Cоздаём в текущем каталоге новый подкаталог с именем .git, 
# содержащий все необходимые файлы репозитория — структуру Git репозитория
$ git init
$ git config --global user.name ${GITHUB_USERNAME}
$ git config --global user.email ${GITHUB_EMAIL}
# check your git global settings
# Проверяем установившиеся настройки
$ git config -e --global
# Добавляем удаленный репозиторий
$ git remote add origin https://github.com/${GITHUB_USERNAME}/lab02.git
# Скачиваем и затем вливаем данные из удалённой ветки в вашу текущую ветку
$ git pull origin main
# Создаем README.md файл
$ touch README.md
# Получаем статус по текущим изменениям
$ git status
On branch master
Untracked files:
  (use "git add <file>..." to include in what will be committed)
	README.md

# Добавляем для отслеживания README.md файл
$ git add README.md
# Создаем коммит для сохранения изменений
$ git commit -m"added README.md"
# Отправляем изменения на сервер
$ git push origin main
```

Добавить на сервисе **GitHub** в репозитории **lab02** файл **.gitignore**
со следующем содержимом:

```sh
*build*/
*install*/
*.swp
.idea/
```

```sh
$ git pull origin main
# Просматриваем список коммитов
$ git log
commit e226ded122a08558d6a56099c611bbdde41a533d (HEAD -> main, origin/main)
Author: tishchka <57598627+tishchka@users.noreply.github.com>
Date:   Mon Mar 15 20:07:33 2021 +0300

    Create  .gitignore

commit 4a69317490ff3f9cc56bbd6a19c17ad49e2a0594 (origin/master, master)
Author: tishchka <katya.t0505@gmail.com>
Date:   Mon Mar 15 09:22:45 2021 -0700

    added README.md

commit 433ffb427629fe2ecbf42b619dd63a40022316a3
Author: tishchka <57598627+tishchka@users.noreply.github.com>
Date:   Mon Mar 15 17:54:54 2021 +0300

    Initial commit
```

```sh
# Создаем директорию sources
$ mkdir sources
# Создаем директорию include
$ mkdir include
# Создаем директорию examples
$ mkdir examples
# Создаем файл print.cpp в sources со соледующим кодом
$ cat > sources/print.cpp <<EOF
#include <print.hpp>

void print(const std::string& text, std::ostream& out)
{
  out << text;
}

void print(const std::string& text, std::ofstream& out)
{
  out << text;
}
EOF
```

```sh
# Создаем файл print.hpp в include со соледующим кодом
$ cat > include/print.hpp <<EOF
#include <fstream>
#include <iostream>
#include <string>

void print(const std::string& text, std::ofstream& out);
void print(const std::string& text, std::ostream& out = std::cout);
EOF
```

```sh
# Создаем файл example1.cpp в examples со соледующим кодом
$ cat > examples/example1.cpp <<EOF
#include <print.hpp>

int main(int argc, char** argv)
{
  print("hello");
}
EOF
```

```sh
# Создаем файл example2.cpp в examples со соледующим кодом
$ cat > examples/example2.cpp <<EOF
#include <print.hpp>

#include <fstream>

int main(int argc, char** argv)
{
  std::ofstream file("log.txt");
  print(std::string("hello"), file);
}
EOF
```

```sh
# Редактируем файл README.md
$ edit README.md
```

```sh
# Получаем статус по текущим изменениям
$ git status
On branch main
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
	modified:   README.md

Untracked files:
  (use "git add <file>..." to include in what will be committed)
	examples/
	include/
	sources/

no changes added to commit (use "git add" and/or "git commit -a")

# Добавляем для отслеживания все файлы
$ git add .
# Создаем коммит
$ git commit -m"added sources"
# Отправляем изменения на сервер
$ git push origin main
```

## Report

```sh
$ cd ~/workspace/
$ export LAB_NUMBER=02
$ git clone https://github.com/tp-labs/lab${LAB_NUMBER}.git tasks/lab${LAB_NUMBER}
$ mkdir reports/lab${LAB_NUMBER}
$ cp tasks/lab${LAB_NUMBER}/README.md reports/lab${LAB_NUMBER}/REPORT.md
$ cd reports/lab${LAB_NUMBER}
$ edit REPORT.md
$ gist REPORT.md
```

## Homework

### Part I

1. Создайте пустой репозиторий на сервисе github.com (или gitlab.com, или bitbucket.com).
2. Выполните инструкцию по созданию первого коммита на странице репозитория, созданного на предыдещем шаге.
3. Создайте файл `hello_world.cpp` в локальной копии репозитория (который должен был появиться на шаге 2). Реализуйте программу **Hello world** на языке C++ используя плохой стиль кода. Например, после заголовочных файлов вставьте строку `using namespace std;`.
4. Добавьте этот файл в локальную копию репозитория.
5. Закоммитьте изменения с *осмысленным* сообщением.
6. Изменитьте исходный код так, чтобы программа через стандартный поток ввода запрашивалось имя пользователя. А в стандартный поток вывода печаталось сообщение `Hello world from @name`, где `@name` имя пользователя.
7. Закоммитьте новую версию программы. Почему не надо добавлять файл повторно `git add`?
8. Запуште изменения в удалёный репозиторий.
9. Проверьте, что история коммитов доступна в удалёный репозитории.

### Part II

**Note:** *Работать продолжайте с теми же репоззиториями, что и в первой части задания.*
1. В локальной копии репозитория создайте локальную ветку `patch1`.
2. Внесите изменения в ветке `patch1` по исправлению кода и избавления от `using namespace std;`.
3. **commit**, **push** локальную ветку в удалённый репозиторий.
4. Проверьте, что ветка `patch1` доступна в удалёный репозитории.
5. Создайте pull-request `patch1 -> master`.
6. В локальной копии в ветке `patch1` добавьте в исходный код комментарии.
7. **commit**, **push**.
8. Проверьте, что новые изменения есть в созданном на **шаге 5** pull-request
9. В удалённый репозитории выполните  слияние PR `patch1 -> master` и удалите ветку `patch1` в удаленном репозитории.
10. Локально выполните **pull**.
11. С помощью команды **git log** просмотрите историю в локальной версии ветки `master`.
12. Удалите локальную ветку `patch1`.

### Part III

**Note:** *Работать продолжайте с теми же репоззиториями, что и в первой части задания.*
1. Создайте новую локальную ветку `patch2`.
2. Измените *code style* с помощью утилиты [**clang-format**](http://clang.llvm.org/docs/ClangFormat.html). Например, используя опцию `-style=Mozilla`.
3. **commit**, **push**, создайте pull-request `patch2 -> master`.
4. В ветке **master** в удаленном репозитории измените комментарии, например, расставьте знаки препинания, переведите комментарии на другой язык.
5. Убедитесь, что в pull-request появились *конфликтны*.
6. Для этого локально выполните **pull** + **rebase** (точную последовательность команд, следует узнать самостоятельно). **Исправьте конфликты**.
7. Сделайте *force push* в ветку `patch2`
8. Убедитель, что в pull-request пропали конфликтны. 
9. Вмержите pull-request `patch2 -> master`.

## Links

- [hub](https://hub.github.com/)
- [GitHub](https://github.com)
- [Bitbucket](https://bitbucket.org)
- [Gitlab](https://about.gitlab.com)
- [LearnGitBranching](http://learngitbranching.js.org/)

```
Copyright (c) 2015-2021 The ISC Authors
```

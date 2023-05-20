#lab02

# Task 1

## 1. Создайте пустой репозиторий на сервисе github.com (или `gitlab.com`, или `bitbucket.com`)

```
https://github.com/vladosfpv/lab02
```
![Безымянный](https://github.com/vladosfpv/lab02/assets/57360144/7cd399c7-9cf5-46f0-b769-430406eceb95)


## 2. Выполните инструкцию по созданию первого коммита на странице репозитория, созданного на предыдещем шаге
 
```
$ mkdir lab-02
$ echo "# lab-02" >> README.md
$ git init
$ git add README.md
$ git commit -m "first commit"
$ git remote add origin https://github.com/vladosfpv/lab02.git
$ git push -u origin master
```

## 3. Создайте файл `hello_world.cpp` в локальной копии репозитория (который должен был появиться на шаге 2). Реализуйте программу `Hello world` на языке C++ используя плохой стиль кода. Например, после заголовочных файлов вставьте строку `using namespace std;`
 
```
#include <iostream>

using namespace std;

int main(int argc, char** argv) {
   cout << "Hello world" << endl;
}
```

## 4. Добавьте этот файл в локальную копию репозитория
 
```
$ git add "Hello world.cpp"
```

## 5. Закоммитьте изменения с осмысленным сообщением
 
```
$ git commit -m "This is first file"
```

## 6. Изменитьте исходный код так, чтобы программа через стандартный поток ввода запрашивалось имя пользователя. А в стандартный поток вывода печаталось сообщение `Hello world` from `@name`, где `@name` имя пользователя
 
```
$ alias edit=subl
$ edit "Hello world.cpp"
```
```
#include <iostream>
#include <string>
 
using namespace std;

int main(int argc, char** argv) {
   string name;
   cin >> name;
   cout << "Hello world from " << name << endl;
}
```

## 7. Закоммитьте новую версию программы. Почему не надо добавлять файл повторно `git add`?

You do not need to re-write the git add command, because the file was already added in step 4
```
$ git commit -a -m "Changed cpp file"
```

## 8. Запуште изменения в удалёный репозиторий
 
```
$ git push -u origin master
```

## 9. Проверьте, что история коммитов доступна в удалёный репозитории
 
The history of changes is available in the repository

# Task 2

## 1. В локальной копии репозитория создайте локальную ветку `patch1`
 
```
$ git checkout -b patch1
```

## 2. Внесите изменения в ветке `patch1` по исправлению кода и избавления от `using namespace std;`
 
```
$ edit "Hello world.cpp"
```
```
#include <iostream>
#include <string>
 
int main(int argc, char** argv){
  string name;
  std::cin >> name;
  std::cout << "Hello world from " << name << std::endl;
}
```

## 3. `commit`, `push` локальную ветку в удалённый репозиторий
 
```
$ git commit -a -m "Fixed cpp file"
$ git push -u origin patch1
```

## 4. Проверьте, что ветка `patch1` доступна в удалёный репозитории
 
The `patch1` branch is available in the remote repository

## 5. Создайте `pull-request` `patch1 -> master`
 
Create a pull-request `patch1 -> master`

## 6. В локальной копии в ветке `patch1` добавьте в исходный код комментарии
 
```
$ edit "Hello world.cpp"
```
```
#include <iostream>
#include <string>
 
int main(int argc, char** argv){
  string name;                                           // Name of @user
  std::cin >> name;                                      // Input name of @user
  std::cout << "Hello world from " << name << std::endl; // Output name of @user
} 
```

## 7. `commit, push`
 
```
$ git commit -a -m "Code with comments"
$ git push -u origin patch1
```

## 8. Проверьте, что новые изменения есть в созданном на шаге 5 `pull-request`
 
There are new changes in the pull-request created in step 5

## 9. В удалённый репозитории выполните слияние `PR` `patch1 -> master` и удалите ветку `patch1` в удаленном репозитории

## 10. Локально выполните `pull`
 
```
$ git pull origin
```

## 11. С помощью команды `git log` просмотрите историю в локальной версии ветки `master`
 
```
$ git log master
```

## 12. Удалите локальную ветку `patch1`

```
$ git branch -d patch1
```

# Task 3

## 1. Создайте новую локальную ветку `patch2`
 
```
$ git checkout -b patch2
```

## 2. Измените `code style` с помощью утилиты `clang-format`. Например, используя опцию `-style=Mozilla`
 
```
$ clang-format -i -style=Mozilla "hello world.cpp"
```

## 3. `commit`, `push`, создайте `pull-request `patch2 -> master`
 
```
$ git commit -a -m "Changed code style in cpp file"
$ git push -u origin patch2
```

## 4. В ветке master в удаленном репозитории измените комментарии, например, расставьте знаки препинания, переведите комментарии на другой язык
 
```
$ git checkout master
$ edit "Hello world.cpp"
```
```
#include <iostream>
#include <string>
 
int main(int argc, char** argv){
  string name;                                           // Имя пользователя
  std::cin >> name;                                      // Ввод имени пользователя
  std::cout << "Hello world from " << name << std::endl; // Вывод данных
} 
```
```
$ git commit -a -m "Fixed cpp file"
$ git push -u origin patch2
```

## 5. Убедитесь, что в `pull-request` появились конфликтны
 
Yes, there were conflicts

## 6. Для этого локально выполните `pull + rebase` (точную последовательность команд, следует узнать самостоятельно). Исправьте конфликты
 
```
$ git pull origin master
$ git rebase master
$ edit "Hello world.cpp"
$ git commit -a -m "Update code"
```

## 7. Сделайте `force push` в ветку `patch2`
 
```
$ git pull origin master
$ git rebase master
$ edit "Hello world.cpp"
$ git commit -a -m "Update Hello world.cpp"
$ git rebase --continue
```

## 8. Убедитель, что в `pull-request` пропали конфликтны
 
Conflicts have disappeared

## 9. Вмержите `pull-request` `patch2 -> master`


![Безымянный](https://github.com/vladosfpv/lab02/assets/57360144/29f292a7-06f9-4716-b1f5-74b2c46f0490)


## Required libraries

```
$ sudo apt install git
$ sudo snap install sublim-text
$ sudo apt install clang-format
```

## References used
- https://habr.com/ru/post/541258/
- https://losst.pro/komandy-linux-dlya-raboty-s-fajlami
- https://ru.stackoverflow.com/questions/134183/Что-такое-pull-request
- https://hub.github.com/
- https://github.com/
- https://bitbucket.org/
- https://about.gitlab.com/
- http://learngitbranching.js.org/

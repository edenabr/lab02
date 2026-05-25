## Part I

### Переходим в папку проекта

```bash
cd ~/Desktop/projects/lab02h
```
Инициализируем Git-репозиторий
```sh
git init
git branch -M main
```

Настраиваем имя пользователя и почту
```sh
git config --global user.name "edenabr"
git config --global user.email "edenabramova@gmail.com"
```

Подключаем удалённый репозиторий GitHub
```
git remote add origin https://github.com/edenabr/lab02.git
git remote -v
```
Создаём файл hello_world.cpp
```sh
cat > hello_world.cpp <<'EOF'
#include <iostream>

using namespace std;

int main()
{
    cout << "Hello world" << endl;
    return 0;
}
EOF
```
Проверяем состояние репозитория
```sh
git status
```

Добавляем файл в индекс
```sh
git add hello_world.cpp
```

Создаём первый коммит
```sh
git commit -m "added hello world program"
```


<details>

<summary>Вывод: </summary>
<pre>
Enumerating objects: 3, done.
Counting objects: 100% (3/3), done.
Delta compression using up to 4 threads
Compressing objects: 100% (2/2), done.
Writing objects: 100% (3/3), 317 bytes | 317.00 KiB/s, done.
Total 3 (delta 0), reused 0 (delta 0), pack-reused 0 (from 0)
To https://github.com/edenabr/lab02.git
 * [new branch]      main -> main
branch 'main' set up to track 'origin/main'.</pre>
</details>


Отправляем изменения на GitHub
```sh
git push -u origin main
```

Изменяем hello_world.cpp: добавляем ввод имени
```sh
cat > hello_world.cpp <<'EOF'
#include <iostream>
#include <string>

using namespace std;

int main()
{
    string name;
    cin >> name;
    cout << "Hello world from @" << name << endl;
    return 0;
}
EOF
```

Проверяем изменения
```sh
git status
```

Добавляем обновлённый файл
```sh
git add hello_world.cpp
```
Второй коммит:
```sh
git commit -m "updated hello world program"
```
Отправляем второй коммит на GitHub
```sh
git push
```
<details>

<summary>Вывод: </summary>
<pre>
On branch main
Your branch is up to date with 'origin/main'.

Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
 modified:   hello_world.cpp

no changes added to commit (use "git add" and/or "git commit -a")
[main 528e140] updated hello world program
 1 file changed, 4 insertions(+), 1 deletion(-)
Username for 'https://github.com': edenabr
Password for 'https://edenabr@github.com': 
Enumerating objects: 5, done.
Counting objects: 100% (5/5), done.
Delta compression using up to 4 threads
Compressing objects: 100% (2/2), done.
Writing objects: 100% (3/3), 375 bytes | 375.00 KiB/s, done.
Total 3 (delta 0), reused 0 (delta 0), pack-reused 0 (from 0)
To https://github.com/edenabr/lab02.git
   17996e9..528e140  main -> main
* 528e140 (HEAD -> main, origin/main) updated hello world program
* 17996e9 added hello world program </pre>
</details>















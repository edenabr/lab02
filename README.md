# Part I

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

# Part II. Ветка `patch1`

## 1. Создание локальной ветки `patch1`

```bash
git checkout -b patch1
```

Проверка текущей ветки:

```bash
git branch
```

## 2. Исправление кода и удаление `using namespace std;`

В файле `hello_world.cpp` были внесены исправления:

```cpp
#include <iostream>
#include <string>

int main()
{
    // Read user name from standard input
    std::string name;
    std::cin >> name;

    // Print greeting message
    std::cout << "Hello world from @" << name << std::endl;

    return 0;
}
```

Проверка изменений:

```bash
git status
git diff
```

Добавление файла в индекс:

```bash
git add hello_world.cpp
```

## 3. Коммит и отправка ветки `patch1` в удалённый репозиторий

```bash
git commit -m "Fixed code style"
git push -u origin patch1
```

## 4. Проверка, что ветка `patch1` появилась в удалённом репозитории

```bash
git branch -r
git ls-remote --heads origin patch1
```

## 5. Создание pull request `patch1 -> main`

Pull request был создан на GitHub:

```text
base: main
compare: patch1
PR: #1
```

Если делать то же самое через GitHub CLI, команда была бы такой:

```bash
gh pr create --base main --head patch1 --title "Fixed code style" --body "Fixed code style"
```

## 6. Добавление комментариев в исходный код в ветке `patch1`

Переход обратно в ветку `patch1`:

```bash
git checkout patch1
```

После добавления комментариев в `hello_world.cpp`:

```bash
git status
git diff
git add hello_world.cpp
```

## 7. Коммит и push новых изменений в `patch1`

```bash
git commit -m "Add comments to source code"
git push origin patch1
```

После этого уже созданный pull request `#1` автоматически обновился, потому что новые изменения были отправлены в ту же ветку `patch1`.

## 8. Проверка, что новые изменения появились в PR

Локальная проверка истории:

```bash
git log --oneline --decorate --graph --all
```

Открытие PR в браузере через GitHub CLI:

```bash
gh pr view 1 --web
```

## 9. Слияние PR `patch1 -> main` и удаление удалённой ветки `patch1`

В истории GitHub появился merge-коммит:

```text
80e8057 Merge pull request #1 from edenabr/patch1
```


## 10. Локальное обновление ветки `main`

```bash
git checkout main
git pull origin main
```

## 11. Просмотр истории локальной ветки `main`

```bash
git log --oneline --decorate --graph
```

В истории должен быть виден merge-коммит:

```text
80e8057 Merge pull request #1 from edenabr/patch1
```

## 12. Удаление локальной ветки `patch1`

```bash
git branch -d patch1
```

Если Git не разрешает удалить ветку после проверки, можно использовать принудительное удаление:

```bash
git branch -D patch1
```

---

# Part III. Ветка `patch2`

## 1. Создание новой локальной ветки `patch2`

Сначала была обновлена ветка `main` после merge `patch1`:

```bash
git checkout main
git pull origin main
```

Создание новой ветки:

```bash
git checkout -b patch2
```

## 2. Форматирование кода с помощью `clang-format`

Форматирование файла `hello_world.cpp` в стиле Mozilla:

```bash
clang-format -i -style=Mozilla hello_world.cpp
```

Проверка изменений:

```bash
git status
git diff
```

Добавление изменений в индекс:

```bash
git add hello_world.cpp
```

## 3. Коммит, push и создание PR `patch2 -> main`

```bash
git commit -m "formatted code with clang-format"
git push -u origin patch2
```

Pull request был создан на GitHub:

```text
base: main
compare: patch2
PR: #2
```


## 4. Изменение комментариев в ветке `main`

В ветке `main` был изменён файл `hello_world.cpp`: комментарии были отредактированы, чтобы затем получить конфликт с веткой `patch2`.

На GitHub появился коммит:

```text
e13c6bc Update hello_world.cpp
```

Если выполнять этот шаг локально, команды были бы такими:

```bash
git checkout main
git pull origin main
```

После редактирования комментариев:

```bash
git status
git diff
git add hello_world.cpp
git commit -m "Update hello_world.cpp"
git push origin main
```

## 5. Проверка появления конфликтов в PR

После изменения `main` pull request `#2` получил конфликты.

Локально можно проверить актуальное состояние веток:

```bash
git fetch origin
git checkout patch2
git status
git log --oneline --decorate --graph --all
```

## 6. Выполнение pull + rebase и исправление конфликтов

Для переноса ветки `patch2` поверх актуальной ветки `main` была выполнена команда rebase:

```bash
git checkout patch2
git pull --rebase origin main
```

Альтернативная запись тех же действий:

```bash
git fetch origin
git rebase origin/main
```

При конфликте Git останавливает rebase. Конфликтующий файл нужно открыть и исправить вручную:

```bash
nano hello_world.cpp
```

или в VS Code:

```bash
code hello_world.cpp
```

После исправления конфликтов:

```bash
git status
git add hello_world.cpp
git rebase --continue
```

Если Git снова остановился на следующем конфликте, команды повторяются:

```bash
git status
git add hello_world.cpp
git rebase --continue
```

Проверка результата после завершения rebase:

```bash
git status
git log --oneline --decorate --graph --all
```

После rebase итоговый коммит форматирования получил хэш:

```text
9a2212b formatted code with clang-format
```

## 7. Force push в ветку `patch2`

Так как после `rebase` история ветки `patch2` изменилась, потребовалась принудительная отправка ветки в GitHub:

```bash
git push --force-with-lease origin patch2
```

## 8. Проверка, что конфликты исчезли из PR

Pull request `#2` был обновлён после force push.

Открытие PR:

```bash
gh pr view 2 --web
```

Локальная проверка истории:

```bash
git fetch origin
git log --oneline --decorate --graph --all
```

## 9. Слияние PR `patch2 -> main`

Pull request `#2` был слит в `main`.

В истории GitHub появился merge-коммит:

```text
d3f6bf4 Merge pull request #2 from edenabr/patch2
```


Если merge был выполнен через сайт GitHub, удалённую ветку можно удалить командой:

```bash
git push origin --delete patch2
```

Обновление локальной ветки `main` после merge:

```bash
git checkout main
git pull origin main
```

Удаление локальной ветки `patch2`:

```bash
git branch -d patch2
```

---

## Итоговая история коммитов

Для просмотра истории использовалась команда:

```bash
git log --oneline --decorate --graph --all
```

Итоговая последовательность основных коммитов:

```text
*   d3f6bf4 Merge pull request #2 from edenabr/patch2
|\
| * 9a2212b formatted code with clang-format
|/
* e13c6bc Update hello_world.cpp
*   80e8057 Merge pull request #1 from edenabr/patch1
|\
| * cd2bc66 tip ветки patch1 перед merge
|/
* 528e140 предыдущий коммит main перед merge #1
```














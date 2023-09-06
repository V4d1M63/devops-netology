## Домашнее задание к занятию «Ветвления в Git» - Вдовин Вадим
 
### Задание «Ветвление, merge и rebase»

Шаг 1. Предположим, что есть задача — написать скрипт, выводящий на экран параметры его запуска. Давайте посмотрим, как будет отличаться работа над этим скриптом с использованием ветвления, merge и rebase.

Создайте в своём репозитории каталог branching и в нём два файла — merge.sh и rebase.sh — с содержимым:
```
#!/bin/bash
# display command line options

count=1
for param in "$*"; do
    echo "\$* Parameter #$count = $param"
    count=$(( $count + 1 ))
done
```
Этот скрипт отображает на экране все параметры одной строкой, а не разделяет их.

![0](https://github.com/V4d1M63/devops-netology/assets/130470784/64a79318-130c-42ef-9e11-c4670b899791)

Шаг 2. Создадим коммит с описанием prepare for merge and rebase и отправим его в ветку main.
```
# git add *                                                                                                                                    
# git commit -m 'prepare for merge and rebase'
[main 7d23527] prepare for merge and rebase
 2 files changed, 16 insertions(+)
 create mode 100644 branching/merge.sh
 create mode 100644 branching/rebase.sh
```

### Подготовка файла merge.sh

Шаг 1. Создайте ветку git-merge.

![1](https://github.com/V4d1M63/devops-netology/assets/130470784/655fe3da-4be8-46dc-9833-6d0d964198dd)

Шаг 2. Замените в ней содержимое файла merge.sh на:
```
#!/bin/bash
# display command line options

count=1
for param in "$@"; do
    echo "\$@ Parameter #$count = $param"
    count=$(( $count + 1 ))
done
```
Шаг 3. Создайте коммит merge: @ instead *, отправьте изменения в репозиторий.

![2](https://github.com/V4d1M63/devops-netology/assets/130470784/db63aaeb-3f40-4128-aeef-d55875d1df9f)

Шаг 4. Разработчик подумал и решил внести ещё одно изменение в merge.sh:
```
#!/bin/bash
# display command line options

count=1
while [[ -n "$1" ]]; do
    echo "Parameter #$count = $1"
    count=$(( $count + 1 ))
    shift
done
```

Теперь скрипт будет отображать каждый переданный ему параметр отдельно.

Шаг 5. Создайте коммит merge: use shift и отправьте изменения в репозиторий.

![3](https://github.com/V4d1M63/devops-netology/assets/130470784/fd25c7ef-a868-4378-b59d-bb7766cce14f)

### Изменим main

Шаг 1. Вернитесь в ветку main. Шаг 2. Предположим, что пока мы работали над веткой git-merge, кто-то изменил main. Для этого изменим содержимое файла rebase.sh на:
```
#!/bin/bash
# display command line options

count=1
for param in "$@"; do
    echo "\$@ Parameter #$count = $param"
    count=$(( $count + 1 ))
done

echo "====="
```
В этом случае скрипт тоже будет отображать каждый параметр в новой строке.

Шаг 3. Отправляем изменённую ветку main в репозиторий.

![4](https://github.com/V4d1M63/devops-netology/assets/130470784/0c9d4960-f4db-4a9f-a946-f95154fb8e09)

### Подготовка файла rebase.sh

Шаг 1. Предположим, что теперь другой участник нашей команды не сделал git pull либо просто хотел ответвиться не от последнего коммита в main, а от коммита, когда мы только создали два файла merge.sh и rebase.sh на первом шаге.
Для этого при помощи команды git log найдём хеш коммита prepare for merge and rebase и выполним git checkout на него так: git checkout 8baf217e80ef17ff577883fda90f6487f67bbcea (хеш будет другой).

![5](https://github.com/V4d1M63/devops-netology/assets/130470784/abdc68ce-3bb7-46c5-8ca5-2583cb2f205d)

![6](https://github.com/V4d1M63/devops-netology/assets/130470784/f1b300dd-838d-4b90-aa17-98f392f650aa)

 Шаг 2. Создадим ветку git-rebase, основываясь на текущем коммите. 

![7](https://github.com/V4d1M63/devops-netology/assets/130470784/eb812be9-c753-4980-917f-8fba52cbd8b8)

 Шаг 3. И изменим содержимое файла rebase.sh на следующее, тоже починив скрипт, но немного в другом стиле:
```
#!/bin/bash
# display command line options

count=1
for param in "$@"; do
    echo "Parameter: $param"
    count=$(( $count + 1 ))
done

echo "====="
```
Шаг 4. Отправим эти изменения в ветку git-rebase с комментарием git-rebase 1.

![8](https://github.com/V4d1M63/devops-netology/assets/130470784/4d965bc9-95c3-4421-ade2-9eebb2e13913)

Шаг 5. И сделаем ещё один коммит git-rebase 2 с пушем, заменив echo "Parameter: $param" на echo "Next parameter: $param".
```
# git commit -m 'git-rebase 2'
[git-rebase de7659e] git-rebase 2
 1 file changed, 1 insertion(+), 1 deletion(-)
```
![9](https://github.com/V4d1M63/devops-netology/assets/130470784/bb7df61d-2e11-4246-9315-14153bbe797c)

### Промежуточный итог

Мы сэмулировали типичную ситуации в разработке кода, когда команда разработчиков работала над одним и тем же участком кода, и кто-то из разработчиков предпочитает делать merge, а кто-то — rebase. Конфликты с merge обычно решаются просто, а с rebase бывают сложности, поэтому давайте смержим все наработки в main и разрешим конфликты.

Если всё было сделано правильно, то на странице network в GitHub, находящейся по адресу https://github.com/ВАШ_ЛОГИН/ВАШ_РЕПОЗИТОРИЙ/network, будет примерно такая схема:

![11](https://github.com/V4d1M63/devops-netology/assets/130470784/e0f80f09-09d8-4e1a-b7c2-104554220399)

### Merge

Сливаем ветку git-merge в main и отправляем изменения в репозиторий, должно получиться без конфликтов:
```
$ git merge git-merge
Merge made by the 'recursive' strategy.
 branching/merge.sh | 5 +++--
 1 file changed, 3 insertions(+), 2 deletions(-)
$ git push
#!/bin/bash
Enumerating objects: 1, done.
Counting objects: 100% (1/1), done.
Writing objects: 100% (1/1), 223 bytes | 223.00 KiB/s, done.
Total 1 (delta 0), reused 0 (delta 0), pack-reused 0
```
В результате получаем такую схему:

![12](https://github.com/V4d1M63/devops-netology/assets/130470784/a717b036-84b2-4ff9-a917-854a7e6f8bec)

### Rebase

Шаг 1. Перед мержем ветки git-rebase выполним её rebase на main. Да, мы специально создали ситуацию с конфликтами, чтобы потренироваться их решать. Шаг 2. Переключаемся на ветку git-rebase и выполняем git rebase -i main. В открывшемся диалоге должно быть два выполненных коммита, давайте заодно объединим их в один, указав слева от нижнего fixup. В результате получаем:
```
$ git rebase -i main
Auto-merging branching/rebase.sh
CONFLICT (content): Merge conflict in branching/rebase.sh
error: could not apply dc4688f... git 2.3 rebase @ instead *
Resolve all conflicts manually, mark them as resolved with
"git add/rm <conflicted_files>", then run "git rebase --continue".
You can instead skip this commit: run "git rebase --skip".
To abort and get back to the state before "git rebase", run "git rebase --abort".
Could not apply dc4688f... git 2.3 rebase @ instead *
```
```
┌──(root㉿test)-[/home/test/devops-netology/branching]
└─# git rebase -i main
Auto-merging branching/rebase.sh
CONFLICT (content): Merge conflict in branching/rebase.sh
error: could not apply 66b9ece... git-rebase 1
hint: Resolve all conflicts manually, mark them as resolved with
hint: "git add/rm <conflicted_files>", then run "git rebase --continue".
hint: You can instead skip this commit: run "git rebase --skip".
hint: To abort and get back to the state before "git rebase", run "git rebase --abort".
Could not apply 66b9ece... git-rebase 1
```
Если посмотреть содержимое файла rebase.sh, то увидим метки, оставленные Git для решения конфликта:
```
cat rebase.sh
#!/bin/bash
# display command line options
count=1
for param in "$@"; do
<<<<<<< HEAD
    echo "\$@ Parameter #$count = $param"
=======
    echo "Parameter: $param"
>>>>>>> dc4688f... git 2.3 rebase @ instead *
    count=$(( $count + 1 ))
done
```
Шаг 3. Удалим метки, отдав предпочтение варианту:
```
echo "\$@ Parameter #$count = $param"
```
Шаг 4. Сообщим Git, что конфликт решён git add rebase.sh и продолжим rebase git rebase --continue.
```
┌──(root㉿test)-[/home/test/devops-netology/branching]
└─# git add rebase.sh

┌──(root㉿test)-[/home/test/devops-netology/branching]
└─# git rebase --continue 
Auto-merging branching/rebase.sh
CONFLICT (content): Merge conflict in branching/rebase.sh
error: could not apply de7659e... git-rebase 2
hint: Resolve all conflicts manually, mark them as resolved with
hint: "git add/rm <conflicted_files>", then run "git rebase --continue".
hint: You can instead skip this commit: run "git rebase --skip".
hint: To abort and get back to the state before "git rebase", run "git rebase --abort".
Could not apply de7659e... git-rebase 2
```
Шаг 5. Опять получим конфликт в файле rebase.sh при попытке применения нашего второго коммита. Давайте разрешим конфликт, оставив строчку echo "Next parameter: $param".

Шаг 6. Далее опять сообщаем Git о том, что конфликт разрешён — git add rebase.sh — и продолжим rebase — git rebase --continue.

В результате будет открыт текстовый редактор, предлагающий написать комментарий к новому объединённому коммиту:
```
# This is a combination of 2 commits.
# This is the 1st commit message:

Merge branch 'git-merge'

# The commit message #2 will be skipped:

# git 2.3 rebase @ instead * (2)
```
Все строчки, начинающиеся на #, будут проигнорированны.

После сохранения изменения Git сообщит:
```
Successfully rebased and updated refs/heads/git-rebase
```
```
┌──(root㉿test)-[/home/test/devops-netology/branching]
└─# git add rebase.sh
                                                                                                 
┌──(root㉿test)-[/home/test/devops-netology/branching]
└─# git rebase --continue
[detached HEAD 21f7f65] git-rebase 2
 1 file changed, 1 insertion(+), 1 deletion(-)
Successfully rebased and updated refs/heads/git-rebase.
```
Шаг 7. И попробуем выполнить git push либо git push -u origin git-rebase, чтобы точно указать, что и куда мы хотим запушить.

Эта команда завершится с ошибкой:
```
git push
To github.com:v4d1m63/devops-netology.git
 ! [rejected]        git-rebase -> git-rebase (non-fast-forward)
error: failed to push some refs to 'git@github.com:v4d1m63/devops-netology.git'
hint: Updates were rejected because the tip of your current branch is behind
hint: its remote counterpart. Integrate the remote changes (e.g.
hint: 'git pull ...') before pushing again.
hint: See the 'Note about fast-forwards' in 'git push --help' for details.
```
![13](https://github.com/V4d1M63/devops-netology/assets/130470784/e56d0d03-adb9-4daf-834b-ddacc1c3e5fa)

Это произошло, потому что мы пытаемся перезаписать историю.

Шаг 8. Чтобы Git позволил нам это сделать, добавим флаг force:
```
git push -u origin git-rebase -f
Enumerating objects: 10, done.
Counting objects: 100% (9/9), done.
Delta compression using up to 12 threads
Compressing objects: 100% (4/4), done.
Writing objects: 100% (4/4), 443 bytes | 443.00 KiB/s, done.
Total 4 (delta 1), reused 0 (delta 0), pack-reused 0
remote: Resolving deltas: 100% (1/1), completed with 1 local object.
To github.com:andrey-borue/devops-netology.git
 + 1829df1...e3b942b git-rebase -> git-rebase (forced update)
Branch 'git-rebase' set up to track remote branch 'git-rebase' from 'origin'.
```

![14](https://github.com/V4d1M63/devops-netology/assets/130470784/628b8ae8-0cb0-4e01-9ea8-77b0de05eab1)

Шаг 9. Теперь можно смержить ветку git-rebase в main без конфликтов и без дополнительного мерж-комита простой перемоткой:
```
$ git checkout main
Switched to branch 'main'
Your branch is up to date with 'origin/main'.

$ git merge git-rebase
Updating 6158b76..45893d1
Fast-forward
 branching/rebase.sh | 3 +--
 1 file changed, 1 insertion(+), 2 deletions(-)
 ```

![15](https://github.com/V4d1M63/devops-netology/assets/130470784/5a17dd6a-c89f-4611-87b7-1acf770dd8f5)

 ```                                                                                           
┌──(root㉿test)-[/home/test/devops-netology/branching]
└─# git merge git-rebase
Updating 0543f10..21f7f65
Fast-forward
 branching/rebase.sh | 2 +-
 1 file changed, 1 insertion(+), 1 deletion(-)
 ```

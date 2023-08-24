## Домашнее задание к занятию "Системы контроля версий"- "Вдовин Вадим"
 

### Задача 1. Создать и настроить репозиторий для дальнейшей работы на курсе.

В рамках курса вы будете писать скрипты и создавать конфигурации для различных систем, которые необходимо сохранять для будущего использования. Сначала надо создать и настроить локальный репозиторий, после чего добавить удалённый репозиторий на GitHub.

### Создание репозитория и первого коммита.

1. Зарегистрируйте аккаунт на https://github.com/. Если предпочитаете другое хранилище для репозитория, можно использовать его.

2. Создайте публичный репозиторий, который будете использовать дальше на протяжении всего курса, желательное с названием devops-netology. Обязательно поставьте галочку Initialize this repository with a README.

![Безымянный](https://github.com/V4d1M63/devops-netology/assets/130470784/b093a3a3-bbc3-45a8-8c8b-f16ea0ea3446)

3. Создайте авторизационный токен для клонирования репозитория.

![1](https://github.com/V4d1M63/devops-netology/assets/130470784/e962cde5-fc73-4b43-a104-ee408487ade9)


4. Склонируйте репозиторий, используя протокол HTTPS (git clone ...).
```
# git clone https://github.com/V4d1M63/devops-netology.git
Cloning into 'devops-netology'...
remote: Enumerating objects: 32, done.
remote: Counting objects: 100% (32/32), done.
remote: Compressing objects: 100% (24/24), done.
remote: Total 32 (delta 0), reused 0 (delta 0), pack-reused 0
Receiving objects: 100% (32/32), 51.09 KiB | 670.00 KiB/s, done.
```
5. Перейдите в каталог с клоном репозитория (cd devops-netology).

6. Произведите первоначальную настройку Git, указав своё настоящее имя, чтобы нам было проще общаться, и email (git config --global user.name и git config --global user.email johndoe@example.com).
```
└─# git config -l
credential.helper=wincred
alias.c=config
user.email=chief.viper2012@yandex.ru
user.name=Vadim
core.repositoryformatversion=0
core.filemode=true
core.bare=false
core.logallrefupdates=true
remote.origin.url=https://github.com/V4d1M63/devops-netology.git
remote.origin.fetch=+refs/heads/*:refs/remotes/origin/*
branch.main.remote=origin
branch.main.merge=refs/heads/main
```
7. Выполните команду git status и запомните результат.

![2](https://github.com/V4d1M63/devops-netology/assets/130470784/1fc6f8e8-2108-43cb-a96c-4379f12437a0)

8. Отредактируйте файл README.md любым удобным способом, тем самым переведя файл в состояние Modified.

9. Ещё раз выполните git status и продолжайте проверять вывод этой команды после каждого следующего шага.

![3](https://github.com/V4d1M63/devops-netology/assets/130470784/884994ca-ab51-40ac-a10b-4f4b5ebcaef4)

10. Теперь посмотрите изменения в файле README.md, выполнив команды git diff и git diff --staged.

![4](https://github.com/V4d1M63/devops-netology/assets/130470784/506ace1c-a7a9-4ef5-8f77-66c2c5ea2f5e)

11. Переведите файл в состояние staged (или, как говорят, просто добавьте файл в коммит) командой git add README.md.
```
└─# git add README.md
```
12. И ещё раз выполните команды git diff и git diff --staged. Поиграйте с изменениями и этими командами, чтобы чётко понять, что и когда они отображают.

![5](https://github.com/V4d1M63/devops-netology/assets/130470784/c4a0892f-cf23-4bff-8ef4-3357ba6198a4)

13. Теперь можно сделать коммит git commit -m 'First commit'.

![6](https://github.com/V4d1M63/devops-netology/assets/130470784/62b1377d-44be-4f1f-949e-6d075452dae5)

14. И ещё раз посмотреть выводы команд git status, git diff и git diff --staged.

![7](https://github.com/V4d1M63/devops-netology/assets/130470784/3f8e416f-7ce7-491c-af55-6b26f074a3e6)

### Создание файлов .gitignore и второго коммита.

1. Создайте файл .gitignore (обратите внимание на точку в начале файла), проверьте его статус сразу после создания.
2. Добавьте файл .gitignore в следующий коммит (git add...).
3. На одном из следующих блоков вы будете изучать Terraform, давайте сразу создадим соотвествующий каталог terraform и внутри этого каталога — файл .gitignore по примеру: https://github.com/github/gitignore/blob/master/Terraform.gitignore.
4. В файле README.md опишите своими словами, какие файлы будут проигнорированы в будущем благодаря добавленному .gitignore.
5. Закоммитьте все новые и изменённые файлы. Комментарий к коммиту должен быть Added gitignore.

![8](https://github.com/V4d1M63/devops-netology/assets/130470784/cae1cd31-feea-4b51-b214-8316f8f468e1)

### Эксперимент с удалением и перемещением файлов (третий и четвёртый коммит).

1. Создайте файлы will_be_deleted.txt (с текстом will_be_deleted) и will_be_moved.txt (с текстом will_be_moved) и закоммите их с комментарием Prepare to delete and move.
```
# git commit -m 'Prepare to delete and move'
On branch main
Your branch is up to date with 'origin/main'.

Untracked files:
  (use "git add <file>..." to include in what will be committed)
        will_be_deleted.txt
        will_be_moved.txt

nothing added to commit but untracked files present (use "git add" to track)
```
2. В случае необходимости обратитесь к официальной документации — здесь подробно описано, как выполнить следующие шаги.
3. Удалите файл will_be_deleted.txt с диска и из репозитория.
```
# git rm will_be_deleted.txt
rm 'will_be_deleted.txt'

# git status
On branch main
Your branch is up to date with 'origin/main'.

Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
        deleted:    will_be_deleted.txt
```
4. Переименуйте (переместите) файл will_be_moved.txt на диске и в репозитории, чтобы он стал называться has_been_moved.txt.
```
# git mv will_be_moved.txt has_been_moved.txt

# git status
On branch main
Your branch is up to date with 'origin/main'.

Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
        renamed:    will_be_moved.txt -> has_been_moved.txt
```
5. Закоммитьте результат работы с комментарием Moved and deleted.
```
# git add .

# git commit -m 'Moved and deleted'
[main 4473d6f] Moved and deleted
 1 file changed, 0 insertions(+), 0 deletions(-)
 rename will_be_moved.txt => has_been_moved.txt (100%)

# git push
Enumerating objects: 3, done.
Counting objects: 100% (3/3), done.
Compressing objects: 100% (2/2), done.
Writing objects: 100% (2/2), 244 bytes | 244.00 KiB/s, done.
Total 2 (delta 1), reused 0 (delta 0), pack-reused 0
remote: Resolving deltas: 100% (1/1), completed with 1 local object.
To https://github.com/V4d1M63/devops-netology
   ebe246f..4473d6f  main -> main
```




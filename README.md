## Домашнее задание к занятию «Основы Git» - Вдовин Вадим
 
### Задание 1. Знакомимся с GitLab и Bitbucket

#### GitLab

Создадим аккаунт в GitLab, если у вас его ещё нет:

1. GitLab. Для регистрации можно использовать аккаунт Google, GitHub и другие.
2. После регистрации или авторизации в GitLab создайте новый проект, нажав на ссылку Create a projet. Желательно назвать также, как и в GitHub — devops-netology и visibility level, выбрать Public.
3. Галочку Initialize repository with a README лучше не ставить, чтобы не пришлось разрешать конфликты.
4. Если вы зарегистрировались при помощи аккаунта в другой системе и не указали пароль, то увидите сообщение: You won't be able to pull or push project code via HTTPS until you set a password on your account. Тогда перейдите по ссылке из этого сообщения и задайте пароль. Если вы уже умеете пользоваться SSH-ключами, то воспользуйтесь этой возможностью (подробнее про SSH мы поговорим в следующем учебном блоке).
5. Перейдите на страницу созданного вами репозитория, URL будет примерно такой: https://gitlab.com/YOUR_LOGIN/devops-netology. Изучите предлагаемые варианты для начала работы в репозитории в секции Command line instructions.
6. Запомните вывод команды git remote -v.
7. Из-за того, что это будет наш дополнительный репозиторий, ни один вариант из перечисленных в инструкции (на странице вновь созданного репозитория) нам не подходит. Поэтому добавляем этот репозиторий, как дополнительный remote, к созданному репозиторию в рамках предыдущего домашнего задания: git remote add gitlab https://gitlab.com/YOUR_LOGIN/devops-netology.git.
8. Отправьте изменения в новый удалённый репозиторий git push -u gitlab main.

![0](https://github.com/V4d1M63/devops-netology/assets/130470784/812b69c4-d74e-437f-a64c-aac703e3f5cc)

9. Обратите внимание, как изменился результат работы команды git remote -v.

Если всё проделано правильно, то результат команды git remote -v должен быть следующий:

![1](https://github.com/V4d1M63/devops-netology/assets/130470784/ee65cca9-89d2-473a-93b7-227a221d7b49)

Дополнительно можете добавить удалённые репозитории по ssh, тогда результат будет примерно такой:
```
# git remote -v                                                        
gitlab  https://gitlab.com/devops-netology6692835/visibility-level.git (fetch)
gitlab  https://gitlab.com/devops-netology6692835/visibility-level.git (push)
gitlab-ssh      git@gitlab.com:devops-netology6692835/visibility-level.git (fetch)
gitlab-ssh      git@gitlab.com:devops-netology6692835/visibility-level.git (push)
origin  https://github.com/v4d1m63/devops-netology.git (fetch)
origin  https://github.com/v4d1m63/devops-netology.git (push)
origin-ssh      git@github.com:v4d1m63/devops-netology.git (fetch)
origin-ssh      git@github.com:v4d1m63/devops-netology.git (push)
```
Выполните push локальной ветки main в новые репозитории.

Подсказка: git push -u gitlab main. На этом этапе история коммитов во всех трёх репозиториях должна совпадать.

### Задание 2. Теги

Представьте ситуацию, когда в коде была обнаружена ошибка — надо вернуться на предыдущую версию кода, исправить её и выложить исправленный код в продакшн. Мы никуда не будем выкладывать код, но пометим некоторые коммиты тегами и создадим от них ветки.

1. Создайте легковестный тег v0.0 на HEAD-коммите и запуште его во все три добавленных на предыдущем этапе upstream.

![2](https://github.com/V4d1M63/devops-netology/assets/130470784/42b100c8-6ba1-4b15-9bc7-d2b196fcdded)
                                                                                            
2. Аналогично создайте аннотированный тег v0.1.
![3](https://github.com/V4d1M63/devops-netology/assets/130470784/a8486654-6421-488f-a672-b01e667e06bc)

3. Перейдите на страницу просмотра тегов в GitHab (и в других репозиториях) и посмотрите, чем отличаются созданные теги.

![4](https://github.com/V4d1M63/devops-netology/assets/130470784/436829de-558c-4b4f-b7d4-7ca873b74467)

### Задание 3. Ветки

Давайте посмотрим, как будет выглядеть история коммитов при создании веток.

1. Переключитесь обратно на ветку main, которая должна быть связана с веткой main репозитория на github.
2. Посмотрите лог коммитов и найдите хеш коммита с названием Prepare to delete and move, который был создан в пределах предыдущего домашнего задания.

![5](https://github.com/V4d1M63/devops-netology/assets/130470784/ea141115-8e5c-468e-870e-3ebc994c8f58)

3. Выполните git checkout по хешу найденного коммита.

![6](https://github.com/V4d1M63/devops-netology/assets/130470784/96760fea-e5af-423f-9efa-9f0604acb6b5)

4. Создайте новую ветку fix, базируясь на этом коммите git switch -c fix.

![7](https://github.com/V4d1M63/devops-netology/assets/130470784/312ac8b2-9220-4b2b-9113-6d25d3d1e608)

5. Отправьте новую ветку в репозиторий на GitHub git push -u origin fix.
```
# git push -u origin fix
git: 'credential-wincred' is not a git command. See 'git --help'.
Username for 'https://github.com': v4d1m63
Password for 'https://v4d1m63@github.com': 
git: 'credential-wincred' is not a git command. See 'git --help'.
Total 0 (delta 0), reused 0 (delta 0), pack-reused 0
remote: 
remote: Create a pull request for 'fix' on GitHub by visiting:
remote:      https://github.com/v4d1m63/devops-netology/pull/new/fix
remote: 
To https://github.com/v4d1m63/devops-netology.git
 * [new branch]      fix -> fix
branch 'fix' set up to track 'origin/fix'.
```
6. Посмотрите, как визуально выглядит ваша схема коммитов: https://github.com/YOUR_ACCOUNT/devops-netology/network.

![8](https://github.com/V4d1M63/devops-netology/assets/130470784/a96d537e-ae77-45bd-b15e-7caf79c2c2dd)

7. Теперь измените содержание файла README.md, добавив новую строчку.
8. Отправьте изменения в репозиторий и посмотрите, как изменится схема на странице https://github.com/YOUR_ACCOUNT/devops-netology/network и как изменится вывод команды git log.

 ![9](https://github.com/V4d1M63/devops-netology/assets/130470784/e0060d91-9b04-4706-90ef-b4156fa4611a)

![10](https://github.com/V4d1M63/devops-netology/assets/130470784/01e3008a-7a15-44cf-840d-0f7fd458f9ce)


### Задание 4. Упрощаем себе жизнь

Попробуем поработь с Git при помощи визуального редактора.

1. В используемой IDE PyCharm откройте визуальный редактор работы с Git, находящийся в меню View -> Tool Windows -> Git.
2. Измените какой-нибудь файл, и он сразу появится на вкладке Local Changes, отсюда можно выполнить коммит, нажав на кнопку внизу этого диалога.

![git-5](https://github.com/V4d1M63/devops-netology/assets/130470784/ee9c433f-ac1a-48ec-b950-908e3d19969e)


3. Элементы управления для работы с Git будут выглядеть примерно так:
4. Попробуйте выполнить пару коммитов, используя IDE.

Если вверху экрана выбрать свою операционную систему, можно посмотреть горячие клавиши для работы с Git. Подробней о визуальном интерфейсе мы расскажем на одной из следующих лекций.

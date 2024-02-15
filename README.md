## Домашнее задание к занятию 7 «Жизненный цикл ПО» - Вдовин Вадим

### Подготовка к выполнению

1. Получить бесплатную версию Jira.
2. Настроить её для своей команды разработки.
3. Создать доски Kanban и Scrum.

### Основная часть

Необходимо создать собственные workflow для двух типов задач: bug и остальные типы задач. Задачи типа bug должны проходить жизненный цикл:

1. Open -> On reproduce.
2. On reproduce -> Open, Done reproduce.
3. Done reproduce -> On fix.
4. On fix -> On reproduce, Done fix.
5. Done fix -> On test.
6. On test -> On fix, Done.
7. Done -> Closed, Open.

![09-ci-01-intro-1](https://github.com/V4d1M63/devops-netology/assets/130470784/8cae1e92-0c3d-4da1-a1d6-71ab815f98ac)

Остальные задачи должны проходить по упрощённому workflow:

1. Open -> On develop.
2. On develop -> Open, Done develop.
3. Done develop -> On test.
4. On test -> On develop, Done.
5. Done -> Closed, Open.

![09-ci-01-intro-2](https://github.com/V4d1M63/devops-netology/assets/130470784/2f4cbf57-82c9-4fc8-86b2-ca3b9fa4eb09)

### Что нужно сделать

1. Создайте задачу с типом bug, попытайтесь провести его по всему workflow до Done.
2. Создайте задачу с типом epic, к ней привяжите несколько задач с типом task, проведите их по всему workflow до Done.
3. При проведении обеих задач по статусам используйте kanban.
4. Верните задачи в статус Open.
5. Перейдите в Scrum, запланируйте новый спринт, состоящий из задач эпика и одного бага, стартуйте спринт, проведите задачи до состояния Closed. Закройте спринт.

![09-ci-01-intro](https://github.com/V4d1M63/devops-netology/assets/130470784/e40b8eba-235b-4a77-957b-70f9e75bb1a8)

6. Если всё отработалось в рамках ожидания — выгрузите схемы workflow для импорта в XML. Файлы с workflow и скриншоты workflow приложите к решению задания.

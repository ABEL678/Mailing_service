# Mailing_service
1. Описание задач
Реализуйте интерфейс заполнения рассылок, то есть CRUD-механизм для управления рассылками.
Реализуйте скрипт рассылки, который работает как из командой строки, так и по расписанию.
Добавьте настройки конфигурации для периодического запуска задачи.
Сущности системы
Клиент сервиса:
контактный email,
ФИО,
комментарий.
Рассылка (настройки):
время рассылки;
периодичность: раз в день, раз в неделю, раз в месяц;
статус рассылки: завершена, создана, запущена.
Сообщение для рассылки:
тема письма,
тело письма.
Логи рассылки:
дата и время последней попытки;
статус попытки;
ответ почтового сервера, если он был.
Не забудьте про связи между сущностями. Вы можете расширять модели для сущностей в произвольном количестве полей либо добавлять вспомогательные модели.

2. Разработка сервиса
Контекст
Чтобы удержать текущих клиентов, часто используют вспомогательные, или «прогревающие», рассылки для информирования и привлечения клиентов.

Разработайте сервис управления рассылками, администрирования и получения статистики.

Описание задач
Реализуйте интерфейс заполнения рассылок, то есть CRUD-механизм для управления рассылками.
Реализуйте скрипт рассылки, который работает как из командой строки, так и по расписанию.
Добавьте настройки конфигурации для периодического запуска задачи.
Сущности системы
Клиент сервиса:
контактный email,
ФИО,
комментарий.
Рассылка (настройки):
время рассылки;
периодичность: раз в день, раз в неделю, раз в месяц;
статус рассылки: завершена, создана, запущена.
Сообщение для рассылки:
тема письма,
тело письма.
Логи рассылки:
дата и время последней попытки;
статус попытки;
ответ почтового сервера, если он был.
Не забудьте про связи между сущностями. Вы можете расширять модели для сущностей в произвольном количестве полей либо добавлять вспомогательные модели.

Логика работы системы
После создания новой рассылки, если текущее время больше времени начала и меньше времени окончания, то должны быть выбраны из справочника все клиенты, которые указаны в настройках рассылки, и запущена отправка для всех этих клиентов.
Если создается рассылка со временем старта в будущем, то отправка должна стартовать автоматически по наступлению этого времени без дополнительных действий со стороны пользователя системы.
По ходу отправки сообщений должна собираться статистика (см. описание сущности «сообщение» и «логи» выше) по каждому сообщению для последующего формирования отчетов.
Внешний сервис, который принимает отправляемые сообщения, может долго обрабатывать запрос, отвечать некорректными данными, на какое-то время вообще не принимать запросы. Нужна корректная обработка подобных ошибок. Проблемы с внешним сервисом не должны влиять на стабильность работы разрабатываемого сервиса рассылок.
‍Рекомендации

Реализовать интерфейс можно с помощью UI kit Bootstrap.
Для работы с периодическими задачами можно использовать либо crontab-задачи в чистом виде, либо изучить дополнительно библиотеку: https://pypi.org/project/django-crontab/
‍Периодические задачи — задачи, которые повторяются с определенной частотой, которая задается расписанием.

‍crontab — классический демон, который используется для периодического выполнения заданий в определенное время. Регулярные действия описываются инструкциями, помещенными в файлы crontab и в специальные каталоги.

Служба crontab не поддерживается в Windows, но может быть запущена через WSL. Поэтому если вы работаете на этой ОС, то решите задачу запуска периодических задач с помощью библиотеки apscheduler: https://pypi.org/project/django-apscheduler/.

Подробную информацию, что такое crontab-задачи, найдите самостоятельно.


2. Доработка сервиса
Контекст
Сервис по управлению рассылками пользуется популярностью, однако запущенный MVP уже не удовлетворяет потребностям бизнеса.

Доработайте ваше веб-приложение. А именно: разделите права доступа для различных пользователей и добавьте раздел блога для развития популярности сервиса в интернете.

Описание задач
Расширьте модель пользователя для регистрации по почте, а также верификации.
Добавьте интерфейс для входа, регистрации и подтверждения почтового ящика.
Реализуйте ограничение доступа к рассылкам для разных пользователей.
Реализуйте интерфейс менеджера.
Создайте блог для продвижения сервиса.
Используйте для наследования модель 
AbstractUser
.

Функционал менеджера
Может просматривать любые рассылки.
Может просматривать список пользователей сервиса.
Может блокировать пользователей сервиса.
Может отключать рассылки.
Не может редактировать рассылки.
Не может управлять списком рассылок.
Не может изменять рассылки и сообщения.
Функционал пользователя
Весь функционал дублируется из первой части курсовой работы. Но теперь нужно следить за тем, чтобы пользователь не мог случайным образом изменить чужую рассылку и мог работать только со своим списком клиентов и со своим списком рассылок.


Продвижение
Блог

Реализуйте приложение для ведения блога. При этом отдельный интерфейс реализовывать не требуется, но необходимо настроить административную панель для контент-менеджера.

В сущность блога добавьте следующие поля:

заголовок,
содержимое статьи,
изображение,
количество просмотров,
дата публикации.
Главная страница

Реализуйте главную страницу в произвольном формате, но обязательно отобразите следующую информацию:

количество рассылок всего,
количество активных рассылок,
количество уникальных клиентов для рассылок,
3 случайные статьи из блога.
Кеширование

Для блога и главной страницы самостоятельно выберите, какие данные необходимо кешировать, а также каким способом необходимо произвести кеширование.

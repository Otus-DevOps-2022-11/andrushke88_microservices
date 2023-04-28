# andrushke88_microservices
andrushke88 microservices repository
## ДЗ № 12 Технология контейнеризации. Введение в Docker
1. Создана ветка docker-2
2. Установка docker
3. Запуск первого контейнера(hello world)
4. Рассмотрены команды Docker ps, images, run, start, attach, exec, commit, kill, stop, system, rm, rmi
5. Дополнен файл log
6. Создан инстанс и поднят Docker-machine
7. Рассмотрено переключение между машинами докера(eval $(docker-machine env docker-host))
8. Повторена практика из лекции
9. Описан файл dockerfile и добавлены кофиги монги
10. Собран образ готового приложения и в последствии протестирован
11. Образ запушен в docker hub и позднее развёрнут на docker-machine
12. Изучены логи контейнера и рассмотрены предложенные команды

## ДЗ № 13 Docker-образы Микросервисы
1. Создание ветки docker-3
2. Подключение linterа к vscode
3. Подключение к docker-host
4. Wget и распаковка файлов в папку src
5. Создание docker файлов для всех сервисов с исправлением post-py dockerfile(добавлено обновление пипа)
6. Сброка образов сервисов и создание сети reddit
7. Запуск на docker-host - работает
8. Запуск с новыми алиасами например:
```console
docker run -d --network=reddit --network-alias=post_db1 --network-alias=comment_db mongo:latest
docker run -d --network=reddit --network-alias=post --env POST_DATABASE_HOST=post_db1 andrushke/post:1.0
docker run -d --network=reddit --network-alias=comment andrushke/comment:1.0
docker run -d --network=reddit -p 9292:9292 andrushke/ui:1.0
```
9 .Уменьшили размер образа ui и записали в файл Dockerfile.1(Alpine Linux)

## ДЗ № 14 Устройство Gitlab CI. Построение процесса непрерывной интеграции 
1. Cоздана машина с помощью packer образа с докером, в terraform созданы директории и докер файл. 
2. Были проблемы с root пользователем, исправил, вошёл в контейнер, запустил 
```console
gitlab-rails console -e production
user = User.where(id: 1).first
user.password = 'secret_pass' 
user.password_confirmation = 'secret_pass'
user.save
```
3. Создал простой playbook для развертывания Gitlab ansible-playbook-gitlab.yml
4. Отключил возможность регистрации
5. Создал группу и проект
6. Добавил remote в настройки репозитория 
```console
git remote add gitlab http:///homework/example.git 
git push gitlab gitlab-ci-1
```
7. Создал pipeline 
8. Добавил ранера для * Создал docker-compose для запука раннера docker-compose-gitlab_runner.yml 
9. Зарегистрировал раннера 
10. Проверил работу пайплайнов 
11. Добавил разные окружения 
12. Проверил работу с тегами и динамическими окружениями

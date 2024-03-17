## Команды Docker

### version

`docker version` - 
проверка версии, отображает cannot connect to docker daemon, если docker engine не запущен  

### run
`docker run hello-world` - скачивает образ *hello-world*, создает и запускает контейнер  
`docker run -i -t busybox` - запуск контейнера из образа *busybox* с флагами `-i` (`--interactive`), `-t` (`--tty`), можно использовать как `-it`  
`docker run -d nginx` - запуск контейнера с образом *nginx* в открепленном режиме `-d` (`--detach`)  
`docker run -d --name my_nginx nginx` - запускает контейнер с образом *nginx* с назначенным именем (`--name`) *my_nginx*  
`docker run -p 8080:80 nginx` - запускает контейнер с образом *nginx* и пробрасывает (`-p --publish`) порт *8080* хоста на порт *80* контейнера  
`docker run -v ${PWD}:/usr/share/nginx/html nginx` - запускает контейнер с образом *nginx* и подключает к нему (`-v --volume`) директорию хоста `${PWD}` (используется переменная окружения PWD (print working directory)) к директории контейнера `/usr/share/nginx/html`  
`docker run --rm bysybox` - запуск контейнера с образом `busybox` и автоматическое удаление его из списка контейнеров сразу после остановки (`--rm`)  
```bash
docker run \  
  --name my_nginx \  
  -v ${PWD}:/usr/share/nginx/html \  
  -p 8080:80 \  
  --rm \  
  nginx
```  
\- перенос длинных строк с помощью обратного слеша  

### ps

`docker ps -a`- отображает список контейнеров, флаг -a (all) отображает остановленные, по умолчанию только активные  

### images

`docker images` - отображает список локальных образов  

### pull

`docker pull hello-world` - скачивание образа *hello-world*  

### rm

`docker rm 7f15c7d50c2c` - удаление контейнера с id *7f15c7d50c2c* по ID или по имени  

### stop

`docker stop admiring_noyce` - остановка контейнера (по имени или ID) с именем *admiring_noyce*  

### container

`docker container prune` - удаляем все остановленные контейнеры  
`docker container inspect 8eae442c6fef` - информация о контейнере с id *8eae442c6fef*  

### exec

`docker exec -it 8eae442c6fef bash` - выполняет команду *bash* в запущенном контейнере с id *8eae442c6fef*  

### Создание образов

Пример Docker-файла:

``` docker
FROM python:alpine # На основе образа python:alpine

WORKDIR /my-app    # Рабочая директория внутри контейнера (создаёт и устаналивает как текущую)

COPY . .           # Копирование файлов из текущей директории в текущую директорию внутри контейнера (в данном случае WORKDIR)

CMD [ "python", "my_app.py" ] # Выполнение команд
```

`docker build . -t my-python-app` - создание образа из Docker-файла расположенного в текущей папке (по пути .) с названием `my-python-app`  
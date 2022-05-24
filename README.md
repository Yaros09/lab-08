#lab-08
#Данная лабораторная работа посвещена изучению систем автоматизации развёртывания и управления приложениями на примере Docker
1) Устанавливаем Docker c помощью
```
sudo snap install docker
sudo docker build -t logger 
```
![InkedСнимок экрана от 2022-05-23 21-04-54_LI](https://user-images.githubusercontent.com/91633974/169910687-a275a0d9-b941-4b08-8fae-a8fb600b2982.jpg)

2) Dockerfile:
```
FROM ubuntu:18.04

RUN apt update
RUN apt install -yy gcc g++ cmake

COPY . print/
WORKDIR print

RUN cmake -H. -B_build -DCMAKE_BUILD_TYPE=Release -DCMAKE_INSTALL_PREFIX=_install
RUN cmake --build _build
RUN cmake --build _build --target install

ENV LOG_PATH /home/logs/log.txt

ENV LOG_PATH /home/logs/log.txt


VOLUME /home/logs

WORKDIR _install/bin

ENTRYPOINT ./demo
```
![Снимок экрана от 2022-05-23 21-05-00](https://user-images.githubusercontent.com/91633974/169907344-c5490cfd-dfdd-40d8-b36c-3e1777b5091b.png)

![Снимок экрана от 2022-05-23 22-40-23](https://user-images.githubusercontent.com/91633974/169907959-f986661d-38d7-4af5-a75b-76c0da87bd21.png)

![Снимок экрана от 2022-05-23 23-48-49](https://user-images.githubusercontent.com/91633974/169908944-0b2b3f10-a85e-48d7-a4e8-3c647694deac.png)

Docker — это платформа, которая предназначена для разработки, развёртывания и запуска приложений в контейнерах.
Контейнер Docker — это образ Docker, вызванный к жизни. Это — самодостаточная операционная система, в которой имеется только самое необходимое и код приложения.
Образы Docker являются результатом процесса их сборки, а контейнеры Docker — это выполняющиеся образы.
В файлах Dockerfile содержатся инструкции по созданию образа. С них, набранных заглавными буквами, начинаются строки этого файла. После инструкций идут их аргументы. Инструкции, при сборке образа, обрабатываются сверху вниз.
Слои в итоговом образе создают только инструкции FROM, RUN, COPY, и ADD. Другие инструкции что-то настраивают, описывают метаданные, или сообщают Docker о том, что во время выполнения контейнера нужно что-то сделать, например — открыть какой-то порт или выполнить какую-то команду.

Основные инструкции Dockerfile:
1) FROM — задаёт базовый (родительский) образ.
2) LABEL — описывает метаданные. Например — сведения о том, кто создал и поддерживает образ.
3) ENV — устанавливает постоянные переменные среды.
4) RUN — выполняет команду и создаёт слой образа. Используется для установки в контейнер пакетов.
5) COPY — копирует в контейнер файлы и папки.
6) CMD — описывает команду с аргументами, которую нужно выполнить когда контейнер будет запущен. Аргументы могут быть переопределены при запуске контейнера. В файле может присутствовать лишь одна инструкция CMD.
7) WORKDIR — задаёт рабочую директорию для следующей инструкции.
8) ARG — задаёт переменные для передачи Docker во время сборки образа.
9) ENTRYPOINT — предоставляет команду с аргументами для вызова во время выполнения контейнера. Аргументы не переопределяются.
10) EXPOSE — указывает на необходимость открыть порт.
11) VOLUME — создаёт точку монтирования для работы с постоянным хранилищем.

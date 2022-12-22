# Подготовка
В этом проекте мы шаг за шагом настроим кластер Kubernetes, состоящий из трёх виртуальных машин c Ubuntu 20.04, а так же развернем еще однин Jenkins сервер и настроим CICD конвейер в наш кластер. В качестве хоста я использовал компьютер с Windows 10 Pro. В процессе настройки нам понадобятся:
- VirtualBox
- Vagrant
- Рабочая станция с 16 Gb ОЗУ

## _Настройка Kubernetes кластера на Vagrant_
В [репозитории](https://github.com/VVaritech/diplom.git) расположены скрипты и Vagrantfile. Выполните приведенные ниже действия, чтобы развернуть кластер Kubernetes и проверить все конфигурации кластера, а так же развернуть Jenkins сервер.
##### Шаг 1: Клонируйте репозиторий
```sh
git clone https://github.com/VVaritech/diplom.git
```
##### Шаг 2: Перейдите в клонированный каталог
```sh
cd diplom
```
##### Шаг 3: Выполните vagrant команду. Она развернет четыре узла. Один master и две worker-node и Jenkins сервер. Установка и настройка происходит через bash скрипты, присутствующие в папке scripts.
```sh
vagrant up
```
##### Шаг 4: После завершения установки войдите в master-node, чтобы проверить конфигурацию кластера.
```sh
# vagrant ssh master
# kubectl get nodes
```
##### Шаг 5: Проверка установки Jenkins
После установки Jenkins вы можете проверить установку jenkins, зайдя на начальную страницу входа в систему Jenkins.
http://localhost:8080/
И если все скрипты отработали корректно, мы сможем увидеть начальную страницу входа Jenkins
![Jenkins](https://miro.medium.com/max/990/1*-tuSyBfeKPx8Ng8aC2YGXA.jpeg)
##### Шаг 6: Настройка Jenkins
Получете стандартный пароль входа
```sh
cat /var/log/jenkins/jenkins.log
```
Настройте Jenkins и установите предложенный плагин
![Jenkins_start](https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcSb_Lk_8eltY3_NpDQyDyaw3Xngn2XE9W-8Zg&usqp=CAU)
В репозитории также находятся Jenkinsfile, Dockerfile и dedployment файлы для разворачивания конвейера CICD.
Чтобы завершить работу виртуальных машин, выполните команду:
```sh
vagrant halt
```
Чтобы удалить виртуальные машины:
```sh
vagrant destroy -f
```

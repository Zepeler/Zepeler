University: [ITMO University](https://itmo.ru/ru/)  
Faculty: [FICT](https://fict.itmo.ru)  
Course: [Introduction to distributed technologies](https://github.com/itmo-ict-faculty/introduction-to-distributed-technologies)  
Year: 2022/2023  
Group: K4113c    
Author: Zhelygin Daniil Yurievich 
Lab: Lab3  

# "Сертификаты и "секреты" в Minikube, безопасное хранение данных."
## Познакомиться с сертификатами и "секретами" в Minikube, правилами безопасного хранения данных в Minikube.
## Ход работы 
1. Cоздаю configMap с переменными: REACT_APP_USERNAME, REACT_APP_COMPANY_NAME
2. Создаем файл сервиса и ингресса и деплоймента и выполняем команду:
```
kubectl apply -f cm.yaml -f deploy.yaml -f service.yaml -f ingress.yaml    
```
<div align = "center"><img src="https://github.com/Zepeler/Zepeler/blob/main/Lr3/img/fail.png" ></div>
3. Включаем ingress

```
minikube addons enable ingress   
```

<div align = "center"><img src="https://github.com/Zepeler/Zepeler/blob/main/Lr3/img/ingress.png" ></div>
4. Устанавливаем ingress controller 

```
kubectl apply -f https://projectcontour.io/quickstart/contour.yaml
```  

<div align = "center"><img src="https://github.com/Zepeler/Zepeler/blob/main/Lr3/img/%D0%A1%D0%BD%D0%B8%D0%BC%D0%BE%D0%BA%20%D1%8D%D0%BA%D1%80%D0%B0%D0%BD%D0%B0%202022-11-19%20%D0%B2%2001.13.52.png" ></div>
5. Создаем тунель и вносим в hosts ip ингресс и домена 

```
minikube tunnel
```   

<div align = "center"><img src="https://github.com/Zepeler/Zepeler/blob/main/Lr3/img/%D1%82%D1%83%D0%BD%D0%B5%D0%BB%D1%8C.png" ></div>
6. Проверяем работоспособноть в браузере 
<div align = "center"><img src="https://github.com/Zepeler/Zepeler/blob/main/Lr3/img/%D1%82%D1%83%D0%BD%D0%B5%D0%BB%D1%8C%20%D1%80%D0%B0%D0%B1%D0%BE%D1%82%D0%B0%D0%B5%D1%82.png" ></div>
7. Создаем файлы tls.key и tls.crt и секре

```
openssl req -x509 -nodes -days 365 -newkey rsa:2048 -keyout tls.key -out tls.crt -subj "/CN=onetestexamle.com"
```
```
kubectl create secret tls test-tls --key="tls.key" --cert="tls.crt"
```

<div align = "center"><img src="https://github.com/Zepeler/Zepeler/blob/main/Lr3/img/%D0%A1%D0%BE%D0%B7%D0%B4%D0%B0%D0%BD%D0%B8%D0%B5%20TLS.png" ></div>
<div align = "center"><img src="https://github.com/Zepeler/Zepeler/blob/main/Lr3/img/%D0%A1%D0%BD%D0%B8%D0%BC%D0%BE%D0%BA%20%D1%8D%D0%BA%D1%80%D0%B0%D0%BD%D0%B0%202022-11-19%20%D0%B2%2001.20.02.png" ></div>
8. Добавляем имя секрета и поле hosts

```
curl --cacert tls.crt https://onetestexamle.com  
```

<div align = "center"><img src="https://github.com/Zepeler/Zepeler/blob/main/Lr3/img/%D0%A1%D0%BD%D0%B8%D0%BC%D0%BE%D0%BA%20%D1%8D%D0%BA%D1%80%D0%B0%D0%BD%D0%B0%202022-11-19%20%D0%B2%2001.21.42.png" ></div>
## Схема 
<div align = "center"><img src="https://github.com/Zepeler/Zepeler/blob/main/shema1.2.png" ></div>

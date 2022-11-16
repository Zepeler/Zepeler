University: [ITMO University](https://itmo.ru/ru/)  
Faculty: [FICT](https://fict.itmo.ru)  
Course: [Introduction to distributed technologies](https://github.com/itmo-ict-faculty/introduction-to-distributed-technologies)  
Year: 2022/2023  
Group: K4113c    
Author: Zhelygin Daniil Yurievich 
Lab: Laba2 

# Развертывание веб сервиса в Minikube, доступ к веб интерфейсу сервиса. Мониторинг
##Цель работы
Ознакомиться с типами "контроллеров" развертывания контейнеров, ознакомится с сетевыми сервисами и развернуть свое веб приложение.
## Ход работы 
1. Cоздать deployment с 2 репликами

```
kubectl apply -f deploy.yaml
```  
```
kubectl apply -f service.yaml
```  
2. Просматриваем созданные сервисы
 ```
kubectl get service
```   
3. подключаемся к контейнерам через браузер
 ```
mkubectl port-forward svc/indfr-service 80:80
```
# Схема 
<div align = "center"><img src="https://github.com/Zepeler/Zepeler/blob/main/shema1.2.png" ></div>

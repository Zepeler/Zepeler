University: [ITMO University](https://itmo.ru/ru/)  
Faculty: [FICT](https://fict.itmo.ru)  
Course: [Introduction to distributed technologies](https://github.com/itmo-ict-faculty/introduction-to-distributed-technologies)  
Year: 2022/2023  
Group: K4113c    
Author: Zhelygin Daniil Yurievich 
Lab: Lab1  

# Создание манифеста  
## Ход работы 
1. Устанавливаю Docker на рабочий компьютер
2. Устаноавливаю Minikube используя оригинальную инструкцию
3. Создаем файл манифеста, где указываем образ `vault`  
4. Создаем под с помощью команды 
```
kubectl apply -f pod.ymal
```  
5. Посмотреть информацию о поде: 
 ```
kubectl get pods
```   
6. Создаем сервис 
 ```
minikube kubectl -- expose pod vault --type=NodePort --port=8200
```
7. Прокидываем порт для доступа к сервису 
 ```
minikube kubectl -- port-forward service/vault 8200:8200
```
## Схема 
<div align = "center"><img src="https://github.com/Zepeler/Zepeler/blob/main/shema1.2.png" ></div>

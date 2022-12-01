University: [ITMO University](https://itmo.ru/ru/)  
Faculty: [FICT](https://fict.itmo.ru)  
Course: [Introduction to distributed technologies](https://github.com/itmo-ict-faculty/introduction-to-distributed-technologies)  
Year: 2022/2023  
Group: K4113c    
Author: Zhelygin Daniil Yurievich                                                                               
Lab: Lab4  


# "Сети связи в Minikube, CNI и CoreDNS""
## Познакомиться с CNI Calico и функцией IPAM Plugin, изучить особенности работы CNI и CoreDNS.
## Ход работы 
1. При запуске minikube установите плагин CNI=calico и режим работы Multi-Node Clusters одновеременно развернуть 2 ноды.

<div align = "center"><img src="https://github.com/Zepeler/Zepeler/blob/main/Lr4/img/%D0%A1%D0%BD%D0%B8%D0%BC%D0%BE%D0%BA%20%D1%8D%D0%BA%D1%80%D0%B0%D0%BD%D0%B0%202022-11-24%20%D0%B2%2021.25.52.png" ></div>

2. Устанавливаем calicoctl 
```
kkubectl apply -f calicoctl.yaml  
```
<div align = "center"><img src="https://github.com/Zepeler/Zepeler/blob/main/Lr4/img/%D0%A1%D0%BD%D0%B8%D0%BC%D0%BE%D0%BA%20%D1%8D%D0%BA%D1%80%D0%B0%D0%BD%D0%B0%202022-11-26%20%D0%B2%2018.02.27.png" ></div>
3. Создаем манфест ippool, где мы видим, существует один пул ipv4 по умолчанию

```
kubectl exec -i -n kube-system calicoctl -- /calicoctl get ippools -o wide 
```

<div align = "center"><img src="https://github.com/Zepeler/Zepeler/blob/main/Lr4/img/%D0%A1%D0%BD%D0%B8%D0%BC%D0%BE%D0%BA%20%D1%8D%D0%BA%D1%80%D0%B0%D0%BD%D0%B0%202022-11-26%20%D0%B2%2018.02.18.png" ></div>
4. В результате создаем 2 ippool

```
kubectl exec -i -n kube-system calicoctl -- /calicoctl create -f - < ippool.yaml 
```  

<div align = "center"><img src="https://github.com/Zepeler/Zepeler/blob/main/Lr4/img/%D0%A1%D0%BD%D0%B8%D0%BC%D0%BE%D0%BA%20%D1%8D%D0%BA%D1%80%D0%B0%D0%BD%D0%B0%202022-11-26%20%D0%B2%2018.02.04.png" ></div>

<div align = "center"><img src="https://github.com/Zepeler/Zepeler/blob/main/Lr4/img/%D0%A1%D0%BD%D0%B8%D0%BC%D0%BE%D0%BA%20%D1%8D%D0%BA%D1%80%D0%B0%D0%BD%D0%B0%202022-11-26%20%D0%B2%2018.01.26.png" ></div>
5. Pапукаем деплоймент, конфигмап и сервес 

```
kubectl apply -f cm.yaml -f deploy.yaml -f service.yaml
```   

<div align = "center"><img src="https://github.com/Zepeler/Zepeler/blob/main/Lr4/img/%D0%A1%D0%BD%D0%B8%D0%BC%D0%BE%D0%BA%20%D1%8D%D0%BA%D1%80%D0%B0%D0%BD%D0%B0%202022-11-26%20%D0%B2%2018.00.51.png" ></div>
<div align = "center"><img src="https://github.com/Zepeler/Zepeler/blob/main/Lr4/img/%D0%A1%D0%BD%D0%B8%D0%BC%D0%BE%D0%BA%20%D1%8D%D0%BA%D1%80%D0%B0%D0%BD%D0%B0%202022-11-26%20%D0%B2%2018.00.27.png" ></div>
6. Проверяем работоспособноть в браузере 


<div align = "center"><img src="https://github.com/Zepeler/Zepeler/blob/main/Lr4/img/%D0%A1%D0%BD%D0%B8%D0%BC%D0%BE%D0%BA%20%D1%8D%D0%BA%D1%80%D0%B0%D0%BD%D0%B0%202022-11-26%20%D0%B2%2017.43.39.png" ></div>

<div align = "center"><img src="hhttps://github.com/Zepeler/Zepeler/blob/main/Lr4/img/%D0%A1%D0%BD%D0%B8%D0%BC%D0%BE%D0%BA%20%D1%8D%D0%BA%D1%80%D0%B0%D0%BD%D0%B0%202022-11-26%20%D0%B2%2017.43.39.png" ></div>
7. Проверяем пинг


<div align = "center"><img src="https://github.com/Zepeler/Zepeler/blob/main/Lr4/img/%D0%A1%D0%BD%D0%B8%D0%BC%D0%BE%D0%BA%20%D1%8D%D0%BA%D1%80%D0%B0%D0%BD%D0%B0%202022-11-26%20%D0%B2%2017.59.36.png" ></div>

## Схема 

<div align = "https://github.com/Zepeler/Zepeler/blob/main/Lr4/img/%D0%A1%D0%BD%D0%B8%D0%BC%D0%BE%D0%BA%20%D1%8D%D0%BA%D1%80%D0%B0%D0%BD%D0%B0%202022-12-01%20%D0%B2%2016.53.30.png" ></div>

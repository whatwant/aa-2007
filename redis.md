### pod 셋팅
```
$ kubectl apply -f redis_deployment.yaml
$ kubectl apply -f redis_service.yaml
```

### docker build
```
$ docker build -t count:v4 -f dockerfile3 ./
```

### image update
```
$ kubectl set image deployments/count count=count:v4
```

### service 등록
```
$ kubectl expose deployment count --port=8080 --type=LoadBalancer
$ minikube service count
```
- check
```
$ curl http://172.17.0.3:31556/
```

### slave 구성
- tutorial p141 참고

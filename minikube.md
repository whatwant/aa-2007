
### kubectl
- install
```
$ curl -LO https://storage.googleapis.com/kubernetes-release/release/`curl -s https://storage.googleapis.com/kubernetes-release/release/stable.txt`/bin/linux/amd64/kubectl
$ chmod +x ./kubectl
$
```
- check
```
$ kubectl version --client
$ kubectl cluster-info
$ kubectl get node
```

### server
- tutorials/kubernetes/server1.js
- run
```
$ node ./server1.js
```
- check
```
http://localhost:8080/
```

### minikube & docker
- docker 환경 설정 (minikube와 docker의 연결?)
```
$ docker images
$ minikube docker-env
$ eval $(minikube -p minikube docker-env)
$ docker images
```
- docker build
```
$ cd map-ui/tutorials/kubernetes
$ docker build -t hostname:v1 -f dockerfile1 ./
```
- check (hostname이라는 이름으로 version1)
```
$ docker images
```
- pod 생성
```
$ kubectl run hostname --image=hostname:v1 --port=8080 --image-pull-policy=Never
```
- dashboard에서 확인
  - 오른쪽 ...에서 Exec 선택하면 터미널 접근
- 서비스 노출시키기
```
$ kubectl expose pod hostname --type=LoadBalancer
```
- dashboard에서 서비스로 보임
- 서비스 포트 확인(연결)
```
$ minikube service hostname
```
- pod 삭제하기
```
$kubectl delete -n default pod hostname
```
- service 삭제하기
```
$ kubectl delete -n default service hostname
```
- deployment 만들기
```
$ kubectl create deployment hostname --image=hostname:v1
```
- 오른쪽 ...의 스케일을 통해 pod 숫자 조정 가능
- service 생성
```
$ kubectl expose deployment hostname --port=8080 --type=LoadBalancer
$ minikube service hostname
```
- hostname 바뀌는거 확인

### minikube yaml
- dashboard의 오른쪽 ...에서 편집 부분을 봐도 확인 가능함
- deployment, service 각각 따로 취급

### persistent volume 만들기
```
$ cd ./map-ui/tutorials/kubernetes
$ docker build -t count:v3 -f dockerfile2 ./
$ kubectl apply -f server2_deployment.yaml
```
- count pod의 Exec 실행 후 *df -h* 해보면 */dev/sda1* 추가 된걸 볼 수 있다

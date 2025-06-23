# Kubernetes'te Medusa

Bu proje MedusaJS e-ticaret uygulamalarını deploy etmek için bir Kubernetes başlangıç kitidir. tural-musab tarafından fork edilmiş ve özelleştirilmiştir.

## Önkoşullar

- Kubernetes cluster (geliştirme amaçlı tercihen Minikube)
- Node v22
- Yarn v4.7.0 (Corepack ile etkinleştirebilmelisiniz)

## Image Oluşturma

Sonraki adımlara geçmeden önce image'ı oluşturmalısınız.

```bash
cd my-medusa-store
yarn build
docker build -t medusa-store:latest .
```

## Kaynaklarınızı K8s Cluster'a Deploy Etme

Kaynaklarınızı kolay temizlik için izole etmek amacıyla bir namespace oluşturmalı ve image'ı yüklemelisiniz.

```bash
minikube image load medusa-store:latest
kubectl create namespace medusa
cd kubernetes
kubectl apply -f . -n medusa
```

## Medusa Instance'ına Erişim

Tüm kaynaklarınızı cluster'a yükledikten sonra, load balancer'a bir tünel oluşturmak için Minikube'u kullanabilirsiniz. Admin dashboard'a erişim için HTTPS kullanmak amacıyla [ngrok](https://ngrok.com) kullanmanız önerilir.

```bash
minikube tunnel 127.0.0.1
# Ayrı bir terminal'de aşağıdaki komutu çalıştırabilirsiniz
ngrok http 80
```
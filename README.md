# Prova 2 de Computação em Nuvem

Instituição: Anhanguera
Disciplina: Computação em Nuvem
Professora: Simone Tatiane Do Canto
Data: 18/11/2026
Aluno: Gabriel Ribeiro de Oliveira



# Questão 1

Resposta: A diferença é na responsabilidade e no parametro/nivel de controle que vai exercer diante uma tecnologia. um exemplo de utilização do modelo iaas e saas são:  
SaaS: Google Workspace
IaaS: Modelo servidor nuvem

# Questão 2

Resposta: Nuvem híbrida combinação de servidores próprios 
(nuvem privada) com serviços de um provedor de nuvem pública.

# Questão 3

Resposta: uma máquina virtual (VM) virtualiza o hardware e roda um sistema operacional completo próprio, enquanto um container virtualiza o nível do sistema operaciona


# EVIDENCIAS

 DOCKER
 
 # Evidência 1 - 

root@controlplane:~$ docker ps
CONTAINER ID   IMAGE          COMMAND                  CREATED         STATUS         PORTS                                     NAMES
a55d6706e158   nginx:alpine   "/docker-entrypoint.…"   3 seconds ago   Up 3 seconds   0.0.0.0:8090->80/tcp, [::]:8090->80/tcp   comunicado-web

# Evidência 2

root@controlplane:~$ curl http://localhost:8090
<!DOCTYPE html>
<html>
<head>
<title>Welcome to nginx!</title>
<style>
html { color-scheme: light dark; }
body { width: 35em; margin: 0 auto;
font-family: Tahoma, Verdana, Arial, sans-serif; }
</style>
</head>
<body>
<h1>Welcome to nginx!</h1>
<p>If you see this page, nginx is successfully installed and working.
Further configuration is required for the web server, reverse proxy, 
API gateway, load balancer, content cache, or other features.</p>

<p>For online documentation and support please refer to
<a href="https://nginx.org/">nginx.org</a>.<br/>
To engage with the community please visit
<a href="https://community.nginx.org/">community.nginx.org</a>.<br/>
For enterprise grade support, professional services, additional 
security features and capabilities please refer to
<a href="https://f5.com/nginx">f5.com/nginx</a>.</p>

<p><em>Thank you for using nginx.</em></p>
</body>
</html>

# Evidência 3

root@controlplane:~$ kubectl get nodes
NAME           STATUS   ROLES           AGE   VERSION
controlplane   Ready    control-plane   13d   v1.37.1
node01         Ready    <none>          13d   v1.37.1

# Evidência 4 

kubectl scale deployment comunicado-web --replicas=3
deployment.apps/comunicado-web scaled

kubectl get pods
NAME                              READY   STATUS    RESTARTS   AGE
comunicado-web-57c76f7bc4-259hw   1/1     Running   0          21s
comunicado-web-57c76f7bc4-nqw42   1/1     Running   0          21s
comunicado-web-57c76f7bc4-xvqk2   1/1     Running   0          87s

#Evidencia 5


root@controlplane:~$ kubectl delete pod comunicado-web-57c76f7bc4-259hw
pod "comunicado-web-57c76f7bc4-259hw" deleted from default namespace
root@controlplane:~$ kubectl get pods
NAME                              READY   STATUS    RESTARTS   AGE
comunicado-web-57c76f7bc4-nqw42   1/1     Running   0          3m22s
comunicado-web-57c76f7bc4-xllvs   1/1     Running   0          11s
comunicado-web-57c76f7bc4-xvqk2   1/1     Running   0          4m28s

# Evidência 6 

root@controlplane:~$ kubectl get services 
NAME         TYPE        CLUSTER-IP   EXTERNAL-IP   PORT(S)   AGE
kubernetes   ClusterIP   10.96.0.1    <none>        443/TCP   13d


root@controlplane:~$ kubectl run teste --image=curlimages/curl --rm -it --restart=Never -- curl http://comunicado-service 
<!DOCTYPE html>
<html>
<head>
<title>Welcome to nginx!</title>
<style>
html { color-scheme: light dark; }
body { width: 35em; margin: 0 auto;
font-family: Tahoma, Verdana, Arial, sans-serif; }
</style>
</head>
<body>
<h1>Welcome to nginx!</h1>
<p>If you see this page, nginx is successfully installed and working.
Further configuration is required for the web server, reverse proxy, 
API gateway, load balancer, content cache, or other features.</p>

<p>For online documentation and support please refer to
<a href="https://nginx.org/">nginx.org</a>.<br/>
To engage with the community please visit
<a href="https://community.nginx.org/">community.nginx.org</a>.<br/>
For enterprise grade support, professional services, additional 
security features and capabilities please refer to
<a href="https://f5.com/nginx">f5.com/nginx</a>.</p>

<p><em>Thank you for using nginx.</em></p>
</body>
</html>
All commands and output from this session will be recorded in container logs, including credentials and sensitive information passed through the command prompt.
If you don't see a command prompt, try pressing enter.
warning: couldn't attach to pod/teste, falling back to streaming logs: unable to upgrade connection: container teste not found in pod teste_default
<!DOCTYPE html>
<html>
<head>
<title>Welcome to nginx!</title>
<style>
html { color-scheme: light dark; }
body { width: 35em; margin: 0 auto;
font-family: Tahoma, Verdana, Arial, sans-serif; }
</style>
</head>
<body>
<h1>Welcome to nginx!</h1>
<p>If you see this page, nginx is successfully installed and working.
Further configuration is required for the web server, reverse proxy, 
API gateway, load balancer, content cache, or other features.</p>

<p>For online documentation and support please refer to
<a href="https://nginx.org/">nginx.org</a>.<br/>
To engage with the community please visit
<a href="https://community.nginx.org/">community.nginx.org</a>.<br/>
For enterprise grade support, professional services, additional 
security features and capabilities please refer to
<a href="https://f5.com/nginx">f5.com/nginx</a>.</p>

<p><em>Thank you for using nginx.</em></p>
</body>
</html>
pod "teste" deleted from default namespace

# Interpretação dos resultados 

# QUESTÃO 1 RESPOSTA:

A imagem Docker é o modelo estático e somente leitura com o código e as dependências, enquanto o container em execução é a instância ativa que roda essa imagem na máquina

# QUESTÃO 2 RESPOSTA:

O Deployment gerencia os Pods, garantindo que a aplicação esteja rodando na quantidade e versão desejadas.

# QUESTÃO 3 RESPOSTA:

Ao excluir um Pod, o Deployment criou outro automaticamente para manter a quantidade de réplicas desejada. Isso acontece porque ele monitora e mantém os Pods em execução.

# QUESTÃO 4 RESPOSTA:
Service no Kubernetes serve para expor e permitir a comunicação com um conjunto de Pods, fornecendo um endereço IP e DNS estáveis, mesmo que os Pods sejam recriados ou alterem seus IPs.

Resumindo: o Service garante uma forma estável de acessar os Pods e distribui o tráfego entre eles.

## CONCLUSÃO:

Aprendi com a aula pratica a excluir um pod e com isso aumentar a quantidade de replicas, aprendi a criar service e verificar como é a comunição http do cluster Kubernetes, aprendi a diferença entre uma imagem docker e um container.

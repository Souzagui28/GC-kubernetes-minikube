# Projeto Kubernetes Básico: Webapp e MongoDB (Gerência de Configuração)

Este projeto demonstra uma implantação simples no Kubernetes de uma aplicação web interagindo com um banco de dados MongoDB. Foi desenvolvido como parte da disciplina de **Gerência de Configuração**, do 7º período de Engenharia de Software.

**Objetivo:** Este é um exercício de primeiro contato com o Kubernetes, focado em entender a orquestração de contêineres e a comunicação entre Deployments e Services.

## 📚 Referência

Todo o código-fonte e a base deste projeto foram copiados da aula da **Professora Nana (TechWorld with Nana)**, disponível no seguinte vídeo:

  * [Link para o vídeo da aula](https://youtu.be/s_o8dwzRlu4)

## 📖 Documentação Útil

Para aprofundar seus conhecimentos e entender melhor os conceitos utilizados neste projeto, consulte as seguintes documentações:

  * **Minikube:**
      * [Documentação Oficial do Minikube](https://minikube.sigs.k8s.io/docs/)
      * [Drivers do Minikube](https://minikube.sigs.k8s.io/docs/drivers/)
  * **Docker:**
      * [Imagem Oficial do MongoDB no Docker Hub](https://hub.docker.com/_/mongo)
  * **Kubernetes:**
      * [Documentação Oficial do Kubernetes](https://kubernetes.io/docs/home/)
      * [Conceitos de Secrets](https://kubernetes.io/docs/concepts/configuration/secret/)
      * [Conceitos de ConfigMaps](https://kubernetes.io/docs/concepts/configuration/configmap/)
      * [Conceitos de Services](https://kubernetes.io/docs/concepts/services-networking/service/)
      * [Conceitos de Deployments](https://kubernetes.io/docs/concepts/workloads/controllers/deployment/)

## 🚀 Pré-requisitos

Certifique-se de ter instalado:

  * **Docker Desktop:** Para rodar o Minikube.
  * **Minikube:** Para criar um cluster Kubernetes local.
  * **kubectl:** Para interagir com o cluster.

## ⚙️ Configuração e Execução

### 1\. Iniciar o Minikube

Abra seu terminal e inicie o Minikube:

```bash
minikube start --driver=docker
```

### 2\. Implantar os Recursos

Este projeto utiliza quatro arquivos YAML principais, cujos códigos foram fornecidos na aula da Professora Nana:

  * `mongo-config.yaml`: Define configurações para o MongoDB, como a URL de conexão.
  * `mongo-secret.yaml`: Configura as credenciais de acesso ao MongoDB (usuário e senha).
  * `mongo.yaml`: Implanta o banco de dados MongoDB e seu Service interno.
  * `webapp.yaml`: Implanta a aplicação web e seu Service externo.

Aplique todos os arquivos na ordem:

```bash
kubectl apply -f mongo-config.yaml
kubectl apply -f mongo-secret.yaml
kubectl apply -f mongo.yaml
kubectl apply -f webapp.yaml
```

### 3\. Verificar o Status

Confira se todos os componentes estão rodando:

```bash
kubectl get all
```

Você deve ver os pods do MongoDB e da aplicação web em status `Running`.

## 🌐 Acessando a Aplicação

Para acessar a aplicação web no seu navegador, utilize o comando `minikube service`:

```bash
minikube service webapp-service
```

Este comando irá abrir automaticamente a URL da aplicação em seu navegador padrão.


## 🗑️ Limpeza dos Recursos

Para remover todos os recursos implantados:

```bash
kubectl delete -f webapp.yaml
kubectl delete -f mongo.yaml
kubectl delete -f mongo-config.yaml
kubectl delete -f mongo-secret.yaml
```

Para uma limpeza completa do Minikube (reinicia o ambiente do zero):

```bash
minikube stop
minikube delete
minikube start --driver=docker
```
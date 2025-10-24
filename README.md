# Repositório de Manifestos (GitOps) - Aplicação FastAPI

Este repositório contém os **manifestos Kubernetes** que definem o estado desejado da nossa aplicação FastAPI no cluster. Ele serve como a **Fonte Única da Verdade** para o nosso pipeline de GitOps.

---

⚠️ **Atenção: Repositório Gerenciado Automaticamente** ⚠️  
**NÃO FAÇA EDITS MANUAIS DIRETAMENTE NESTE REPOSITÓRIO.**

Este repositório é gerenciado pelo pipeline de CI/CD configurado no `Projeto-CI`. Mudanças manuais serão sobrescritas pela automação e podem causar inconsistências de estado.

---

## 🎯 Propósito

O objetivo deste repositório é **descrever declarativamente** o que deve estar rodando no Kubernetes.  
A ferramenta de **Entrega Contínua (ArgoCD)** é responsável por ler este repositório e garantir que o estado do cluster seja idêntico ao que está definido aqui.

---

## 🛠️ Ferramentas

- **ArgoCD**: Monitora este repositório e sincroniza automaticamente qualquer mudança com o cluster Kubernetes.

---

## 📁 Estrutura de Arquivos

/k8s
 ├─ deployment.yaml # Define como a aplicação deve ser executada (réplicas, imagem Docker, etc.)
 ├─ service.yaml # Define como a aplicação é exposta (NodePort, LoadBalancer, etc.)


- **deployment.yaml**: A `image: tag` neste arquivo é atualizada automaticamente pelo CI.  
- **service.yaml**: Configura o acesso à aplicação no cluster.

---

## 🔄 Fluxo de Trabalho (GitOps)

1. Um desenvolvedor faz **push de código** no repositório `Projeto-CI`.
2. O **GitHub Actions** é acionado, constrói e publica uma nova imagem Docker  
   Ex: `gianpedro/fastapi-app:hash-do-commit`.
3. O GitHub Actions clona este repositório (`Projeto-CD`), atualiza o arquivo `k8s/deployment.yaml` com a nova tag da imagem e realiza um **commit automático**.
4. O **ArgoCD**, monitorando este repositório, detecta o novo commit.
5. O ArgoCD aplica as mudanças no cluster Kubernetes, realizando um **rolling update** para a nova versão da aplicação.

---

## 🔗 Repositórios Relacionados

- **Repositório da Aplicação (CI)**: [https://github.com/gianpedrobc/Projeto_CI](https://github.com/gianpedrobc/Projeto_CI)

- **Repositório do DockerHub**: [https://hub.docker.com/repository/docker/gianpedro/fastapi-app/general](https://hub.docker.com/repository/docker/gianpedro/fastapi-app/general)



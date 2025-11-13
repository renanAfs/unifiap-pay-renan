# Desafio UniFIAP Pay SPB# Desafio UniFIAP Pay SPB# Desafio UniFIAP Pay SPB# Desafio UniFIAP Pay SPB# 🚀 UniFIAP Pay SPB - Sistema de Pagamentos Instantâneos# 🚀 PROJETO COMPLETO 100%



## Dados do Aluno



**Nome:** Renan Assi de Freitas  ![Status](https://img.shields.io/badge/status-active-success.svg)

**RM:** 93744  

**Docker Hub:** renanafs  ![Kubernetes](https://img.shields.io/badge/kubernetes-v1.33-blue.svg)

**Pontuação Total:** 9,0 pts

![Rancher](https://img.shields.io/badge/rancher-v2.12.3-green.svg)![Status](https://img.shields.io/badge/status-active-success.svg)

---

![Python](https://img.shields.io/badge/python-3.11-blue.svg)

## 1. Arquitetura da Solução e Contexto SPB

![Docker](https://img.shields.io/badge/docker-latest-blue.svg)![Kubernetes](https://img.shields.io/badge/kubernetes-v1.33-blue.svg)

### 1.1. Descrição do Projeto



Sistema de pagamentos PIX seguindo as regras do **SPB (Sistema de Pagamentos Brasileiro)** com arquitetura de microsserviços Cloud Native.

## Dados do Aluno![Rancher](https://img.shields.io/badge/rancher-v2.12.3-green.svg)![Status](https://img.shields.io/badge/status-active-success.svg)

**Pilares do Desafio:**

1. **Segurança** - Containers e redes isoladas

2. **Orquestração** - Kubernetes para gerenciar a aplicação em escala

3. **Regras de Negócio** - Reserva Bancária e Liquidação**Nome:** Renan Assi de Freitas  ![Python](https://img.shields.io/badge/python-3.11-blue.svg)



### 1.2. Papéis e Responsabilidades dos Microsserviços (Fluxo SPB)**RM:** 93744  



| Microsserviço | Função Principal (Papel no SPB) | Responsabilidades de Código |**Docker Hub:** renanafs  ![Docker](https://img.shields.io/badge/docker-latest-blue.svg)![Kubernetes](https://img.shields.io/badge/kubernetes-v1.33-blue.svg)

|---------------|----------------------------------|------------------------------|

| **api-pagamentos** | Banco Originador (UniFIAP Pay) | 1. **Ler Saldo:** Consultar `RESERVA_BANCARIA_SALDO`<br>2. **Pré-Validar:** SE Valor PIX <= RESERVA_BANCARIA_SALDO<br>3. **Registrar:** Escrever no arquivo `/var/logs/api/instrucoes.log` com status `AGUARDANDO_LIQUIDACAO` |**Total de Pontos:** 9,0 pts

| **auditoria-service** | Sistema de Liquidação (BACEN/STR) | 1. **Monitorar:** Ler `/var/logs/api/instrucoes.log`<br>2. **Liquidação:** Atualizar status para `LIQUIDADO`<br>3. **Automação:** Executar a cada 15 segundos |

| **frontend-pix** | Interface do Usuário | Formulário web para transações PIX |



### 1.3. Diagrama de Arquitetura---



**Componentes:**## Dados do Aluno![Rancher](https://img.shields.io/badge/rancher-v2.12.3-green.svg)![Status](https://img.shields.io/badge/status-active-success.svg)

- **Kubernetes** (Docker Desktop) - Orquestração

- **Rancher v2.12.3** - Gerenciamento visual (https://localhost:8443)## 📋 Índice

- **PersistentVolume** - `/var/logs/api/instrucoes.log` (Livro-Razão compartilhado)

- **ConfigMap** - `RESERVA_BANCARIA_SALDO=1000000.00`

- **Prometheus + Grafana** - Monitoramento

- **Kube-state-metrics** - Métricas do Kubernetes1. [Arquitetura da Solução](#1-arquitetura-da-solução)



---2. [Instalação Completa](#2-instalação-completa)**Nome:** Renan Assi de Freitas  ![Python](https://img.shields.io/badge/python-3.11-blue.svg)



## 2. Passos de Execução3. [Evidências e Resultados](#3-evidências-e-resultados)



### 2.1. Configuração Local (Docker)4. [Comandos de Validação](#4-comandos-de-validação)**RM:** 93744  



#### Criar Rede Docker Segmentada5. [Troubleshooting](#5-troubleshooting)



```powershell**Total de Pontos:** 9,0 pts![Docker](https://img.shields.io/badge/docker-latest-blue.svg)![Kubernetes](https://img.shields.io/badge/kubernetes-v1.33-blue.svg)

docker network create --driver bridge --subnet 172.25.0.0/24 unifiap_net

```---



### 2.2. Build e Publicação das Imagens (v1.93744)



#### Build com Multi-Stage## 1. Arquitetura da Solução



```powershell---

cd core/api-pagamentos

docker build -t renanafs/unifiap-api-pagamentos:v1.93744 .### 1.1. Descrição



cd ../auditoria-service

docker build -t renanafs/unifiap-auditoria:v1.93744 .

Sistema de pagamentos PIX seguindo as regras do **SPB (Sistema de Pagamentos Brasileiro)** com arquitetura de microsserviços Cloud Native.

cd ../frontend-pix

docker build -t renanafs/unifiap-frontend-pix:v1.93744 .## 📋 Índice## Dados do Aluno![Rancher](https://img.shields.io/badge/rancher-v2.12.3-green.svg)![Status](https://img.shields.io/badge/status-active-success.svg)

cd ../..

```### 1.2. Microsserviços e Responsabilidades



#### Publicação no Docker Hub



```powershell| Microsserviço | Função SPB | Responsabilidades |

docker login

docker push renanafs/unifiap-api-pagamentos:v1.93744|---------------|------------|-------------------|1. [Arquitetura da Solução](#1-arquitetura-da-solução)

docker push renanafs/unifiap-auditoria:v1.93744

docker push renanafs/unifiap-frontend-pix:v1.93744| **api-pagamentos** | Banco Originador (UniFIAP Pay) | • Validar saldo da Reserva Bancária<br>• Registrar instrução PIX no arquivo compartilhado<br>• Status inicial: `AGUARDANDO_LIQUIDACAO` |

```

| **auditoria-service** | Sistema de Liquidação (BACEN/STR) | • Monitorar arquivo de instruções<br>• Processar liquidação a cada 15s<br>• Atualizar status para `LIQUIDADO` |2. [Instalação Completa](#2-instalação-completa)

#### Varredura de Vulnerabilidades

| **frontend-pix** | Interface do Usuário | • Formulário web para transações<br>• Comunicação com API de Pagamentos |

```powershell

docker scout cves renanafs/unifiap-api-pagamentos:v1.937443. [Evidências e Resultados](#3-evidências-e-resultados)**Nome:** Renan Assi de Freitas  ![Python](https://img.shields.io/badge/python-3.11-blue.svg)

docker scout cves renanafs/unifiap-auditoria:v1.93744

docker scout cves renanafs/unifiap-frontend-pix:v1.93744### 1.3. Componentes da Infraestrutura

```

4. [Comandos de Validação](#4-comandos-de-validação)

### 2.3. Subindo o Rancher

**Orquestração:**

```powershell

docker-compose -f docker-compose.rancher.yml up -d- Kubernetes (Docker Desktop)5. [Troubleshooting](#5-troubleshooting)**RM:** 93744  

```

- Rancher v2.12.3 (https://localhost:8443)

**Acesso:** https://localhost:8443  

**Credenciais:** admin / unifiap123



### 2.4. Deploy no Kubernetes**Monitoramento:**



```powershell- Prometheus (coleta de métricas)---**Total de Pontos Deste Desafio:** 9,0 pts![Docker](https://img.shields.io/badge/docker-latest-blue.svg)![Kubernetes](https://img.shields.io/badge/kubernetes-v1.33-blue.svg)

# Deploy dos serviços

kubectl apply -f k8s/unifiap-pay-spb.yaml- Grafana (dashboards)

kubectl apply -f k8s/kube-state-metrics.yaml

- Kube-state-metrics (métricas do Kubernetes)

# Configurar Prometheus

kubectl create configmap prometheus-config --from-file=monitoring/prometheus.yml -n unifiapay- Node Exporter (métricas do sistema)

kubectl patch deployment prometheus -n unifiapay -p '{

  "spec": {## 1. Arquitetura da Solução

    "template": {

      "spec": {**Recursos Compartilhados:**

        "volumes": [{"name": "config", "configMap": {"name": "prometheus-config"}}],

        "containers": [{- PersistentVolume: `/var/logs/api/instrucoes.log` (Livro-Razão do SPB)

          "name": "prometheus",

          "volumeMounts": [{"name": "config", "mountPath": "/etc/prometheus/prometheus.yml", "subPath": "prometheus.yml"}]- ConfigMap: `RESERVA_BANCARIA_SALDO=1000000.00`

        }]

      }### 1.1. Descrição---

    }

  }---

}'



# Configurar Grafana

$POD_NAME = kubectl get pods -n unifiapay -l app=grafana -o jsonpath='{.items[0].metadata.name}'## 2. Instalação Completa

kubectl exec -n unifiapay $POD_NAME -- grafana-cli admin reset-admin-password admin

python scripts/import-grafana-dashboard.pySistema de pagamentos PIX seguindo as regras do **SPB (Sistema de Pagamentos Brasileiro)** com arquitetura de microsserviços Cloud Native.



# Importar cluster no Rancher (via interface web)### PASSO 1: Pré-requisitos

# 1. Cluster Management → Import Existing → Generic

# 2. Nome: docker-desktop → Create

# 3. Copiar comando curl e executar

# 4. Aplicar patch:```powershell

kubectl patch deployment cattle-cluster-agent -n cattle-system -p '{"spec":{"template":{"spec":{"hostNetwork":true}}}}'

```# Verificar Docker Desktop com Kubernetes### 1.2. Microsserviços e Responsabilidades## 📋 ÍndiceSistema de pagamentos PIX integrado com SPB (Sistema de Pagamentos Brasileiro), desenvolvido para demonstrar arquitetura de microsserviços com Kubernetes, monitoramento Prometheus/Grafana e gerenciamento via Rancher.![Rancher](https://img.shields.io/badge/rancher-v2.12.3-green.svg)![Status](https://img.shields.io/badge/status-active-success.svg)## Dados do Aluno



---docker version



## 3. Evidências e Resultadoskubectl version --client



### 3.1. Etapa 1: Docker e Imagem Segura (1,5 pts)



#### Print 1: Docker Build Multi-Stage# Instalar dependência Python| Microsserviço | Função SPB | Responsabilidades |



**Comando:**pip install requests

```powershell

docker build -t renanafs/unifiap-api-pagamentos:v1.93744 .```|---------------|------------|-------------------|

```



![alt text](image-1.png) 

Stage de compilação### PASSO 2: Criar Rede Docker Isolada| **api-pagamentos** | Banco Originador (UniFIAP Pay) | • Validar saldo da Reserva Bancária<br>• Registrar instrução PIX no arquivo compartilhado<br>• Status inicial: `AGUARDANDO_LIQUIDACAO` |- [1. Arquitetura da Solução e Contexto SPB](#1-arquitetura-da-solução-e-contexto-spb)

- `[stage-1 1/6]` até `[stage-1 6/6]` ← Stage final

- `=> naming to docker.io/renanafs/unifiap-api-pagamentos:v1.93744`



---```powershell| **auditoria-service** | Sistema de Liquidação (BACEN/STR) | • Monitorar arquivo de instruções<br>• Processar liquidação a cada 15s<br>• Atualizar status para `LIQUIDADO` |



#### Print 2: Docker Push# Criar rede customizada (172.25.0.0/24)



**Comando:**docker network create --driver bridge --subnet 172.25.0.0/24 unifiap_net| **frontend-pix** | Interface do Usuário | • Formulário web para transações<br>• Comunicação com API de Pagamentos |  - [1.1. Descrição do Projeto](#11-descrição-do-projeto)

```powershell

docker push renanafs/unifiap-api-pagamentos:v1.93744

docker push renanafs/unifiap-auditoria:v1.93744

docker push renanafs/unifiap-frontend-pix:v1.93744# Validar criação

```

docker network inspect unifiap_net

![alt text](image-2.png)

![alt text](image-3.png)

- Confirmação das 3 imagens publicadas



---

### PASSO 3: Build das Imagens Docker

#### Print 3: Docker Scout (Vulnerabilidades)



**Comando:**

```powershell```powershell**Orquestração:**  - [1.3. Diagrama de Arquitetura](#13-diagrama-de-arquitetura)

docker scout cves renanafs/unifiap-api-pagamentos:v1.93744

```# Build api-pagamentos (tag v1.93744)



![alt text](image-4.png)

```

## Overviewdocker build -t renanafs/unifiap-api-pagamentos:v1.93744 .

  vulnerabilities │    0C     3H     5M    20L

```- Rancher v2.12.3 (https://localhost:8443)- [2. Passos de Execução](#2-passos-de-execução)

**Destaque:** `0C` = **0 CRITICAL** ✅

# Build auditoria-service

---

cd ../auditoria-service

### 3.2. Etapa 2: Rede, Comunicação e Segmentação (2,5 pts)

docker build -t renanafs/unifiap-auditoria:v1.93744 .

#### Print 1: Rede Docker Customizada

**Monitoramento:**  - [2.1. Configuração Local (Docker)](#21-configuração-local-docker)

**Comando:**

```powershell# Build frontend-pix

docker network inspect unifiap_net

```cd ../frontend-pix- Prometheus (coleta de métricas)



![alt text](image-5.png)

```json

"IPAM": {- Grafana (dashboards)  - [2.2. Build e Publicação das Imagens](#22-build-e-publicação-das-imagens-com-versão-e-rm-do-aluno)## 📋 Índice![Docker](https://img.shields.io/badge/docker-latest-blue.svg)![Kubernetes](https://img.shields.io/badge/kubernetes-v1.32-blue.svg)- **Nome:** Renan Assi de Freitas  

    "Config": [

        {# Voltar ao diretório raiz

            "Subnet": "172.25.0.0/24"

        }cd ../..- Kube-state-metrics (métricas do Kubernetes)

    ]

}```

```

- Node Exporter (métricas do sistema)  - [2.3. Subindo o Rancher](#23-subindo-o-rancher-gerenciamento-de-containers)

---

### PASSO 4: Varredura de Vulnerabilidades

#### Print 2: Comunicação Entre Containers



**Comando:**

```powershell```powershell

kubectl exec -n unifiapay deployment/api-pagamentos-simple -- curl -s http://auditoria-service:5001/health

```# Analisar imagens com Docker Scout**Recursos Compartilhados:**  - [2.4. Deploy no Kubernetes](#24-deploy-no-kubernetes)



![alt text](image-6.png)



---docker scout cves renanafs/unifiap-auditoria:v1.93744- PersistentVolume: `/var/logs/api/instrucoes.log` (Livro-Razão do SPB)



#### Print 3: Leitura de RESERVA_BANCARIA_SALDOdocker scout cves renanafs/unifiap-frontend-pix:v1.93744



**Comando:**```- ConfigMap: `RESERVA_BANCARIA_SALDO=1000000.00`- [3. Evidências e Resultados](#3-evidências-e-resultados)

```powershell

kubectl logs -n unifiapay deployment/api-pagamentos-simple --tail 20

```

### PASSO 5: Publicar no Docker Hub

![alt text](image-7.png)

  - [3.1. Etapa 1: Docker e Imagem Segura (1,5 pts)](#31-etapa-1-docker-e-imagem-segura-15-pts)- [Pré-requisitos](#-pré-requisitos)



---# Login no Docker Hub



### 3.3. Etapa 3: Kubernetes – Estrutura, Escala e Deploy (3,0 pts)docker login



#### Print 1: Pods com 2 Réplicas# Username: renanafs



**Comando:**# Password: [sua senha]## 2. Instalação Completa  - [3.2. Etapa 2: Rede, Comunicação e Segmentação (2,5 pts)](#32-etapa-2-rede-comunicação-e-segmentação-25-pts)

```powershell

kubectl get pods -n unifiapay -o wide

```

# Push das imagens

![alt text](image-8.png)

```

docker push renanafs/unifiap-frontend-pix:v1.93744

---

```

#### Print 2: Escala Horizontal



**Comando:**

```powershell### PASSO 6: Atualizar Manifestos Kubernetes```powershell  - [3.4. Etapa 4: Kubernetes – Segurança, Observação e Operação (2,0 pts)](#34-etapa-4-kubernetes--segurança-observação-e-operação-20-pts)

kubectl scale deployment api-pagamentos-simple -n unifiapay --replicas=3

kubectl get pods -n unifiapay -l app=api-pagamentos-simple

```

**IMPORTANTE:** Antes de aplicar, você precisa atualizar o arquivo `k8s/unifiap-pay-spb.yaml` para usar suas imagens do Docker Hub.# Verificar Docker Desktop com Kubernetes

![alt text](image-9.png)

#### Print 3: Volume Compartilhado (Livro-Razão)



**Comando:**

```powershell```yamlkubectl version --client

# Pod 1 da API

$POD1 = kubectl get pods -n unifiapay -l app=api-pagamentos-simple -o jsonpath='{.items[0].metadata.name}'# Exemplo:

kubectl exec -n unifiapay $POD1 -- tail -5 /var/logs/api/instrucoes.log

image: renanafs/unifiap-api-pagamentos:v1.93744  - [Pré-requisitos](#pré-requisitos)

# Pod 2 da API

$POD2 = kubectl get pods -n unifiapay -l app=api-pagamentos-simple -o jsonpath='{.items[1].metadata.name}'image: renanafs/unifiap-auditoria:v1.93744

kubectl exec -n unifiapay $POD2 -- tail -5 /var/logs/api/instrucoes.log

image: renanafs/unifiap-frontend-pix:v1.93744# Instalar dependência Python

# Pod da Auditoria

$POD_AUDIT = kubectl get pods -n unifiapay -l app=auditoria-simple -o jsonpath='{.items[0].metadata.name}'```

kubectl exec -n unifiapay $POD_AUDIT -- tail -5 /var/logs/api/instrucoes.log

```pip install requests  - [URLs de Acesso](#urls-de-acesso)- [Componentes](#-componentes)



![alt text](image-10.png)

```

2025-11-13 15:30:25|uuid|chave|valor|STATUS```

```

```powershell

---

# Aplicar manifestos  - [Comandos Úteis](#comandos-úteis)

#### Print 4: Monitoramento Contínuo (Auditoria)

kubectl apply -f k8s/unifiap-pay-spb.yaml

**Comando:**

```powershellkubectl apply -f k8s/kube-state-metrics.yaml### PASSO 2: Criar Rede Docker Isolada

kubectl logs -n unifiapay deployment/auditoria-simple --tail 30

```



**📸 TIRE PRINT:** Capture mostrando logs:# Aguardar pods subirem (1-2 minutos)  - [Troubleshooting](#troubleshooting)- [URLs de Acesso](#-urls-de-acesso)

```

INFO:root:[2025-11-13 15:30:40] Iniciando ciclo de liquidação...kubectl get pods -n unifiapay -w

INFO:root:Encontradas X transações aguardando liquidação

INFO:root:✅ Liquidação concluída``````powershell

```



---

### PASSO 8: Configurar Prometheus# Criar rede customizada (172.25.0.0/24)

### 3.4. Etapa 4: Kubernetes – Segurança, Observação e Operação (2,0 pts)



#### Print 1: Limites de Recursos

```powershelldocker network create --driver bridge --subnet 172.25.0.0/24 unifiap_net

**Comando:**

```powershell# Criar ConfigMap

kubectl top pods -n unifiapay

```kubectl create configmap prometheus-config --from-file=monitoring/prometheus.yml -n unifiapay---- [Comandos Úteis](#-comandos-úteis)



**📸 TIRE PRINT:** Capture mostrando uso de CPU e Memória de cada pod



---# Aplicar patch no deployment# Validar criação



#### Print 2: SecurityContextkubectl patch deployment prometheus -n unifiapay -p '{



**Comando:**  "spec": {docker network inspect unifiap_net

```powershell

kubectl get deployment api-pagamentos-simple -n unifiapay -o yaml | Select-String -Pattern "securityContext" -Context 5    "template": {

```

      "spec": {```

**📸 TIRE PRINT:** Capture mostrando:

```yaml        "volumes": [

securityContext:

  runAsNonRoot: true          {## 1. Arquitetura da Solução e Contexto SPB- [Testes](#-testes)## 📋 Índice![Python](https://img.shields.io/badge/python-3.11-blue.svg)- **Total de Pontos Deste Desafio:** 9,0 pts  

  runAsUser: 1000

  allowPrivilegeEscalation: false            "name": "config",

```

            "configMap": {### PASSO 3: Build das Imagens Docker

---

              "name": "prometheus-config"

#### Print 3: Deploy Inseguro (Tentativa)

            }

**Comando:**

```powershell          }

kubectl run test-insecure --image=nginx -n unifiapay --overrides='{

  "spec": {        ],```powershell

    "containers": [{

      "name": "nginx",        "containers": [

      "image": "nginx",

      "securityContext": {"privileged": true}          {# Build api-pagamentos (tag v1.93744)### 1.1. Descrição do Projeto- [Troubleshooting](#-troubleshooting)

    }]

  }            "name": "prometheus",

}'

            "volumeMounts": [cd core/api-pagamentos

kubectl describe pod test-insecure -n unifiapay

```              {



**📸 TIRE PRINT:** Capture mostrando a criação do pod e a descrição                "name": "config",docker build -t codecaman/unifiap-api-pagamentos:v1.93744 .



---                "mountPath": "/etc/prometheus/prometheus.yml",



#### Print 4: Permissões ServiceAccount                "subPath": "prometheus.yml"



**Comando:**              }

```powershell

kubectl auth can-i create pods --as=system:serviceaccount:unifiapay:default -n unifiapay            ]# Build auditoria-serviceEste projeto implementa uma **arquitetura de microsserviços moderna na Nuvem (Cloud Native)** para a **UniFIAP Pay**.- [Estrutura do Projeto](#-estrutura-do-projeto)

kubectl auth can-i delete deployments --as=system:serviceaccount:unifiapay:default -n unifiapay

kubectl auth can-i get pods --as=system:serviceaccount:unifiapay:default -n unifiapay          }

```

        ]cd ../auditoria-service

**📸 TIRE PRINT:** Capture mostrando:

```      }

no   ← create pods (negado)

no   ← delete deployments (negado)    }docker build -t codecaman/unifiap-auditoria:v1.93744 .

yes  ← get pods (permitido)

```  }



---}'



## 4. Comandos Úteis



### Verificar Status# Aguardar restart# Build frontend-pixO objetivo é simular um **fluxo de pagamento PIX** seguindo as regras do **Sistema de Pagamentos Brasileiro (SPB)**, que exige compensação e liquidação através do Banco Central (STR).



```powershellkubectl rollout status deployment prometheus -n unifiapay

kubectl get pods -n unifiapay

kubectl get svc -n unifiapaycd ../frontend-pix

kubectl get deployments -n unifiapay

```# Recarregar configuração



### Testar PIXStart-Sleep -Seconds 15docker build -t codecaman/unifiap-frontend-pix:v1.93744 .



```powershellcurl -X POST http://localhost:30090/-/reload

curl -X POST http://localhost:30050/pix -H "Content-Type: application/json" -d @test-pix.json

``````



### Acessos



| Serviço | URL | Credenciais |### PASSO 9: Configurar Grafana# Voltar ao diretório raizO desafio foca em **três pilares**:---- [Pré-requisitos](#-pré-requisitos)

|---------|-----|-------------|

| Frontend PIX | http://localhost:30082 | - |

| Grafana | http://localhost:30300 | admin / admin |

| Prometheus | http://localhost:30090 | - |```powershellcd ../..

| Rancher | https://localhost:8443 | admin / unifiap123 |

# Resetar senha do admin

---

$POD_NAME = kubectl get pods -n unifiapay -l app=grafana -o jsonpath='{.items[0].metadata.name}'```

## 📊 Checklist de Evidências

kubectl exec -n unifiapay $POD_NAME -- grafana-cli admin reset-admin-password admin

### Etapa 1 (1,5 pts)

- [ ] Print do `docker build` mostrando multi-stage

- [ ] Print do `docker push` com tag v1.93744

- [ ] Print do `docker scout` com 0 CRITICAL# Importar dashboard (automático)



### Etapa 2 (2,5 pts)Start-Sleep -Seconds 5### PASSO 4: Varredura de Vulnerabilidades1. **Segurança**: Construir containers e redes isoladas.

- [ ] Print do `docker network inspect` mostrando 172.25.0.0/24

- [ ] Print do `curl` entre containerspython scripts/import-grafana-dashboard.py

- [ ] Print dos logs mostrando RESERVA_BANCARIA_SALDO

```

### Etapa 3 (3,0 pts)

- [ ] Print do `kubectl get pods` com 2 réplicas

- [ ] Print do `kubectl scale` mostrando 3 réplicas

- [ ] Print dos 3 pods lendo mesmo arquivo### PASSO 10: Subir o Rancher```powershell2. **Orquestração**: Usar o Kubernetes para gerenciar a aplicação em escala.

- [ ] Print dos logs da auditoria processando



### Etapa 4 (2,0 pts)

- [ ] Print do `kubectl top pods````powershell# Analisar imagens com Docker Scout

- [ ] Print do YAML com securityContext

- [ ] Print da tentativa de pod privilegiado# Iniciar container do Rancher

- [ ] Print do `kubectl auth can-i`

docker-compose -f docker-compose.rancher.yml up -ddocker scout cves codecaman/unifiap-api-pagamentos:v1.937443. **Regras de Negócio**: Aplicar a lógica da Reserva Bancária e Liquidação.## 🔧 Pré-requisitos- [Instalação Completa](#-instalação-completa)

---



**Autor:** Renan Assi de Freitas | **RM:** 93744 | **FIAP** - Pós Tech Software Architecture

# Aguardar inicialização (60 segundos)docker scout cves codecaman/unifiap-auditoria:v1.93744

Start-Sleep -Seconds 60

docker scout cves codecaman/unifiap-frontend-pix:v1.93744

# Acesse: https://localhost:8443

# Login: admin / unifiap123```

```

**Tecnologias Utilizadas:**

### PASSO 11: Importar Cluster no Rancher

### PASSO 5: Publicar no Docker Hub

**Via Interface Web:**

- **Docker** - Containerização dos microsserviços

1. Acesse https://localhost:8443

2. Login: `admin` / `unifiap123````powershell

3. Clique em **Cluster Management**

4. Clique em **Import Existing**# Login no Docker Hub- **Kubernetes** - Orquestração e gerenciamento de containersAntes de iniciar, certifique-se de ter instalado:- [Arquitetura](#%EF%B8%8F-arquitetura)Sistema de pagamentos PIX integrado com SPB (Sistema de Pagamentos Brasileiro), desenvolvido para demonstrar arquitetura de microsserviços com Kubernetes, monitoramento e gerenciamento via Rancher.## 🚀 PROJETO FINALIZADO - VERSÃO COMPLETA

5. Selecione **Generic**

6. Nome do cluster: `docker-desktop`docker login

7. Clique em **Create**

8. **COPIE O SEGUNDO COMANDO** (começa com `curl --insecure`)- **Rancher v2.12.3** - Interface de gerenciamento de clusters



**Via Terminal:**# Push das imagens



```powershelldocker push codecaman/unifiap-api-pagamentos:v1.93744- **Python 3.11 + Flask** - Desenvolvimento dos microsserviços

# Cole o comando do Rancher (exemplo - USE SEU TOKEN):

curl --insecure -sfL https://localhost:8443/v3/import/SEU_TOKEN.yaml | kubectl apply -f -docker push codecaman/unifiap-auditoria:v1.93744



# Aguardar cattle-system subirdocker push codecaman/unifiap-frontend-pix:v1.93744- **Prometheus + Grafana** - Monitoramento e observabilidade

Start-Sleep -Seconds 15

```

# Aplicar patch hostNetwork

kubectl patch deployment cattle-cluster-agent -n cattle-system -p '{- **Nginx** - Servidor web para o frontend- **Docker Desktop** com Kubernetes habilitado- [Componentes](#-componentes)

  "spec": {

    "template": {### PASSO 6: Deploy no Kubernetes

      "spec": {

        "hostNetwork": true

      }

    }```powershell

  }

}'# Aplicar manifestos---- **kubectl** configurado e funcionando



# Verificar statuskubectl apply -f k8s/unifiap-pay-spb.yaml

kubectl get pods -n cattle-system

```kubectl apply -f k8s/kube-state-metrics.yaml



**Aguarde 1-2 minutos** - O cluster mudará de "Provisioning" para "Active" no Rancher.



---# Aguardar pods subirem (1-2 minutos)### 1.2. Papéis e Responsabilidades dos Microsserviços (Fluxo SPB)- **Python 3.11+** com a biblioteca `requests` instalada:- [Acessos](#-acessos)Sistema de Pagamentos Brasileiro (SPB) - **100% IMPLEMENTADO** com:



## 3. Evidências e Resultadoskubectl get pods -n unifiapay -w



### 3.1. Etapa 1: Docker e Imagem Segura (1,5 pts)```



#### Comandos para Evidências:



```powershell### PASSO 7: Configurar Prometheus| Microsserviço | Função Principal (Papel no SPB) | Responsabilidades de Código |  ```bash

# BUILD (Print obrigatório - mostra multi-stage)

cd core/api-pagamentos

docker build -t renanafs/unifiap-api-pagamentos:v1.93744 .

```powershell|---------------|----------------------------------|------------------------------|

cd ../auditoria-service

docker build -t renanafs/unifiap-auditoria:v1.93744 .# Criar ConfigMap



cd ../frontend-pixkubectl create configmap prometheus-config --from-file=monitoring/prometheus.yml -n unifiapay| **api-pagamentos** | Simula o **Banco Originador (UniFIAP Pay)**. Garante que o banco tem dinheiro suficiente no BACEN para cobrir o PIX (a **Reserva Bancária**). | 1. **Ler Saldo**: Consultar `RESERVA_BANCARIA_SALDO` (do ENV/ConfigMap).<br>2. **Pré-Validar**: Aplicar a regra: **SE** Valor do PIX <= RESERVA_BANCARIA_SALDO.<br>3. **Registrar**: Se aprovado, escrever (apendar) a instrução de pagamento no arquivo `/var/logs/api/instrucoes.log` com o status `AGUARDANDO_LIQUIDACAO`. |  pip install requests- [Comandos Úteis](#-comandos-úteis)

docker build -t renanafs/unifiap-frontend-pix:v1.93744 .



cd ../..

# Aplicar patch no deployment| **auditoria-service** | Simula o **Sistema de Liquidação (BACEN/STR)**. Atua como a autoridade central que processa os pagamentos. | 1. **Monitorar**: Ler novas linhas no arquivo `/var/logs/api/instrucoes.log` (o **Livro-Razão**).<br>2. **Liquidação**: Buscar transações `AGUARDANDO_LIQUIDACAO` e atualizar o status para `LIQUIDADO`.<br>3. **Automação**: Ser executado de forma contínua (monitoramento a cada 15 segundos). |

# PUSH (Print obrigatório - mostra tag v1.93744)

docker push renanafs/unifiap-api-pagamentos:v1.93744kubectl patch deployment prometheus -n unifiapay -p '{

docker push renanafs/unifiap-auditoria:v1.93744

docker push renanafs/unifiap-frontend-pix:v1.93744  "spec": {| **frontend-pix** | Interface web para o usuário final realizar transações PIX. | 1. **Interface**: Fornecer formulário HTML para entrada de dados (chave PIX, valor, descrição).<br>2. **Comunicação**: Enviar requisições POST para a API de Pagamentos.<br>3. **Feedback**: Exibir resultado da transação ao usuário. |  ```



# VULNERABILIDADES (Print obrigatório - sem vulnerabilidades críticas)    "template": {

docker scout cves renanafs/unifiap-api-pagamentos:v1.93744

docker scout cves renanafs/unifiap-auditoria:v1.93744      "spec": {

docker scout cves renanafs/unifiap-frontend-pix:v1.93744

```        "volumes": [



**📸 Prints necessários:**          {**Fluxo de Dados:**- **curl** para realizar testes de API- [Testes](#-testes)## 🏗️ Arquitetura

- [ ] `docker build` mostrando multi-stage build

- [ ] `docker push` com tag v1.93744 (3 imagens)            "name": "config",

- [ ] `docker scout` sem vulnerabilidades críticas (0 critical, 0 high)

            "configMap": {

---

              "name": "prometheus-config"

### 3.2. Etapa 2: Rede, Comunicação e Segmentação (2,5 pts)

            }1. **Usuário** acessa o Frontend PIX e preenche os dados da transação- **PowerShell 5.1+** (Windows) ou **Bash** (Linux/macOS)

#### Comandos para Evidências:

          }

```powershell

# REDE CUSTOMIZADA (Print obrigatório)        ],2. **Frontend** envia requisição POST para `api-pagamentos`

docker network inspect unifiap_net

        "containers": [

# COMUNICAÇÃO ENTRE CONTAINERS (Print obrigatório)

kubectl exec -n unifiapay deployment/api-pagamentos-simple -- curl -s http://auditoria-service:5001/health          {3. **API Pagamentos** valida o saldo da Reserva Bancária- [Troubleshooting](#-troubleshooting)



# LEITURA DE ENV (Print obrigatório)            "name": "prometheus",

kubectl logs -n unifiapay deployment/api-pagamentos-simple --tail 20 | Select-String "RESERVA_BANCARIA_SALDO"

```            "volumeMounts": [4. Se aprovado, **API Pagamentos** registra a instrução no arquivo compartilhado (`instrucoes.log`) com status `AGUARDANDO_LIQUIDACAO`



**📸 Prints necessários:**              {

- [ ] `docker network inspect` mostrando subnet 172.25.0.0/24

- [ ] `curl` entre containers funcionando                "name": "config",5. **Auditoria Service** monitora continuamente o arquivo `instrucoes.log`---

- [ ] Logs mostrando leitura de `RESERVA_BANCARIA_SALDO`

                "mountPath": "/etc/prometheus/prometheus.yml",

---

                "subPath": "prometheus.yml"6. Ao detectar novas transações pendentes, **Auditoria Service** atualiza o status para `LIQUIDADO`

### 3.3. Etapa 3: Kubernetes – Estrutura, Escala e Deploy (3,0 pts)

              }

#### Comandos para Evidências:

            ]7. Transação é concluída e registrada nos logs- ✅ **Microsserviços Completos**: API PIX + Auditoria BACEN

```powershell

# PODS COM RÉPLICAS (Print obrigatório)          }

kubectl get pods -n unifiapay -o wide

        ]

# ESCALA HORIZONTAL (Print obrigatório)

kubectl scale deployment api-pagamentos-simple -n unifiapay --replicas=3      }

kubectl get pods -n unifiapay -l app=api-pagamentos-simple

    }---## 🚀 Instalação Passo a Passo

# VOLUME COMPARTILHADO (Print obrigatório)

# Pod 1 da API  }

$POD1 = kubectl get pods -n unifiapay -l app=api-pagamentos-simple -o jsonpath='{.items[0].metadata.name}'

kubectl exec -n unifiapay $POD1 -- tail -5 /var/logs/api/instrucoes.log}'



# Pod 2 da API

$POD2 = kubectl get pods -n unifiapay -l app=api-pagamentos-simple -o jsonpath='{.items[1].metadata.name}'

kubectl exec -n unifiapay $POD2 -- tail -5 /var/logs/api/instrucoes.log# Aguardar restart### 1.3. Diagrama de Arquitetura## 🔧 Pré-requisitos



# Pod da Auditoriakubectl rollout status deployment prometheus -n unifiapay

$POD_AUDIT = kubectl get pods -n unifiapay -l app=auditoria-simple -o jsonpath='{.items[0].metadata.name}'

kubectl exec -n unifiapay $POD_AUDIT -- tail -5 /var/logs/api/instrucoes.log



# MONITORAMENTO CONTÍNUO (Print obrigatório)# Recarregar configuração

kubectl logs -n unifiapay deployment/auditoria-simple --tail 30 -f

```Start-Sleep -Seconds 15A arquitetura do sistema é composta pelos seguintes componentes:### PASSO 1: Deploy dos Microsserviços no Kubernetes



**📸 Prints necessários:**curl -X POST http://localhost:30090/-/reload

- [ ] `kubectl get pods` mostrando API com 2 réplicas iniciais

- [ ] `kubectl scale` aumentando para 3 réplicas```

- [ ] 3 pods (2 API + 1 Auditoria) lendo/escrevendo mesmo arquivo

- [ ] Logs da auditoria processando a cada 15s



---### PASSO 8: Configurar Grafana**Camada de Gerenciamento:**```- ✅ **Frontend Web Moderno**: Interface PIX responsiva com Bootstrap



### 3.4. Etapa 4: Kubernetes – Segurança, Observação e Operação (2,0 pts)



#### Comandos para Evidências:```powershell- **Rancher** (https://localhost:8443) - Interface web para gerenciar o cluster Kubernetes



```powershell# Resetar senha do admin

# LIMITES DE RECURSOS (Print obrigatório)

kubectl top pods -n unifiapay$POD_NAME = kubectl get pods -n unifiapay -l app=grafana -o jsonpath='{.items[0].metadata.name}'- **Docker Desktop** - Cluster Kubernetes localExecute os comandos abaixo para subir toda a infraestrutura do UniFIAP Pay SPB:



# SECURITY CONTEXT (Print obrigatório)kubectl exec -n unifiapay $POD_NAME -- grafana-cli admin reset-admin-password admin

kubectl get deployment api-pagamentos-simple -n unifiapay -o yaml | Select-String -Pattern "securityContext" -Context 5



# DEPLOY INSEGURO (Print obrigatório - tentativa)

kubectl run test-insecure --image=nginx -n unifiapay --overrides='{# Importar dashboard (automático)

  "spec": {

    "containers": [{Start-Sleep -Seconds 5**Camada de Aplicação (Microsserviços):**- **Docker Desktop** com Kubernetes habilitado

      "name": "nginx",

      "image": "nginx",python scripts/import-grafana-dashboard.py

      "securityContext": {

        "privileged": true```- **api-pagamentos** (NodePort 30050) - Processa transações PIX e valida saldo de reserva bancária

      }

    }]

  }

}'### PASSO 9: Subir o Rancher- **auditoria-service** (NodePort 30051) - Simula liquidação automática do BACEN a cada 15 segundos```bash



kubectl describe pod test-insecure -n unifiapay



# PERMISSÕES SERVICEACCOUNT (Print obrigatório)```powershell- **frontend-pix** (NodePort 30082) - Interface web para realizar transações

kubectl auth can-i create pods --as=system:serviceaccount:unifiapay:default -n unifiapay

kubectl auth can-i delete deployments --as=system:serviceaccount:unifiapay:default -n unifiapay# Iniciar container do Rancher

kubectl auth can-i get pods --as=system:serviceaccount:unifiapay:default -n unifiapay

```docker-compose -f docker-compose.rancher.yml up -d# 1.1. Aplicar todos os recursos (Namespace, ConfigMaps, Secrets, Deployments, Services)- **kubectl** configurado e apontando para o cluster local┌─────────────────────────────────────────────────────────┐- ✅ **Docker Otimizado**: Multi-stage builds com segurança



**📸 Prints necessários:**

- [ ] `kubectl top pods` mostrando limites aplicados

- [ ] Manifest YAML com `runAsNonRoot: true`# Aguardar inicialização (60 segundos)**Camada de Observabilidade (Monitoramento):**

- [ ] Tentativa de deploy inseguro + `describe pod`

- [ ] `kubectl auth can-i` mostrando permissões restritasStart-Sleep -Seconds 60



---- **Prometheus** (NodePort 30090) - Coleta e armazena métricas do sistema e Kuberneteskubectl apply -f k8s/unifiap-pay-spb.yaml



## 4. Comandos de Validação# Acesse: https://localhost:8443



### Verificar Status Completo# Login: admin / unifiap123- **Grafana** (NodePort 30300) - Visualização de métricas através de dashboards



```powershell```

# Todos os pods rodando

kubectl get pods -n unifiapay- **Node Exporter** (NodePort 30100) - Coleta métricas do sistema operacional (CPU, memória, disco)- **Python 3.11+** com requests (`pip install requests`)



# Todos os services### PASSO 10: Importar Cluster no Rancher

kubectl get svc -n unifiapay

- **Kube State Metrics** (porta 8080 interna) - Coleta métricas dos recursos do Kubernetes (pods, deployments, etc)

# Deployments

kubectl get deployments -n unifiapay**Via Interface Web:**



# ConfigMaps# 1.2. Aplicar kube-state-metrics para coletar métricas do Kubernetes

kubectl get configmap -n unifiapay

1. Acesse https://localhost:8443

# PersistentVolume e PVC

kubectl get pv,pvc -n unifiapay2. Login: `admin` / `unifiap123`**Recursos Compartilhados:**



# Rancher3. Clique em **Cluster Management**

kubectl get pods -n cattle-system

docker ps --filter name=rancher4. Clique em **Import Existing**- **PersistentVolume** (`unifiap-logs-pv`) - Volume compartilhado de 1Gi para logskubectl apply -f k8s/kube-state-metrics.yaml- **curl** instalado (para testes de API)│                  Rancher Management                      │- ✅ **Kubernetes Completo**: 10 manifests + RBAC + NetworkPolicies  

```

5. Selecione **Generic**

### Testar Transação PIX

6. Nome do cluster: `docker-desktop`- **PersistentVolumeClaim** (`unifiap-logs-pvc`) - Claim do volume compartilhado

```powershell

# Usando arquivo JSON7. Clique em **Create**

curl -X POST http://localhost:30050/pix -H "Content-Type: application/json" -d @test-pix.json

8. **COPIE O SEGUNDO COMANDO** (começa com `curl --insecure`)- **ConfigMap** (`unifiap-config`) - Variáveis de ambiente (RESERVA_BANCARIA_SALDO, etc)

# Teste manual

curl -X POST http://localhost:30050/pix -H "Content-Type: application/json" -d '{

  "chave_pix": "11999887766",

  "valor": 50.00,**Via Terminal:**- **Namespace** (`unifiapay`) - Isolamento lógico dos recursos

  "descricao": "Teste RM 93744"

}'

```

```powershell# 1.3. Verificar se todos os pods foram criados- **PowerShell 5.1+** (Windows) ou **Bash** (Linux/Mac)

### Verificar Logs

# Cole o comando do Rancher (exemplo - USE SEU TOKEN):

```powershell

# API de Pagamentoscurl --insecure -sfL https://localhost:8443/v3/import/SEU_TOKEN.yaml | kubectl apply -f -**Elementos de Segurança:**

kubectl logs -n unifiapay deployment/api-pagamentos-simple --tail 50 -f



# Auditoria (liquidação)

kubectl logs -n unifiapay deployment/auditoria-simple --tail 50 -f# Aguardar cattle-system subir- **SecurityContext** - Configurações de segurança (runAsNonRoot, readOnlyRootFilesystem)kubectl get pods -n unifiapay



# PrometheusStart-Sleep -Seconds 15

kubectl logs -n unifiapay deployment/prometheus --tail 50

- **Resources** - Limites de CPU e memória para todos os pods

# Grafana

kubectl logs -n unifiapay deployment/grafana --tail 50# Aplicar patch hostNetwork

```

kubectl patch deployment cattle-cluster-agent -n cattle-system -p '{- **ServiceAccount** - Contas de serviço dedicadas com permissões restritas│              https://localhost:8443                      │- ✅ **Rancher Configurado**: Interface de gerenciamento visual

### Acessar Serviços

  "spec": {

| Serviço | URL | Credenciais |

|---------|-----|-------------|    "template": {- **NetworkPolicy** - Políticas de rede para segmentação (futuro)

| Frontend PIX | http://localhost:30082 | - |

| API Swagger | http://localhost:30050/docs | - |      "spec": {

| Auditoria | http://localhost:30051 | - |

| Grafana | http://localhost:30300 | admin / admin |        "hostNetwork": true# Aguarde até que TODOS os 7 pods estejam com status "Running" (1/1)

| Prometheus | http://localhost:30090 | - |

| Rancher | https://localhost:8443 | admin / unifiap123 |      }



---    }**Volume Compartilhado (Livro-Razão):**



## 5. Troubleshooting  }



### Pods não iniciam}'# Pods esperados:## 🚀 Instalação Completa



```powershell

# Ver detalhes

kubectl describe pod <NOME_DO_POD> -n unifiapay# Verificar statusO arquivo `/var/logs/api/instrucoes.log` atua como o **Livro-Razão do SPB**, sendo compartilhado entre:



# Ver logskubectl get pods -n cattle-system

kubectl logs <NOME_DO_POD> -n unifiapay

```- `api-pagamentos` → Escreve novas instruções (APPEND)# - api-pagamentos-simple

# Reiniciar deployment

kubectl rollout restart deployment <NOME_DO_DEPLOYMENT> -n unifiapay

```

**Aguarde 1-2 minutos** - O cluster mudará de "Provisioning" para "Active" no Rancher.- `auditoria-service` → Lê e atualiza status das instruções

### Rancher não conecta



```powershell

# Verificar patch hostNetwork---# - auditoria-simple└────────────────────┬────────────────────────────────────┘- ✅ **Monitoramento**: Prometheus + Grafana + Dashboards

kubectl get deployment cattle-cluster-agent -n cattle-system -o yaml | Select-String "hostNetwork"



# Aplicar patch se necessário

kubectl patch deployment cattle-cluster-agent -n cattle-system -p '{## 3. Evidências e ResultadosEste design simula o comportamento real do SPB, onde todas as transações são registradas centralmente e processadas pelo Banco Central.

  "spec": {

    "template": {

      "spec": {

        "hostNetwork": true### 3.1. Etapa 1: Docker e Imagem Segura (1,5 pts)# - frontend-pix-simple

      }

    }

  }

}'#### Comandos para Evidências:---



# Ver logs

kubectl logs -n cattle-system deployment/cattle-cluster-agent --tail 20

``````powershell# - grafana### Passo 1: Deploy do Sistema UniFIAP Pay SPB



### Grafana sem dados# BUILD (Print obrigatório)



```powershelldocker build -t codecaman/unifiap-api-pagamentos:v1.93744 .## 2. Passos de Execução

# Verificar kube-state-metrics

kubectl get pods -n unifiapay -l app=kube-state-metrics



# Verificar targets do Prometheus# PUSH (Print obrigatório)# - prometheus

curl http://localhost:30090/api/v1/targets

docker push codecaman/unifiap-api-pagamentos:v1.93744

# Recarregar Prometheus

curl -X POST http://localhost:30090/-/reloaddocker push codecaman/unifiap-auditoria:v1.93744### 2.1. Configuração Local (Docker)

```

docker push codecaman/unifiap-frontend-pix:v1.93744

### Limpar ambiente completo

# - node-exporter                     │- ✅ **Segurança**: Non-root containers + políticas de rede

```powershell

# Remover todos os recursos# VULNERABILIDADES (Print obrigatório)

kubectl delete -f k8s/unifiap-pay-spb.yaml

kubectl delete -f k8s/kube-state-metrics.yamldocker scout cves codecaman/unifiap-api-pagamentos:v1.93744Antes de iniciar o deploy, é necessário configurar o ambiente local.



# Parar Rancher```

docker-compose -f docker-compose.rancher.yml down

# - kube-state-metrics

# Remover namespaces

kubectl delete namespace unifiapay --force --grace-period=0**📸 Prints necessários:**

kubectl delete namespace cattle-system --force --grace-period=0

- [ ] `docker build` mostrando multi-stage#### Pré-requisitos

# Remover rede Docker

docker network rm unifiap_net- [ ] `docker push` com tag v1.93744 (3 imagens)

```

- [ ] `docker scout` sem vulnerabilidades críticas``````bash

---



## 📁 Estrutura do Projeto

---Certifique-se de ter instalado:

```

unifiap-pay-spb/

├── core/

│   ├── api-pagamentos/          # Microsserviço de pagamentos### 3.2. Etapa 2: Rede, Comunicação e Segmentação (2,5 pts)

│   ├── auditoria-service/       # Microsserviço de liquidação

│   └── frontend-pix/            # Interface web

├── k8s/

│   ├── unifiap-pay-spb.yaml     # Manifesto principal#### Comandos para Evidências:- **Docker Desktop** com Kubernetes habilitado

│   └── kube-state-metrics.yaml  # Métricas do K8s

├── monitoring/

│   ├── prometheus.yml           # Config do Prometheus

│   └── grafana/```powershell- **kubectl** configurado e funcionando**⏱️ Tempo estimado:** 1-2 minutos# 1. Aplicar todos os recursos do Kubernetes        ┌────────────▼─────────────┐- ✅ **Deploy Automatizado**: Scripts Windows + Linux prontos  

│       └── dashboards/

│           └── unifiap-complete.json# REDE CUSTOMIZADA (Print obrigatório)

├── scripts/

│   └── import-grafana-dashboard.pydocker network inspect unifiap_net- **Python 3.11+** com a biblioteca `requests`:

├── docker-compose.rancher.yml   # Rancher

├── test-pix.json                # Payload de teste

└── README.md                    # Este arquivo

```# COMUNICAÇÃO ENTRE CONTAINERS (Print obrigatório)  ```bash



---kubectl exec -n unifiapay deployment/api-pagamentos-simple -- curl -s http://auditoria-service:5001/health



## 📚 Recursos Importantes  pip install requests



**Imagens Docker Hub:**# LEITURA DE ENV (Print obrigatório)

- renanafs/unifiap-api-pagamentos:v1.93744

- renanafs/unifiap-auditoria:v1.93744kubectl logs -n unifiapay deployment/api-pagamentos-simple --tail 20 | Select-String "RESERVA_BANCARIA_SALDO"  ```---kubectl apply -f k8s/unifiap-pay-spb.yaml

- renanafs/unifiap-frontend-pix:v1.93744

```

**ConfigMap:**

- RESERVA_BANCARIA_SALDO: 1000000.00 (R$ 1 milhão)- **curl** para realizar testes de API

- LIQUIDATION_MODE: continuous

- MONITORING_INTERVAL: 15s**📸 Prints necessários:**



**Volume Compartilhado:**- [ ] `docker network inspect` mostrando subnet 172.25.0.0/24- **PowerShell 5.1+** (Windows)

- Path: /var/logs/api/instrucoes.log

- Função: Livro-Razão do SPB- [ ] `curl` entre containers funcionando

- Compartilhado entre: api-pagamentos (write) + auditoria-service (read/update)

- [ ] Logs mostrando leitura de `RESERVA_BANCARIA_SALDO`

---



## 👨‍💻 Autor

---#### Criar Rede Docker Segmentada (Isolamento)### PASSO 2: Configurar o Prometheus        │   Kubernetes Cluster     │

**Renan Assi de Freitas**  

**RM:** 93744  

**Docker Hub:** renanafs  

**FIAP** - Pós Tech Software Architecture### 3.3. Etapa 3: Kubernetes – Estrutura, Escala e Deploy (3,0 pts)



---



## 🚀 Início Rápido - Comandos Essenciais#### Comandos para Evidências:Para isolar os containers em uma rede customizada:



Para executar a **Etapa 1** agora mesmo:



```powershell```powershell

# 1. Build

cd core/api-pagamentos# PODS COM RÉPLICAS (Print obrigatório)

docker build -t renanafs/unifiap-api-pagamentos:v1.93744 .

kubectl get pods -n unifiapay -o wide```bashO Prometheus precisa de um ConfigMap para coletar métricas do kube-state-metrics:# 2. Aplicar kube-state-metrics para métricas do Kubernetes

# 2. Push (após login)

docker login

docker push renanafs/unifiap-api-pagamentos:v1.93744

![alt text](image.png)

# ESCALA HORIZONTAL (Print obrigatório)# Criar rede Docker customizada

# 3. Scan

docker scout cves renanafs/unifiap-api-pagamentos:v1.93744kubectl scale deployment api-pagamentos-simple -n unifiapay --replicas=3

```

kubectl get pods -n unifiapay -l app=api-pagamentos-simpledocker network create --driver bridge --subnet 172.25.0.0/24 unifiap_net

**🎉 Sistema completo e funcional!**



# VOLUME COMPARTILHADO (Print obrigatório)

# Pod 1 da API

$POD1 = kubectl get pods -n unifiapay -l app=api-pagamentos-simple -o jsonpath='{.items[0].metadata.name}'# Verificar a criação da rede```bashkubectl apply -f k8s/kube-state-metrics.yaml        │    (Docker Desktop)      │---

kubectl exec -n unifiapay $POD1 -- tail -5 /var/logs/api/instrucoes.log

docker network inspect unifiap_net

# Pod 2 da API

$POD2 = kubectl get pods -n unifiapay -l app=api-pagamentos-simple -o jsonpath='{.items[1].metadata.name}'```# 2.1. Criar o ConfigMap com a configuração do Prometheus

kubectl exec -n unifiapay $POD2 -- tail -5 /var/logs/api/instrucoes.log



# Pod da Auditoria

$POD_AUDIT = kubectl get pods -n unifiapay -l app=auditoria-simple -o jsonpath='{.items[0].metadata.name}'**Saída esperada:**kubectl create configmap prometheus-config --from-file=monitoring/prometheus.yml -n unifiapay

kubectl exec -n unifiapay $POD_AUDIT -- tail -5 /var/logs/api/instrucoes.log

```json

# MONITORAMENTO CONTÍNUO (Print obrigatório)

kubectl logs -n unifiapay deployment/auditoria-simple --tail 30 -f[

```

    {

**📸 Prints necessários:**

- [ ] `kubectl get pods` mostrando API com 2 réplicas        "Name": "unifiap_net",# 2.2. Criar arquivo de patch temporário (COPIE E COLE TODO O BLOCO)# 3. Verificar se todos os pods estão rodando        └────────────┬─────────────┘

- [ ] `kubectl scale` aumentando para 3 réplicas

- [ ] 3 pods (2 API + 1 Auditoria) lendo/escrevendo mesmo arquivo        "Driver": "bridge",

- [ ] Logs da auditoria processando a cada 15s

        "IPAM": {cat <<'EOF' > /tmp/prometheus-patch.json

---

            "Config": [

### 3.4. Etapa 4: Kubernetes – Segurança, Observação e Operação (2,0 pts)

                {{kubectl get pods -n unifiapay

#### Comandos para Evidências:

                    "Subnet": "172.25.0.0/24"

```powershell

# LIMITES DE RECURSOS (Print obrigatório)                }  "spec": {

kubectl top pods -n unifiapay

            ]

# SECURITY CONTEXT (Print obrigatório)

kubectl get deployment api-pagamentos-simple -n unifiapay -o yaml | Select-String -Pattern "securityContext" -Context 5        }    "template": {                     │## 📋 Índice



# DEPLOY INSEGURO (Print obrigatório - tentativa)    }

kubectl run test-insecure --image=nginx -n unifiapay --overrides='{

  "spec": {]      "spec": {

    "containers": [{

      "name": "nginx",```

      "image": "nginx",

      "securityContext": {        "volumes": [# Aguarde até que todos os pods estejam com status Running (1/1)

        "privileged": true

      }#### Preparar Variáveis de Ambiente

    }]

  }          {

}'

As variáveis de ambiente estão configuradas no **ConfigMap** `unifiap-config` dentro do arquivo `k8s/unifiap-pay-spb.yaml`:

kubectl describe pod test-insecure -n unifiapay

            "name": "config",# Pods esperados: 7 (api-pagamentos, auditoria, frontend-pix, grafana, prometheus, node-exporter, kube-state-metrics)     ┌───────────────┴───────────────┐1. [Arquitetura da Solução](#1-arquitetura-da-solução-e-contexto-spb)

# PERMISSÕES SERVICEACCOUNT (Print obrigatório)

kubectl auth can-i create pods --as=system:serviceaccount:unifiapay:default -n unifiapay```yaml

kubectl auth can-i delete deployments --as=system:serviceaccount:unifiapay:default -n unifiapay

kubectl auth can-i get pods --as=system:serviceaccount:unifiapay:default -n unifiapayapiVersion: v1            "configMap": {

```

kind: ConfigMap

**📸 Prints necessários:**

- [ ] `kubectl top pods` mostrando limites aplicadosmetadata:              "name": "prometheus-config"```

- [ ] Manifest YAML com `runAsNonRoot: true`

- [ ] Tentativa de deploy inseguro + `describe pod`  name: unifiap-config

- [ ] `kubectl auth can-i` mostrando permissões restritas

  namespace: unifiapay            }

---

data:

## 4. Comandos de Validação

  RESERVA_BANCARIA_SALDO: "1000000.00"  # R$ 1.000.000,00          }     │                               │2. [Estrutura do Projeto](#2-estrutura-do-projeto)

### Verificar Status Completo

  LIQUIDATION_MODE: "continuous"

```powershell

# Todos os pods rodando  MONITORING_INTERVAL: "15s"        ],

kubectl get pods -n unifiapay

```

# Todos os services

kubectl get svc -n unifiapay        "containers": [### Passo 2: Configurar Prometheus



# Deployments**Não é necessário criar arquivo `.env`** - as variáveis são injetadas automaticamente via ConfigMap.

kubectl get deployments -n unifiapay

          {

# ConfigMaps

kubectl get configmap -n unifiapay---



# PersistentVolume e PVC            "name": "prometheus",┌────▼────────┐            ┌────────▼────────┐3. [Execução Rápida](#3-execução-rápida)

kubectl get pv,pvc -n unifiapay

### 2.2. Build e Publicação das Imagens com Versão e RM do Aluno

# Rancher

kubectl get pods -n cattle-system            "volumeMounts": [

docker ps --filter name=rancher

```Todas as imagens devem ser versionadas com o padrão `v1.<RM_do_aluno>`, neste caso: **v1.93744**



### Testar Transação PIX              {```bash



```powershell#### Build com Multi-Stage (para imagens menores e seguras)

# Usando arquivo JSON

curl -X POST http://localhost:30050/pix -H "Content-Type: application/json" -d @test-pix.json                "name": "config",



# Teste manualOs Dockerfiles já estão configurados com multi-stage build para otimização:

curl -X POST http://localhost:30050/pix -H "Content-Type: application/json" -d '{

  "chave_pix": "11999887766",                "mountPath": "/etc/prometheus/prometheus.yml",# 1. Criar ConfigMap com configuração do Prometheus│  UniFIAP    │            │   Monitoring    │4. [Documentação Técnica](#4-documentação-técnica)

  "valor": 50.00,

  "descricao": "Teste RM 93744"**Exemplo do Dockerfile da API Pagamentos:**

}'

```                "subPath": "prometheus.yml"



### Verificar Logs```dockerfile



```powershell# Stage 1: Build              }kubectl create configmap prometheus-config --from-file=monitoring/prometheus.yml -n unifiapay

# API de Pagamentos

kubectl logs -n unifiapay deployment/api-pagamentos-simple --tail 50 -fFROM python:3.11-slim AS builder



# Auditoria (liquidação)WORKDIR /app            ]

kubectl logs -n unifiapay deployment/auditoria-simple --tail 50 -f

COPY requirements.txt .

# Prometheus

kubectl logs -n unifiapay deployment/prometheus --tail 50RUN pip install --no-cache-dir -r requirements.txt          }│  Services   │            │     Stack       │5. [Evidências e Avaliação](#5-evidências-e-avaliação)



# Grafana

kubectl logs -n unifiapay deployment/grafana --tail 50

```# Stage 2: Runtime        ]



### Acessar ServiçosFROM python:3.11-slim



| Serviço | URL | Credenciais |WORKDIR /app      }# 2. Criar arquivo de patch para o Prometheus

|---------|-----|-------------|

| Frontend PIX | http://localhost:30082 | - |COPY --from=builder /usr/local/lib/python3.11/site-packages /usr/local/lib/python3.11/site-packages

| API Swagger | http://localhost:30050/docs | - |

| Auditoria | http://localhost:30051 | - |COPY app.py .    }

| Grafana | http://localhost:30300 | admin / admin |

| Prometheus | http://localhost:30090 | - |EXPOSE 5000

| Rancher | https://localhost:8443 | admin / unifiap123 |

CMD ["python", "app.py"]  }cat <<EOF > /tmp/prometheus-patch.json├─────────────┤            ├─────────────────┤6. [Troubleshooting](#6-troubleshooting)

---

```

## 5. Troubleshooting

}

### Pods não iniciam

#### Comandos de Build

```powershell

# Ver detalhesEOF{

kubectl describe pod <NOME_DO_POD> -n unifiapay

```bash

# Ver logs

kubectl logs <NOME_DO_POD> -n unifiapay# 1. Build da imagem api-pagamentos



# Reiniciar deploymentcd core/api-pagamentos

kubectl rollout restart deployment <NOME_DO_DEPLOYMENT> -n unifiapay

```docker build -t codecaman/unifiap-api-pagamentos:v1.93744 .# 2.3. Aplicar o patch no deployment do Prometheus  "spec": {│ API Pag     │            │ Prometheus      │



### Rancher não conecta



```powershell# 2. Build da imagem auditoria-servicekubectl patch deployment prometheus -n unifiapay --patch-file /tmp/prometheus-patch.json

# Verificar patch hostNetwork

kubectl get deployment cattle-cluster-agent -n cattle-system -o yaml | Select-String "hostNetwork"cd ../auditoria-service



# Aplicar patch se necessáriodocker build -t codecaman/unifiap-auditoria:v1.93744 .    "template": {

kubectl patch deployment cattle-cluster-agent -n cattle-system -p '{

  "spec": {

    "template": {

      "spec": {# 3. Build da imagem frontend-pix# 2.4. Aguardar o Prometheus reiniciar

        "hostNetwork": true

      }cd ../frontend-pix

    }

  }docker build -t codecaman/unifiap-frontend-pix:v1.93744 .kubectl rollout status deployment prometheus -n unifiapay      "spec": {│ Auditoria   │            │ Grafana         │---

}'



# Ver logs

kubectl logs -n cattle-system deployment/cattle-cluster-agent --tail 20# Voltar ao diretório raiz

```

cd ../..

### Grafana sem dados

```# 2.5. Recarregar a configuração do Prometheus        "volumes": [

```powershell

# Verificar kube-state-metrics

kubectl get pods -n unifiapay -l app=kube-state-metrics

#### Varredura de Vulnerabilidadessleep 15

# Verificar targets do Prometheus

curl http://localhost:30090/api/v1/targets



# Recarregar PrometheusExecute o Docker Scout para verificar vulnerabilidades:curl -X POST http://localhost:30090/-/reload          {│ Frontend    │            │ Node Exporter   │

curl -X POST http://localhost:30090/-/reload

```



### Limpar ambiente completo```bash```



```powershell# Analisar api-pagamentos

# Remover todos os recursos

kubectl delete -f k8s/unifiap-pay-spb.yamldocker scout cves codecaman/unifiap-api-pagamentos:v1.93744            "name": "config",

kubectl delete -f k8s/kube-state-metrics.yaml



# Parar Rancher

docker-compose -f docker-compose.rancher.yml down# Analisar auditoria-service**⏱️ Tempo estimado:** 30 segundos



# Remover namespacesdocker scout cves codecaman/unifiap-auditoria:v1.93744

kubectl delete namespace unifiapay --force --grace-period=0

kubectl delete namespace cattle-system --force --grace-period=0            "configMap": {└─────────────┘            └─────────────────┘## 1. Arquitetura da Solução e Contexto SPB



# Remover rede Docker# Analisar frontend-pix

docker network rm unifiap_net

```docker scout cves codecaman/unifiap-frontend-pix:v1.93744---



---```



## 📁 Estrutura do Projeto              "name": "prometheus-config"



```**Saída esperada (exemplo):**

unifiap-pay-spb/

├── core/```### PASSO 3: Configurar o Grafana

│   ├── api-pagamentos/          # Microsserviço de pagamentos

│   ├── auditoria-service/       # Microsserviço de liquidação✓ Provenance: SLSA Build Level 1

│   └── frontend-pix/            # Interface web

├── k8s/✓ No critical vulnerabilities detected            }```

│   ├── unifiap-pay-spb.yaml     # Manifesto principal

│   └── kube-state-metrics.yaml  # Métricas do K8s✓ 0 high severity vulnerabilities

├── monitoring/

│   ├── prometheus.yml           # Config do Prometheus✓ 2 medium severity vulnerabilitiesO Grafana precisa de um datasource (Prometheus) e um dashboard:

│   └── grafana/

│       └── dashboards/✓ 5 low severity vulnerabilities

│           └── unifiap-complete.json

├── scripts/```          }

│   └── import-grafana-dashboard.py

├── docker-compose.rancher.yml   # Rancher

├── test-pix.json                # Payload de teste

└── README.md                    # Este arquivo#### Publicação das Imagens no Docker Hub```bash

```



---

```bash# 3.1. Resetar a senha do admin do Grafana para 'admin'        ],### 1.1. Descrição do Projeto

## 📚 Recursos Importantes

# Login no Docker Hub

**Imagens Docker Hub:**

- codecaman/unifiap-api-pagamentos:v1.93744docker loginPOD_NAME=$(kubectl get pods -n unifiapay -l app=grafana -o jsonpath='{.items[0].metadata.name}')

- codecaman/unifiap-auditoria:v1.93744

- codecaman/unifiap-frontend-pix:v1.93744



**ConfigMap:**# Push das imagenskubectl exec -n unifiapay $POD_NAME -- grafana-cli admin reset-admin-password admin        "containers": [

- RESERVA_BANCARIA_SALDO: 1000000.00 (R$ 1 milhão)

- LIQUIDATION_MODE: continuousdocker push codecaman/unifiap-api-pagamentos:v1.93744

- MONITORING_INTERVAL: 15s

docker push codecaman/unifiap-auditoria:v1.93744

**Volume Compartilhado:**

- Path: /var/logs/api/instrucoes.logdocker push codecaman/unifiap-frontend-pix:v1.93744

- Função: Livro-Razão do SPB

- Compartilhado entre: api-pagamentos (write) + auditoria-service (read/update)```# 3.2. Aguardar 5 segundos          {## 📋 ComponentesEste projeto implementa uma **arquitetura de microsserviços moderna na Nuvem (Cloud Native)** para a UniFIAP Pay. O objetivo é simular um fluxo de pagamento PIX seguindo as regras do **Sistema de Pagamentos Brasileiro (SPB)**, que exige compensação e liquidação através do Banco Central (STR).



---



## 👨‍💻 Autor**Saída esperada:**sleep 5



**Renan Assi de Freitas**  ```

**RM:** 93744  

**FIAP** - Pós Tech Software ArchitectureThe push refers to repository [docker.io/codecaman/unifiap-api-pagamentos]            "name": "prometheus",



---v1.93744: digest: sha256:abc123... size: 1234



**🎉 Sistema completo e funcional!**```# 3.3. Importar datasource e dashboard automaticamente




**Repositórios Docker Hub:**python scripts/import-grafana-dashboard.py            "volumeMounts": [

- https://hub.docker.com/r/codecaman/unifiap-api-pagamentos

- https://hub.docker.com/r/codecaman/unifiap-auditoria```

- https://hub.docker.com/r/codecaman/unifiap-frontend-pix

              {

---

**Alternativa Manual (se o script Python falhar):**

### 2.3. Subindo o Rancher (Gerenciamento de Containers)

                "name": "config",### Microsserviços#### 🎯 Três Pilares do Desafio:

Para gerenciar os containers e clusters de forma visual, suba o Rancher localmente.

1. Acesse http://localhost:30300

#### Iniciar o Rancher

2. Login: `admin` / `admin`                "mountPath": "/etc/prometheus/prometheus.yml",

```bash

# Subir o container do Rancher usando docker-compose3. Vá em **Configuration (⚙️)** → **Data sources** → **Add data source**

docker-compose -f docker-compose.rancher.yml up -d

4. Selecione **Prometheus**                "subPath": "prometheus.yml"- **API Pagamentos** - Processa transações PIX e valida saldo de reserva- **🔒 Segurança:** Construir containers e redes isoladas

# Aguardar 60 segundos para inicialização

Start-Sleep -Seconds 605. Em **URL**, digite: `http://prometheus-service:9090`



# Verificar se o container está rodando6. Clique em **Save & Test**              }

docker ps --filter name=rancher

```7. Vá em **Dashboards (+)** → **Import**



**Saída esperada:**8. Clique em **Upload JSON file**            ]- **Auditoria Service** - Simula liquidação automática do BACEN (15s)- **⚙️ Orquestração:** Usar o Kubernetes para gerenciar a aplicação em escala

```

CONTAINER ID   IMAGE                    STATUS         PORTS9. Selecione: `monitoring/grafana/dashboards/unifiap-complete.json`

abc123def456   rancher/rancher:v2.12.3  Up 2 minutes   0.0.0.0:8080->80/tcp, 0.0.0.0:8443->443/tcp

```10. Escolha o datasource **Prometheus**          }



#### Acessar o Rancher11. Clique em **Import**



1. Acesse **https://localhost:8443** no navegador        ]- **Frontend PIX** - Interface web para operações- **💰 Regras de Negócio:** Aplicar a lógica da Reserva Bancária e Liquidação

2. Aceite o certificado self-signed (aviso de segurança)

3. Login: `admin`**⏱️ Tempo estimado:** 1 minuto (automático) ou 3 minutos (manual)

4. Senha: `unifiap123`

      }

#### Monitorar Recursos no Rancher

---

Use o painel do Rancher para:

    }

- Visualizar todos os **Pods** do namespace `unifiapay`

- Monitorar **Deployments** e **Services**### PASSO 4: Deploy do Rancher

- Acompanhar logs em tempo real

- Verificar uso de recursos (CPU/Memória)  }

- Gerenciar escala de réplicas

O Rancher é a ferramenta de gerenciamento visual dos clusters Kubernetes:

---

}### Monitoramento### 1.2. Microsserviços e Responsabilidades

### 2.4. Deploy no Kubernetes

```bash

#### Verificar e Atualizar os YAMLs

# 4.1. Subir o container do RancherEOF

**IMPORTANTE:** Certifique-se de que os arquivos em `./k8s` apontam para suas imagens do Docker Hub com seu RM (93744).

docker-compose -f docker-compose.rancher.yml up -d

Verifique o arquivo `k8s/unifiap-pay-spb.yaml`:

- **Prometheus** - Coleta de métricas

```yaml

# Exemplo - api-pagamentos deployment# 4.2. Aguardar 60 segundos para o Rancher inicializar

spec:

  containers:sleep 60# 3. Aplicar o patch no Prometheus

  - name: api-pagamentos

    image: codecaman/unifiap-api-pagamentos:v1.93744  # ← Verificar tag

```

# 4.3. Acesse https://localhost:8443 no navegadorkubectl patch deployment prometheus -n unifiapay --patch-file /tmp/prometheus-patch.json- **Grafana** - Visualização e dashboards| 🏗️ Microsserviço | 🎭 Função Principal (SPB) | 💻 Responsabilidades Técnicas |

#### Aplicar os Manifestos

# Login: admin

```bash

# 1. Aplicar todos os recursos (Namespace, ConfigMaps, Deployments, Services)# Senha: unifiap123

kubectl apply -f k8s/unifiap-pay-spb.yaml

```

# 2. Aplicar kube-state-metrics para coletar métricas do Kubernetes

kubectl apply -f k8s/kube-state-metrics.yaml# 4. Aguardar o Prometheus reiniciar- **Node Exporter** - Métricas do sistema|-------------------|---------------------------|-------------------------------|



# 3. Verificar se todos os pods foram criados**⏱️ Tempo estimado:** 1-2 minutos

kubectl get pods -n unifiapay

kubectl rollout status deployment prometheus -n unifiapay

# Aguarde até que TODOS os 7 pods estejam com status "Running" (1/1)

```---



**Pods esperados:**| **api-pagamentos** | Simula o **Banco Originador** (UniFIAP Pay)<br/>Garante reserva bancária suficiente no BACEN | • Consultar `RESERVA_BANCARIA_SALDO`<br/>• Validar: `Valor PIX ≤ Reserva`<br/>• Registrar instrução com status `AGUARDANDO_LIQUIDACAO` |

- `api-pagamentos-simple-xxxxxxxxx-xxxxx` (Running 1/1)

- `auditoria-simple-xxxxxxxxx-xxxxx` (Running 1/1)### PASSO 5: Importar o Cluster Kubernetes no Rancher

- `frontend-pix-simple-xxxxxxxxx-xxxxx` (Running 1/1)

- `grafana-xxxxxxxxx-xxxxx` (Running 1/1)# 5. Recarregar configuração do Prometheus

- `prometheus-xxxxxxxxx-xxxxx` (Running 1/1)

- `node-exporter-xxxxxxxxx-xxxxx` (Running 1/1)Agora vamos conectar o cluster Kubernetes local ao Rancher:

- `kube-state-metrics-xxxxxxxxx-xxxxx` (Running 1/1)

sleep 15### Gerenciamento| **auditoria-service** | Simula o **Sistema de Liquidação** (BACEN/STR)<br/>Processa e liquida os pagamentos | • Monitorar arquivo `/var/logs/api/instrucoes.log`<br/>• Atualizar status para `LIQUIDADO`<br/>• Executar via CronJob a cada 6h |

#### Configurar o Prometheus

#### 5.1. Via Interface Web

```bash

# 1. Criar o ConfigMap com a configuração do Prometheuscurl -X POST http://localhost:30090/-/reload

kubectl create configmap prometheus-config --from-file=monitoring/prometheus.yml -n unifiapay

1. Acesse **https://localhost:8443**

# 2. Aplicar patch para montar o ConfigMap no deployment

kubectl patch deployment prometheus -n unifiapay -p '{2. Faça login com `admin` / `unifiap123````- **Rancher** - Orquestração e gerenciamento de clusters Kubernetes

  "spec": {

    "template": {3. No menu lateral, clique em **Cluster Management**

      "spec": {

        "volumes": [4. Clique no botão **Import Existing** (canto superior direito)

          {

            "name": "config",5. Selecione **Generic** como tipo de cluster

            "configMap": {

              "name": "prometheus-config"6. Em **Cluster Name**, digite: `docker-desktop`### Passo 3: Configurar Grafana### 1.3. Arquitetura Visual

            }

          }7. Clique em **Create**

        ],

        "containers": [8. Na próxima tela, você verá 3 comandos. **COPIE O SEGUNDO** (que começa com `curl --insecure...`)

          {

            "name": "prometheus",

            "volumeMounts": [

              {#### 5.2. Via Terminal```bash## 🚀 Quick Start

                "name": "config",

                "mountPath": "/etc/prometheus/prometheus.yml",

                "subPath": "prometheus.yml"

              }```bash# 1. Resetar senha do admin do Grafana para 'admin'

            ]

          }# 5.2.1. Cole o comando copiado do Rancher (exemplo abaixo - USE O SEU TOKEN):

        ]

      }curl --insecure -sfL https://localhost:8443/v3/import/SEU_TOKEN_AQUI.yaml | kubectl apply -f -POD_NAME=$(kubectl get pods -n unifiapay -l app=grafana -o jsonpath='{.items[0].metadata.name}')#### 🏗️ Pods dos Serviços

    }

  }

}'

# 5.2.2. Aguardar 15 segundos para os pods do cattle-system subiremkubectl exec -n unifiapay $POD_NAME -- grafana-cli admin reset-admin-password admin

# 3. Aguardar o Prometheus reiniciar

kubectl rollout status deployment prometheus -n unifiapaysleep 15



# 4. Recarregar a configuração do Prometheus### Pré-requisitos<img width="1536" height="1024" alt="services" src="https://github.com/user-attachments/assets/da38336e-13d9-4eb0-8262-3fb2555e3c24" />

Start-Sleep -Seconds 15

curl -X POST http://localhost:30090/-/reload# 5.2.3. Aplicar patch para permitir acesso ao localhost

```

kubectl patch deployment cattle-cluster-agent -n cattle-system -p '{"spec":{"template":{"spec":{"hostNetwork":true}}}}'# 2. Aguardar alguns segundos

#### Configurar o Grafana



```bash

# 1. Resetar a senha do admin do Grafana para 'admin'# 5.2.4. Verificar se o agent está rodandosleep 5- Docker Desktop com Kubernetes habilitado

$POD_NAME = kubectl get pods -n unifiapay -l app=grafana -o jsonpath='{.items[0].metadata.name}'

kubectl exec -n unifiapay $POD_NAME -- grafana-cli admin reset-admin-password adminkubectl get pods -n cattle-system



# 2. Aguardar 5 segundos

Start-Sleep -Seconds 5

# 5.2.5. Volte ao navegador e aguarde 1-2 minutos

# 3. Importar datasource e dashboard automaticamente

python scripts/import-grafana-dashboard.py# O cluster "docker-desktop" mudará de status "Provisioning" para "Active"# 3. Importar datasource e dashboard automaticamente via Python- kubectl configurado#### 💾 Volume Compartilhado (Livro-Razão)

```

```

**Saída esperada:**

```python scripts/import-grafana-dashboard.py

🔧 Configurando Grafana...

✅ Datasource Prometheus criado com sucesso!**⏱️ Tempo estimado:** 2-3 minutos

✅ Dashboard importado com sucesso!

📊 URL: http://localhost:30300/d/unifiap-spb-complete/unifiap-pay-spb-sistema-completo- make (GNU Make)<img width="1536" height="1024" alt="pvc" src="https://github.com/user-attachments/assets/234c2f85-29ac-46cc-acb1-99f8eb896f22" />

```

---

#### Importar Cluster no Rancher

# OU manualmente via Web UI:

1. Acesse **https://localhost:8443**

2. Faça login com `admin` / `unifiap123`## ✅ Verificação Final

3. No menu lateral, clique em **Cluster Management**

4. Clique no botão **Import Existing** (canto superior direito)# - Acesse http://localhost:30300- curl

5. Selecione **Generic** como tipo de cluster

6. Em **Cluster Name**, digite: `docker-desktop`Execute os comandos abaixo para confirmar que tudo está funcionando:

7. Clique em **Create**

8. **COPIE O SEGUNDO COMANDO** (que começa com `curl --insecure...`)# - Login: admin / admin



```bash```bash

# Exemplo do comando (USE O SEU TOKEN):

curl --insecure -sfL https://localhost:8443/v3/import/SEU_TOKEN_AQUI.yaml | kubectl apply -f -# Verificar todos os pods do UniFIAP# - Configuration (⚙️) → Data sources → Add data source → Prometheus#### ⚙️ ConfigMap e Secrets



# Aguardar 15 segundoskubectl get pods -n unifiapay

Start-Sleep -Seconds 15

# Resultado esperado: 7 pods com status Running (1/1)# - URL: http://prometheus-service:9090 → Save & Test

# Aplicar patch para permitir acesso ao localhost

kubectl patch deployment cattle-cluster-agent -n cattle-system -p '{

  "spec": {

    "template": {# Verificar pods do Rancher# - Dashboards (+) → Import → Upload JSON file### 1. Deploy do Sistema<img width="1536" height="1024" alt="configmap" src="https://github.com/user-attachments/assets/618ee716-d992-4d53-a3a1-dbbd7d8b6e23" />

      "spec": {

        "hostNetwork": truekubectl get pods -n cattle-system

      }

    }# Resultado esperado: 1 pod cattle-cluster-agent Running# - Selecione: monitoring/grafana/dashboards/unifiap-complete.json

  }

}'



# Verificar se o agent está rodando# Verificar services# - Import

kubectl get pods -n cattle-system

```kubectl get svc -n unifiapay



**Aguarde 1-2 minutos** - O cluster "docker-desktop" mudará de status **"Provisioning"** para **"Active"** no Rancher.# Resultado esperado: 6 services com portas NodePort```



---



## 3. Evidências e Resultados# Testar transação PIX```bash#### 🌐 Rede Docker Customizada



### 3.1. Etapa 1: Docker e Imagem Segura (1,5 pts)curl -X POST http://localhost:30050/pix \



**Objetivo:** Demonstrar a criação de imagens Docker seguras, otimizadas e versionadas.  -H "Content-Type: application/json" \### Passo 4: Deploy do Rancher



#### Evidência 1.1: Build Multi-Stage  -d @test-pix.json



**Comando:**# Resultado esperado: JSON com "sucesso": true e status "AGUARDANDO_LIQUIDACAO"# Deploy completo do UniFIAP Pay SPB<img width="1536" height="1024" alt="network" src="https://github.com/user-attachments/assets/186a33bc-5b7a-4d0e-9ac8-e96bbe3ec05e" />

```bash

cd core/api-pagamentos```

docker build -t codecaman/unifiap-api-pagamentos:v1.93744 .

``````bash



**Print esperado:**---

```

[+] Building 45.3s (12/12) FINISHED# 1. Subir o container do Ranchermake deploy

=> [builder 1/4] FROM docker.io/library/python:3.11-slim

=> [builder 2/4] WORKDIR /app## 🏗️ Arquitetura do Sistema

=> [builder 3/4] COPY requirements.txt .

=> [builder 4/4] RUN pip install --no-cache-dir -r requirements.txtdocker-compose -f docker-compose.rancher.yml up -d

=> [stage-1 1/3] FROM docker.io/library/python:3.11-slim

=> [stage-1 2/3] COPY --from=builder /usr/local/lib/python3.11/site-packages### Camada de Gerenciamento

=> [stage-1 3/3] COPY app.py .

=> exporting to image- **Rancher** (https://localhost:8443) - Interface web para gerenciar o cluster Kubernetes---

=> => naming to docker.io/codecaman/unifiap-api-pagamentos:v1.93744

```



**📸 Print obrigatório:** Capturar tela mostrando o build multi-stage completo.### Camada de Aplicação (Microsserviços)# 2. Aguardar 60 segundos para o Rancher inicializar completamente



#### Evidência 1.2: Push para Docker Hub- **API Pagamentos** - Processa transações PIX e valida saldo de reserva bancária



**Comando:**- **Auditoria Service** - Simula liquidação automática do BACEN a cada 15 segundossleep 60# Verificar status

```bash

docker push codecaman/unifiap-api-pagamentos:v1.93744- **Frontend PIX** - Interface web para realizar transações

docker push codecaman/unifiap-auditoria:v1.93744

docker push codecaman/unifiap-frontend-pix:v1.93744

```

### Camada de Observabilidade (Monitoramento)

**Print esperado:**

```- **Prometheus** - Coleta e armazena métricas do sistema e Kubernetes# 3. Acessar https://localhost:8443make status## 2. Estrutura do Projeto

The push refers to repository [docker.io/codecaman/unifiap-api-pagamentos]

v1.93744: digest: sha256:7a8b9c1d2e3f4g5h6i7j8k9l0m1n2o3p4q5r6s7t8u9v size: 1234- **Grafana** - Visualização de métricas através de dashboards

```

- **Node Exporter** - Coleta métricas do sistema operacional (CPU, memória, disco)# Login: admin / unifiap123

**📸 Print obrigatório:** Capturar tela mostrando os 3 pushes bem-sucedidos com a tag v1.93744.

- **Kube State Metrics** - Coleta métricas dos recursos do Kubernetes (pods, deployments, etc)

#### Evidência 1.3: Varredura de Vulnerabilidades

``````

**Comando:**

```bash---

docker scout cves codecaman/unifiap-api-pagamentos:v1.93744

docker scout cves codecaman/unifiap-auditoria:v1.93744

docker scout cves codecaman/unifiap-frontend-pix:v1.93744

```## 📦 Componentes



**Print esperado:**### Passo 5: Importar Cluster no Rancher```

```

✓ Provenance: SLSA Build Level 1### Microsserviços

✓ Image: codecaman/unifiap-api-pagamentos:v1.93744

✓ Platform: linux/amd64



  Target  │  codecaman/unifiap-api-pagamentos:v1.93744| Componente | Porta | Tecnologia | Função |

  Digest  │  sha256:7a8b9c1d2e...

  |------------|-------|------------|--------|#### Via Web UI:### 2. Iniciar Rancher📁 unifiap-pay-spb/

  0 critical vulnerabilities

  0 high severity vulnerabilities| **API Pagamentos** | 30050 | Python/Flask | Valida saldo e registra instruções PIX |

  2 medium severity vulnerabilities

  5 low severity vulnerabilities| **Auditoria Service** | 30051 | Python/Flask | Monitora e liquida transações |

```

| **Frontend PIX** | 30082 | HTML/CSS/JS + Nginx | Interface web do usuário |

**📸 Print obrigatório:** Capturar tela mostrando ausência de vulnerabilidades críticas (0 critical, 0 high).

1. Acesse **https://localhost:8443**├── 🐳 api-pagamentos/              # Microsserviço da API

**✅ Checklist Etapa 1:**

- [ ] Print do `docker build` mostrando multi-stage### Monitoramento

- [ ] Print do `docker push` com tag v1.93744

- [ ] Print do `docker scout` comprovando ausência de vulnerabilidades críticas2. Login: **admin / unifiap123**



---| Componente | Porta | Função |



### 3.2. Etapa 2: Rede, Comunicação e Segmentação (2,5 pts)|------------|-------|--------|3. **Cluster Management** → **Import Existing**```bash│   ├── app.py                     # API Flask com validação SPB



**Objetivo:** Demonstrar isolamento de rede, comunicação entre containers e leitura de variáveis de ambiente.| **Prometheus** | 30090 | Coleta de métricas |



#### Evidência 2.1: Rede Docker Customizada| **Grafana** | 30300 | Visualização de dashboards |4. Selecione **Generic**



**Comando:**| **Node Exporter** | 30100 | Métricas do sistema |

```bash

docker network inspect unifiap_net| **Kube State Metrics** | 8080 (interno) | Métricas do Kubernetes |5. **Cluster Name**: `docker-desktop`# Subir Rancher│   ├── requirements.txt           # Dependências Python

```



**Print esperado:**

```json### Gerenciamento6. Clique em **Create**

[

    {

        "Name": "unifiap_net",

        "Id": "abc123def456...",| Componente | Portas | Função |7. Na próxima tela, **copie o segundo comando** (curl --insecure...)make rancher-up│   └── Dockerfile                 # Multi-stage build seguro

        "Created": "2025-11-13T...",

        "Driver": "bridge",|------------|--------|--------|

        "IPAM": {

            "Driver": "default",| **Rancher** | 8080 (HTTP), 8443 (HTTPS) | Gerenciamento de clusters |

            "Config": [

                {

                    "Subnet": "172.25.0.0/24",

                    "Gateway": "172.25.0.1"---#### Via Terminal:├── 🔍 auditoria-service/           # Microsserviço de auditoria

                }

            ]

        },

        "Containers": {}## 🔗 URLs de Acesso

    }

]

```

| Serviço | URL | Credenciais | Descrição |```bash# Aguardar 60 segundos e acessar:│   ├── app.py                     # Sistema de liquidação BACEN

**📸 Print obrigatório:** Capturar tela mostrando o bloco IP customizado `172.25.0.0/24`.

|---------|-----|-------------|-----------|

#### Evidência 2.2: Comunicação Entre Containers

| **Frontend PIX** | http://localhost:30082 | - | Realizar transações PIX |# Exemplo do comando fornecido pelo Rancher (substitua pelo seu token):

**Comando (dentro do Kubernetes):**

```bash| **API Swagger** | http://localhost:30050/docs | - | Documentação interativa da API |

# Verificar comunicação entre api-pagamentos e auditoria-service

kubectl exec -n unifiapay deployment/api-pagamentos-simple -- curl -s http://auditoria-service:5001/health| **Auditoria** | http://localhost:30051 | - | Status do serviço de liquidação |curl --insecure -sfL https://localhost:8443/v3/import/SEU_TOKEN_AQUI.yaml | kubectl apply -f -# https://localhost:8443│   ├── requirements.txt           # Dependências mínimas



# Verificar acesso ao Prometheus| **Grafana** | http://localhost:30300 | admin / admin | Dashboards de monitoramento |

kubectl exec -n unifiapay deployment/api-pagamentos-simple -- curl -s http://prometheus-service:9090/-/healthy

```| **Prometheus** | http://localhost:30090 | - | Métricas e targets |



**Print esperado:**| **Rancher** | https://localhost:8443 | admin / unifiap123 | Gerenciamento de clusters |

```json

{| **Dashboard Local** | Abrir `dashboard.html` | - | Painel de acesso rápido |# Aguardar pods do cattle-system subirem# Login: admin / unifiap123│   └── Dockerfile                 # Multi-stage build seguro

  "status": "healthy",

  "service": "auditoria-service",

  "timestamp": "2025-11-13T..."

}---sleep 15

```



**📸 Print obrigatório:** Capturar tela mostrando comunicação bem-sucedida entre pods.

## 🛠️ Comandos Úteis```├── 🌐 frontend-pix/                # Interface Web Moderna

#### Evidência 2.3: Leitura de Variáveis de Ambiente



**Comando:**

```bash### Verificar Status# Aplicar patch hostNetwork para permitir acesso ao localhost

# Ver logs da API mostrando leitura do ConfigMap

kubectl logs -n unifiapay deployment/api-pagamentos-simple --tail 20

```

```bashkubectl patch deployment cattle-cluster-agent -n cattle-system -p '{"spec":{"template":{"spec":{"hostNetwork":true}}}}'│   ├── index.html                 # UI responsiva Bootstrap

**Print esperado:**

```# Status de todos os pods

INFO:root:Iniciando API de Pagamentos...

INFO:root:RESERVA_BANCARIA_SALDO carregado: R$ 1000000.00kubectl get pods -n unifiapay

INFO:root:Servidor rodando na porta 5000

INFO:root:Aguardando requisições PIX...

```

# Status detalhado de um pod específico# Verificar status### 3. Importar Cluster no Rancher│   ├── app.js                     # Lógica JavaScript

**📸 Print obrigatório:** Capturar tela mostrando logs da API lendo `RESERVA_BANCARIA_SALDO` do ConfigMap.

kubectl describe pod <NOME_DO_POD> -n unifiapay

**✅ Checklist Etapa 2:**

- [ ] Print do `docker network inspect` mostrando subnet 172.25.0.0/24kubectl get pods -n cattle-system

- [ ] Print do `curl` ou `ping` mostrando comunicação entre containers

- [ ] Print dos logs mostrando leitura de `RESERVA_BANCARIA_SALDO`# Status dos deployments



---kubectl get deployments -n unifiapay│   ├── style.css                  # Estilos Glass Morphism



### 3.3. Etapa 3: Kubernetes – Estrutura, Escala e Deploy (3,0 pts)



**Objetivo:** Demonstrar deploy no Kubernetes, escala de réplicas e compartilhamento de volume.# Status dos services# Aguardar 1-2 minutos e o cluster ficará Active no Rancher



#### Evidência 3.1: Pods Rodando com Réplicaskubectl get svc -n unifiapay



**Comando:**``````bash│   ├── nginx.conf                 # Configuração Nginx

```bash

# Verificar todos os pods# Status do Rancher

kubectl get pods -n unifiapay -o wide

```kubectl get pods -n cattle-system



**Print esperado:**docker ps --filter name=rancher

```

NAME                                    READY   STATUS    RESTARTS   AGE   NODE```## 🏗️ Arquitetura# Ver instruções de importação│   ├── Dockerfile                 # Container web otimizado

api-pagamentos-simple-xxxxxxxxx-xxxxx   1/1     Running   0          5m    docker-desktop

api-pagamentos-simple-xxxxxxxxx-yyyyy   1/1     Running   0          2m    docker-desktop

auditoria-simple-xxxxxxxxx-xxxxx        1/1     Running   0          5m    docker-desktop

frontend-pix-simple-xxxxxxxxx-xxxxx     1/1     Running   0          5m    docker-desktop### Ver Logs

prometheus-xxxxxxxxx-xxxxx              1/1     Running   0          5m    docker-desktop

grafana-xxxxxxxxx-xxxxx                 1/1     Running   0          5m    docker-desktop

node-exporter-xxxxxxxxx-xxxxx           1/1     Running   0          5m    docker-desktop

kube-state-metrics-xxxxxxxxx-xxxxx      1/1     Running   0          5m    docker-desktop```bash```make rancher-import│   └── README.md                  # Documentação frontend

```

# Logs da API de Pagamentos

**📸 Print obrigatório:** Capturar tela mostrando a API com **2 réplicas** rodando.

kubectl logs -n unifiapay -l app=api-pagamentos-simple --tail 50 -f┌─────────────────────────────────────────────────────────┐

#### Evidência 3.2: Escala Horizontal



**Comando:**

```bash# Logs do Serviço de Auditoria│                  Rancher Management                      │├── 🚜 rancher-setup/               # Configuração Rancher

# Escalar api-pagamentos para 3 réplicas

kubectl scale deployment api-pagamentos-simple -n unifiapay --replicas=3kubectl logs -n unifiapay -l app=auditoria-simple --tail 50 -f



# Aguardar e verificar│              https://localhost:8443                      │

kubectl get pods -n unifiapay -l app=api-pagamentos-simple -w

```# Logs do Prometheus



**Print esperado:**kubectl logs -n unifiapay -l app=prometheus --tail 50│                  admin / unifiap123                      │# Seguir os passos exibidos para importar o cluster docker-desktop│   ├── docker-compose.yml         # Stack completa

```

NAME                                    READY   STATUS    RESTARTS   AGE

api-pagamentos-simple-xxxxxxxxx-xxxxx   1/1     Running   0          10m

api-pagamentos-simple-xxxxxxxxx-yyyyy   1/1     Running   0          7m# Logs do Grafana└────────────────────┬────────────────────────────────────┘

api-pagamentos-simple-xxxxxxxxx-zzzzz   1/1     Running   0          5s   ← Nova réplica

```kubectl logs -n unifiapay -l app=grafana --tail 50



**📸 Print obrigatório:** Capturar tela mostrando aumento de réplicas (2 → 3).                     │```│   ├── traefik.yml                # Load balancer



#### Evidência 3.3: Volume Compartilhado (Livro-Razão)# Logs do Rancher Agent



**Comando:**kubectl logs -n cattle-system -l app=cattle-cluster-agent --tail 50        ┌────────────▼─────────────┐

```bash

# Logs de dois pods da API escrevendo no mesmo arquivo```

$POD1 = kubectl get pods -n unifiapay -l app=api-pagamentos-simple -o jsonpath='{.items[0].metadata.name}'

$POD2 = kubectl get pods -n unifiapay -l app=api-pagamentos-simple -o jsonpath='{.items[1].metadata.name}'        │   Kubernetes Cluster     ││   ├── prometheus.yml             # Monitoramento



kubectl exec -n unifiapay $POD1 -- tail -5 /var/logs/api/instrucoes.log### Reiniciar Serviços

kubectl exec -n unifiapay $POD2 -- tail -5 /var/logs/api/instrucoes.log

        │    (Docker Desktop)      │

# Logs do pod de auditoria lendo o mesmo arquivo

$POD_AUDIT = kubectl get pods -n unifiapay -l app=auditoria-simple -o jsonpath='{.items[0].metadata.name}'```bash

kubectl exec -n unifiapay $POD_AUDIT -- tail -5 /var/logs/api/instrucoes.log

```# Reiniciar todos os serviços        │      v1.33.1+k3s1        │## 🔗 Acessos│   ├── grafana/                   # Dashboards



**Print esperado (arquivo compartilhado):**kubectl rollout restart deployment -n unifiapay

```

2025-11-13 15:30:25|76c7d24c-2745-4eb6-bb1b-45725e2c253a|11999887766|10.50|AGUARDANDO_LIQUIDACAO        └────────────┬─────────────┘

2025-11-13 15:31:40|abc123def456...|11988776655|25.00|AGUARDANDO_LIQUIDACAO

2025-11-13 15:32:15|def456ghi789...|11977665544|50.00|LIQUIDADO# Reiniciar serviço específico

```

kubectl rollout restart deployment api-pagamentos-simple -n unifiapay                     ││   ├── deploy.sh/.bat             # Scripts automação

**📸 Print obrigatório:** Capturar tela mostrando os 3 pods (2 da API + 1 da Auditoria) lendo/escrevendo no **mesmo arquivo** `instrucoes.log`.

kubectl rollout restart deployment auditoria-simple -n unifiapay

#### Evidência 3.4: Monitoramento Contínuo (Substituindo CronJob)

kubectl rollout restart deployment prometheus -n unifiapay     ┌───────────────┴───────────────┐

**Comando:**

```bashkubectl rollout restart deployment grafana -n unifiapay

# Ver logs da auditoria processando transações a cada 15 segundos

kubectl logs -n unifiapay deployment/auditoria-simple --tail 30 -f     │                               │| Serviço | URL | Credenciais |│   └── README.md                  # Guia Rancher

```

# Verificar status do rollout

**Print esperado:**

```kubectl rollout status deployment <NOME_DO_DEPLOYMENT> -n unifiapay┌────▼────────┐            ┌────────▼────────┐

INFO:root:Iniciando Serviço de Auditoria e Liquidação...

INFO:root:Modo de liquidação: continuous```

INFO:root:Intervalo de monitoramento: 15s

INFO:root:Monitorando arquivo: /var/logs/api/instrucoes.log│  UniFIAP    │            │   Monitoring    │|---------|-----|-------------|├── ☸️ k8s/                         # Manifests Kubernetes



INFO:root:[2025-11-13 15:30:40] Iniciando ciclo de liquidação...### Limpeza Completa

INFO:root:Encontradas 2 transações aguardando liquidação

INFO:root:Liquidando transação: 76c7d24c-2745-4eb6-bb1b-45725e2c253a│  Services   │            │     Stack       │

INFO:root:Liquidando transação: abc123def456...

INFO:root:✅ Liquidação concluída. 2 transações processadas.```bash



INFO:root:[2025-11-13 15:30:55] Iniciando ciclo de liquidação...# Remover todos os recursos do UniFIAP├─────────────┤            ├─────────────────┤| **Frontend PIX** | http://localhost:30082 | - |│   ├── 00-namespace.yaml          # Namespace unifiapay

INFO:root:Nenhuma transação pendente neste ciclo.

```kubectl delete -f k8s/unifiap-pay-spb.yaml



**📸 Print obrigatório:** Capturar tela mostrando logs da auditoria processando transações automaticamente.kubectl delete -f k8s/kube-state-metrics.yaml│ API Pag     │            │ Prometheus      │



**NOTA:** Este projeto utiliza **monitoramento contínuo** ao invés de CronJob, pois o serviço de auditoria roda 24/7 verificando novas transações a cada 15 segundos. Esta abordagem é mais adequada para liquidação em tempo real do SPB.



**✅ Checklist Etapa 3:**# Parar e remover Rancher (mantém volumes)│ Auditoria   │            │ Grafana         │| **API Swagger** | http://localhost:30050/docs | - |│   ├── 01-configmap.yaml          # Configurações (Reserva Bancária)

- [ ] Print do `kubectl get pods` mostrando API com 2 réplicas

- [ ] Print do `kubectl scale` e subsequente `kubectl get pods` mostrando aumento de réplicasdocker-compose -f docker-compose.rancher.yml down

- [ ] Print de logs dos 2 pods da API e 1 pod da Auditoria lendo/escrevendo no mesmo `instrucoes.log`

- [ ] Print dos logs da auditoria mostrando processamento automático│ Frontend    │            │ Node Exporter   │



---# Remover Rancher E SEUS DADOS (CUIDADO!)



### 3.4. Etapa 4: Kubernetes – Segurança, Observação e Operação (2,0 pts)docker-compose -f docker-compose.rancher.yml down -v│             │            │ Kube-State      │| **Auditoria** | http://localhost:30051 | - |│   ├── 02-secret.yaml             # Secrets (PIX keys)



**Objetivo:** Demonstrar práticas de segurança, observabilidade e controle de acesso.



#### Evidência 4.1: Limites de Recursos (CPU/Memória)# Remover namespace do Rancher (se necessário)└─────────────┘            └─────────────────┘



**Comando:**kubectl delete namespace cattle-system --force --grace-period=0

```bash

# Verificar uso de recursos de todos os pods```| **Grafana** | http://localhost:30300 | admin/admin |│   ├── 03-pvc.yaml               # Volume compartilhado

kubectl top pods -n unifiapay

```# Limpar ConfigMaps



**Print esperado:**kubectl delete configmap prometheus-config -n unifiapay

```

NAME                                    CPU(cores)   MEMORY(bytes)kubectl delete configmap grafana-dashboards -n unifiapay

api-pagamentos-simple-xxxxxxxxx-xxxxx   45m          128Mi

api-pagamentos-simple-xxxxxxxxx-yyyyy   38m          115Mikubectl delete configmap grafana-datasources -n unifiapay## 📦 Componentes| **Prometheus** | http://localhost:30090 | - |│   ├── 04-rbac.yaml              # Permissões RBAC restritas

auditoria-simple-xxxxxxxxx-xxxxx        15m          64Mi

frontend-pix-simple-xxxxxxxxx-xxxxx     8m           32Mi```

prometheus-xxxxxxxxx-xxxxx              120m         256Mi

grafana-xxxxxxxxx-xxxxx                 85m          198Mi

node-exporter-xxxxxxxxx-xxxxx           12m          45Mi

kube-state-metrics-xxxxxxxxx-xxxxx      25m          78Mi---

```

### Microsserviços| **Rancher** | https://localhost:8443 | admin/unifiap123 |│   ├── 05-api-pagamentos-deployment.yaml

**📸 Print obrigatório:** Capturar tela mostrando limites de CPU/Memória aplicados e em uso.

## 🧪 Testes

#### Evidência 4.2: SecurityContext Configurado

- **API Pagamentos** - Processa transações PIX e valida saldo de reserva bancária

**Comando:**

```bash### Teste de Transação PIX

# Ver configuração de segurança da API

kubectl get deployment api-pagamentos-simple -n unifiapay -o yaml | Select-String -Pattern "securityContext" -Context 5- **Auditoria Service** - Simula liquidação automática do BACEN (intervalo de 15s)│   ├── 06-api-pagamentos-service.yaml

```

#### Usando arquivo JSON (recomendado):

**Print esperado:**

```yaml- **Frontend PIX** - Interface web para realizar operações PIX

spec:

  containers:```bash

  - name: api-pagamentos

    image: codecaman/unifiap-api-pagamentos:v1.93744curl -X POST http://localhost:30050/pix \## 📊 Testes│   ├── 07-auditoria-service-deployment.yaml

    securityContext:

      runAsNonRoot: true  -H "Content-Type: application/json" \

      runAsUser: 1000

      readOnlyRootFilesystem: false  -d @test-pix.json### Monitoramento

      allowPrivilegeEscalation: false

      capabilities:```

        drop:

        - ALL- **Prometheus** - Coleta e armazena métricas do sistema│   ├── 08-cronjob.yaml           # CronJob liquidação (6h)

```

**Resposta esperada:**

**📸 Print obrigatório:** Capturar tela mostrando `runAsNonRoot: true`, `runAsUser: 1000`, `allowPrivilegeEscalation: false`.

```json- **Grafana** - Visualização de métricas com dashboards

#### Evidência 4.3: Bloqueio de Deploy Inseguro

{

**Comando (criar pod inseguro):**

```bash  "instrucao_id": "uuid-gerado-automaticamente",- **Node Exporter** - Métricas do host/sistema operacional### Testar Transação PIX│   └── 09-network-policy.yaml    # Políticas de rede

# Tentar criar pod com privilégios elevados

kubectl run test-insecure --image=nginx -n unifiapay --overrides='{  "mensagem": "PIX registrado e aguardando liquidação pelo BACEN",

  "spec": {

    "containers": [{  "status": "AGUARDANDO_LIQUIDACAO",- **Kube State Metrics** - Métricas dos recursos do Kubernetes

      "name": "nginx",

      "image": "nginx",  "sucesso": true,

      "securityContext": {

        "privileged": true  "timestamp": "2025-11-13T...",├── 🐳 docker/                      # Configurações Docker

      }

    }]  "valor": "10.5"

  }

}'}### Gerenciamento



# Verificar se foi bloqueado (depende de PodSecurityPolicy ou Admission Controller)```

kubectl describe pod test-insecure -n unifiapay

```- **Rancher** - Orquestração e gerenciamento centralizado de clusters Kubernetes```bash│   ├── docker-compose.yml        # Orquestração local



**Print esperado (se houver policy ativa):**#### Teste manual com valores personalizados:

```

Error from server (Forbidden): pods "test-insecure" is forbidden: 

violates PodSecurity "restricted:latest": 

privileged (container "nginx" must not set securityContext.privileged=true)```bash

```

curl -X POST http://localhost:30050/pix \## 🔗 Acessos# Executar transação de teste│   ├── .env                      # Variáveis de ambiente

**NOTA:** O Docker Desktop Kubernetes não tem PodSecurityPolicy habilitado por padrão. Para demonstrar este requisito, você pode:

1. Configurar um Admission Controller personalizado  -H "Content-Type: application/json" \

2. Usar Rancher Policies

3. Documentar a configuração de segurança mesmo sem bloqueio automático  -d '{



**📸 Print obrigatório:** Capturar tela mostrando tentativa de deploy inseguro e descrição do pod.    "chave_pix": "11999887766",



#### Evidência 4.4: Permissões de ServiceAccount    "valor": 50.00,| Serviço | URL | Credenciais | Descrição |make test│   └── pix.key                   # Chave PIX simulada



**Comando:**    "descricao": "Pagamento de teste"

```bash

# Verificar permissões da ServiceAccount padrão  }'|---------|-----|-------------|-----------|

kubectl auth can-i create pods --as=system:serviceaccount:unifiapay:default -n unifiapay

kubectl auth can-i delete deployments --as=system:serviceaccount:unifiapay:default -n unifiapay```

kubectl auth can-i get pods --as=system:serviceaccount:unifiapay:default -n unifiapay

```| **Frontend PIX** | http://localhost:30082 | - | Interface para transações PIX |```├── 🔧 scripts/                     # Automação



**Print esperado:**### Verificar Métricas do Prometheus

```

no   ← create pods (negado)| **API Swagger** | http://localhost:30050/docs | - | Documentação interativa da API |

no   ← delete deployments (negado)

yes  ← get pods (permitido)```bash

```

# Ver todos os targets| **Auditoria** | http://localhost:30051 | - | Status do serviço de auditoria |│   ├── build.sh/.bat             # Build e push imagens

**📸 Print obrigatório:** Capturar tela mostrando que a ServiceAccount tem permissões restritas.

curl http://localhost:30090/api/v1/targets | jq '.data.activeTargets[] | {job: .scrapePool, health: .health}'

**✅ Checklist Etapa 4:**

- [ ] Print do `kubectl top pods` mostrando limites de CPU/Memória| **Grafana** | http://localhost:30300 | admin/admin | Dashboards de monitoramento |

- [ ] Print do manifest YAML mostrando `securityContext` configurado

- [ ] Print de tentativa de deploy insegura e `kubectl describe pod` mostrando bloqueio/warning# Verificar se kube-state-metrics está funcionando

- [ ] Print do `kubectl auth can-i` provando permissões restritas

curl http://localhost:30090/api/v1/query?query=kube_pod_info| **Prometheus** | http://localhost:30090 | - | Métricas e targets |Ou manualmente:│   ├── deploy-k8s.sh/.bat        # Deploy Kubernetes

---



## Anexos

# Métricas de CPU| **Rancher** | https://localhost:8443 | admin/unifiap123 | Gerenciamento de clusters |

### Pré-requisitos

curl http://localhost:30090/api/v1/query?query=node_cpu_seconds_total

Certifique-se de ter instalado:

| **Dashboard HTML** | `dashboard.html` | - | Painel de acesso rápido local |│   └── collect-evidences.sh      # Coleta evidências

- **Docker Desktop** com Kubernetes habilitado

- **kubectl** configurado e funcionando# Métricas de memória

- **Python 3.11+** com a biblioteca `requests`:

  ```bashcurl http://localhost:30090/api/v1/query?query=node_memory_MemAvailable_bytes

  pip install requests

  ``````

- **curl** para realizar testes de API

- **PowerShell 5.1+** (Windows)## 🛠️ Comandos Úteis```bash└── 📚 docs/                        # Documentação completa



---### Verificar Liquidação Automática



### URLs de Acesso



| Serviço | URL | Credenciais | Descrição |```bash

|---------|-----|-------------|-----------|

| **Frontend PIX** | http://localhost:30082 | - | Realizar transações PIX |# Acompanhar logs da auditoria em tempo real### Verificar Statuscurl -X POST http://localhost:30050/pix \    ├── evidencias-README.md       # Guia de evidências

| **API Swagger** | http://localhost:30050/docs | - | Documentação interativa da API |

| **Auditoria** | http://localhost:30051 | - | Status do serviço de liquidação |kubectl logs -n unifiapay -l app=auditoria-simple --tail 10 -f

| **Grafana** | http://localhost:30300 | admin / admin | Dashboards de monitoramento |

| **Prometheus** | http://localhost:30090 | - | Métricas e targets |

| **Rancher** | https://localhost:8443 | admin / unifiap123 | Gerenciamento de clusters |

| **Dashboard Local** | Abrir `dashboard.html` | - | Painel de acesso rápido |# Você verá mensagens a cada 15 segundos processando as instruções pendentes



---``````bash  -H "Content-Type: application/json" \    ├── manual-uso.md             # Manual técnico



### Comandos Úteis



#### Verificar Status---# Status de todos os pods do UniFIAP



```bash

# Status de todos os pods

kubectl get pods -n unifiapay## 🐛 Troubleshootingkubectl get pods -n unifiapay  -d '{    └── etapa[1-4]/              # Diretórios para screenshots



# Status detalhado de um pod específico

kubectl describe pod <NOME_DO_POD> -n unifiapay

### Problema: Pods não iniciam

# Status dos deployments

kubectl get deployments -n unifiapay



# Status dos services**Sintoma:** Pods ficam em status `Pending`, `CrashLoopBackOff` ou `Error`# Status detalhado dos deployments    "chave_pix": "11888888888",```

kubectl get svc -n unifiapay



# Status do Rancher

kubectl get pods -n cattle-system**Solução:**kubectl get deployments -n unifiapay

docker ps --filter name=rancher

``````bash



#### Ver Logs# 1. Ver detalhes do pod    "valor": 10.50,



```bashkubectl describe pod <NOME_DO_POD> -n unifiapay

# Logs da API de Pagamentos

kubectl logs -n unifiapay deployment/api-pagamentos-simple --tail 50 -f# Status de todos os services



# Logs do Serviço de Auditoria# 2. Ver logs do pod

kubectl logs -n unifiapay deployment/auditoria-simple --tail 50 -f

kubectl logs <NOME_DO_POD> -n unifiapaykubectl get svc -n unifiapay    "descricao": "Teste sistema"---

# Logs do Prometheus

kubectl logs -n unifiapay deployment/prometheus --tail 50



# Logs do Grafana# 3. Verificar recursos disponíveis

kubectl logs -n unifiapay deployment/grafana --tail 50

kubectl top nodes

# Logs do Rancher Agent

kubectl logs -n cattle-system deployment/cattle-cluster-agent --tail 50kubectl top pods -n unifiapay# Status do Rancher  }'

```



#### Reiniciar Serviços

# 4. Se necessário, reiniciar o deploymentkubectl get pods -n cattle-system

```bash

# Reiniciar todos os serviçoskubectl rollout restart deployment <NOME_DO_DEPLOYMENT> -n unifiapay

kubectl rollout restart deployment -n unifiapay

```docker ps --filter name=rancher```## 3. Execução Rápida

# Reiniciar serviço específico

kubectl rollout restart deployment api-pagamentos-simple -n unifiapay

kubectl rollout restart deployment auditoria-simple -n unifiapay

kubectl rollout restart deployment prometheus -n unifiapay---```

kubectl rollout restart deployment grafana -n unifiapay



# Verificar status do rollout

kubectl rollout status deployment <NOME_DO_DEPLOYMENT> -n unifiapay### Problema: Rancher não conecta ao cluster

```



#### Escalar Serviços

**Sintoma:** Erro "cluster not found" nos logs do cattle-cluster-agent### Logs

```bash

# Escalar API de Pagamentos para 3 réplicas

kubectl scale deployment api-pagamentos-simple -n unifiapay --replicas=3

**Solução:**### Ver Logs### 🚀 OPÇÃO 1: Deploy Completo com Rancher (RECOMENDADO)

# Escalar Frontend PIX para 2 réplicas

kubectl scale deployment frontend-pix-simple -n unifiapay --replicas=2```bash



# Verificar réplicas# 1. Verificar se o patch hostNetwork foi aplicado```bash

kubectl get deployment -n unifiapay

```kubectl get deployment cattle-cluster-agent -n cattle-system -o yaml | grep hostNetwork



#### Testar Transação PIX# Logs da API de Pagamentos



```bash# 2. Se não aparecer "hostNetwork: true", aplicar o patch

# Usando arquivo JSON (recomendado)

curl -X POST http://localhost:30050/pix -H "Content-Type: application/json" -d @test-pix.jsonkubectl patch deployment cattle-cluster-agent -n cattle-system -p '{"spec":{"template":{"spec":{"hostNetwork":true}}}}'kubectl logs -n unifiapay -l app=api-pagamentos-simple --tail 50



# Teste manual com valores personalizados

curl -X POST http://localhost:30050/pix -H "Content-Type: application/json" -d '{

  "chave_pix": "11999887766",# 3. Aguardar o rollout```bash#### Pré-requisitos

  "valor": 50.00,

  "descricao": "Pagamento de teste"kubectl rollout status deployment cattle-cluster-agent -n cattle-system

}'

```# Logs do serviço de Auditoria



**Resposta esperada:**# 4. Verificar logs

```json

{kubectl logs -n cattle-system -l app=cattle-cluster-agent --tail 20kubectl logs -n unifiapay -l app=auditoria-simple --tail 50# Logs de todos os serviços```bash

  "instrucao_id": "uuid-gerado-automaticamente",

  "mensagem": "PIX registrado e aguardando liquidação pelo BACEN",```

  "status": "AGUARDANDO_LIQUIDACAO",

  "sucesso": true,

  "timestamp": "2025-11-13T...",

  "valor": "50.00"---

}

```# Logs do Prometheusmake logs# Verificar ferramentas necessárias



#### Limpeza Completa### Problema: Namespace cattle-system travado em "Terminating"



```bashkubectl logs -n unifiapay -l app=prometheus --tail 50

# Remover todos os recursos do UniFIAP

kubectl delete -f k8s/unifiap-pay-spb.yaml**Sintoma:** Namespace não é removido após `kubectl delete namespace cattle-system`

kubectl delete -f k8s/kube-state-metrics.yaml

docker --version

# Parar e remover Rancher (mantém volumes)

docker-compose -f docker-compose.rancher.yml down**Solução:**



# Remover Rancher E SEUS DADOS (CUIDADO!)```bash# Logs do Grafana

docker-compose -f docker-compose.rancher.yml down -v

# 1. Exportar o namespace

# Remover namespace do Rancher

kubectl delete namespace cattle-system --force --grace-period=0kubectl get namespace cattle-system -o json > /tmp/ns.jsonkubectl logs -n unifiapay -l app=grafana --tail 50# Log específicodocker-compose --version



# Limpar ConfigMaps

kubectl delete configmap prometheus-config -n unifiapay

```# 2. Editar o arquivo e remover o array de finalizers



---# Abra /tmp/ns.json em um editor e remova esta linha:



### Troubleshooting# "finalizers": ["controller.cattle.io/namespace-auth"],# Logs do cattle-cluster-agent (Rancher)kubectl logs -n unifiapay -l app=api-pagamentos-simple```



#### Problema: Pods não iniciam# Deixe assim:



**Sintoma:** Pods ficam em status `Pending`, `CrashLoopBackOff` ou `Error`# "finalizers": [],kubectl logs -n cattle-system -l app=cattle-cluster-agent --tail 50



**Solução:**

```bash

# 1. Ver detalhes do pod# 3. Aplicar a correção```kubectl logs -n unifiapay -l app=auditoria-simple

kubectl describe pod <NOME_DO_POD> -n unifiapay

kubectl replace --raw /api/v1/namespaces/cattle-system/finalize -f /tmp/ns.json

# 2. Ver logs do pod

kubectl logs <NOME_DO_POD> -n unifiapay



# 3. Verificar recursos disponíveis# 4. Verificar remoção

kubectl top nodes

kubectl top pods -n unifiapaykubectl get namespace cattle-system### Restart de Serviços```#### Deploy Automático



# 4. Se necessário, reiniciar o deployment# Deve retornar "NotFound"

kubectl rollout restart deployment <NOME_DO_DEPLOYMENT> -n unifiapay

``````



#### Problema: Rancher não conecta ao cluster



**Sintoma:** Erro "cluster not found" nos logs do cattle-cluster-agent---```bash```bash



**Solução:**

```bash

# 1. Verificar se o patch hostNetwork foi aplicado### Problema: Grafana mostra "No data" nos dashboards# Reiniciar todos os deployments

kubectl get deployment cattle-cluster-agent -n cattle-system -o yaml | Select-String "hostNetwork"



# 2. Se não aparecer "hostNetwork: true", aplicar o patch

kubectl patch deployment cattle-cluster-agent -n cattle-system -p '{**Sintoma:** Todos os painéis do Grafana aparecem sem dadoskubectl rollout restart deployment -n unifiapay## 🛠️ Comandos Make# Windows

  "spec": {

    "template": {

      "spec": {

        "hostNetwork": true**Solução:**

      }

    }```bash

  }

}'# 1. Verificar se kube-state-metrics está rodando# Reiniciar serviço específicocd rancher-setup



# 3. Aguardar o rolloutkubectl get pods -n unifiapay -l app=kube-state-metrics

kubectl rollout status deployment cattle-cluster-agent -n cattle-system

kubectl rollout restart deployment api-pagamentos-simple -n unifiapay

# 4. Verificar logs

kubectl logs -n cattle-system deployment/cattle-cluster-agent --tail 20# 2. Verificar se Prometheus está coletando métricas

```

curl http://localhost:30090/api/v1/targets | grep kube-state-metricskubectl rollout restart deployment auditoria-simple -n unifiapay```bashdeploy.bat

#### Problema: Grafana mostra "No data"

# Deve mostrar "health": "up"

**Sintoma:** Todos os painéis do Grafana aparecem sem dados

kubectl rollout restart deployment grafana -n unifiapay

**Solução:**

```bash# 3. Verificar se o datasource está configurado

# 1. Verificar se kube-state-metrics está rodando

kubectl get pods -n unifiapay -l app=kube-state-metricscurl -u admin:admin http://localhost:30300/api/datasourceskubectl rollout restart deployment prometheus -n unifiapaymake help           # Lista todos os comandos disponíveis



# 2. Verificar se Prometheus está coletando métricas

curl http://localhost:30090/api/v1/targets | Select-String "kube-state-metrics"

# 4. Recarregar configuração do Prometheus```

# 3. Recarregar configuração do Prometheus

curl -X POST http://localhost:30090/-/reloadcurl -X POST http://localhost:30090/-/reload



# 4. Aguardar 30 segundos e atualizar o dashboard (F5)make deploy         # Deploy completo do sistema# Linux/macOS  

Start-Sleep -Seconds 30

```# 5. Aguardar 30 segundos e atualizar o dashboard (F5 no navegador)



#### Problema: Transação PIX falhasleep 30### Limpeza



**Sintoma:** API retorna erro ao tentar criar transação```



**Solução:**make status         # Status de todos os serviçoscd rancher-setup

```bash

# 1. Verificar se a API está rodando---

kubectl get pods -n unifiapay -l app=api-pagamentos-simple

```bash

# 2. Ver logs da API

kubectl logs -n unifiapay deployment/api-pagamentos-simple --tail 50### Problema: Prometheus não coleta métricas



# 3. Verificar se o ConfigMap foi carregado# Remover todos os recursos do UniFIAPmake logs           # Logs dos principais serviçoschmod +x deploy.sh

kubectl describe pod <NOME_DO_POD_API> -n unifiapay | Select-String "RESERVA_BANCARIA_SALDO"

**Sintoma:** Targets aparecem como "down" no Prometheus

# 4. Testar com valor menor que o saldo da reserva

curl -X POST http://localhost:30050/pix -H "Content-Type: application/json" -d '{kubectl delete -f k8s/unifiap-pay-spb.yaml

  "chave_pix": "11999887766",

  "valor": 10.00,**Solução:**

  "descricao": "Teste"

}'```bashkubectl delete -f k8s/kube-state-metrics.yamlmake test           # Testa sistema com transação PIX./deploy.sh

```

# 1. Verificar se o ConfigMap foi criado

---

kubectl get configmap prometheus-config -n unifiapay

## 📁 Estrutura do Projeto



```

unifiap-pay-spb/# 2. Verificar se está montado no deployment# Parar e remover Rancher```

│

├── core/                              # Código-fonte dos microsserviçoskubectl describe deployment prometheus -n unifiapay | grep -A 10 Volumes

│   ├── api-pagamentos/                # Serviço de pagamentos PIX

│   │   ├── app.py                     # Aplicação Flaskdocker-compose -f docker-compose.rancher.yml down

│   │   ├── Dockerfile                 # Imagem Docker (multi-stage)

│   │   └── requirements.txt           # Dependências Python# 3. Ver logs do Prometheus

│   │

│   ├── auditoria-service/             # Serviço de liquidaçãokubectl logs -n unifiapay -l app=prometheus --tail 50make rancher-up     # Inicia Rancher

│   │   ├── app.py                     # Aplicação Flask

│   │   ├── Dockerfile                 # Imagem Docker (multi-stage)

│   │   └── requirements.txt           # Dependências Python

│   │# 4. Se necessário, recriar o ConfigMap# Remover volumes do Rancher (ATENÇÃO: Remove todos os dados)

│   └── frontend-pix/                  # Interface web

│       ├── index.html                 # Página principalkubectl create configmap prometheus-config \

│       ├── app.js                     # Lógica JavaScript

│       ├── style.css                  # Estilos CSS  --from-file=monitoring/prometheus.yml \docker-compose -f docker-compose.rancher.yml down -vmake rancher-import # Instruções para importar cluster#### ✨ URLs de Acesso (Após Deploy):

│       ├── nginx.conf                 # Configuração Nginx

│       └── Dockerfile                 # Imagem Docker  -n unifiapay \

│

├── k8s/                               # Manifestos Kubernetes  --dry-run=client -o yaml | kubectl apply -f -

│   ├── unifiap-pay-spb.yaml           # Deploy completo

│   └── kube-state-metrics.yaml        # Métricas do Kubernetes

│

├── monitoring/                        # Configurações de observabilidade# 5. Reiniciar o Prometheus# Remover namespace cattle-system (se necessário)make rancher-down   # Para Rancher- **🎛️ Rancher UI**: http://localhost (admin / UniFIAP@2024!)

│   ├── prometheus.yml                 # Configuração do Prometheus

│   ├── alert_rules.yml                # Regras de alerta (opcional)kubectl rollout restart deployment prometheus -n unifiapay

│   └── grafana/

│       ├── dashboards/```kubectl delete namespace cattle-system --force --grace-period=0

│       │   └── unifiap-complete.json  # Dashboard completo

│       ├── datasources/

│       │   └── prometheus-datasource.yml

│       └── provisioning/---```- **💳 Frontend PIX**: http://localhost:8080

│

├── scripts/                           # Scripts de automação

│   ├── import-grafana-dashboard.py    # Importa dashboard via API

│   ├── setup-grafana.ps1              # Configuração manual## 📁 Estrutura do Projeto

│   ├── build.sh                       # Build das imagens Docker

│   └── deploy-k8s.sh                  # Deploy no Kubernetes

│

├── docs/                              # Documentação```## 🧪 Testesmake clean          # Remove todos os recursos- **🔧 API Pagamentos**: http://localhost:5000

│   ├── manual-uso.md                  # Manual de uso

│   ├── credenciais.md                 # Lista de credenciaisunifiap-pay-spb/

│   └── evidencias/                    # Evidências de testes

││

├── docker-compose.rancher.yml         # Docker Compose do Rancher

├── dashboard.html                     # Dashboard HTML para acesso rápido├── core/                              # Código-fonte dos microsserviços

├── test-pix.json                      # Payload de teste para transações PIX

└── README.md                          # Este arquivo│   ├── api-pagamentos/                # Serviço de pagamentos PIX### Teste de Transação PIXmake clean-rancher  # Remove apenas Rancher- **📊 Grafana**: http://localhost:3000

```

│   │   ├── app.py                     # Aplicação Flask

---

│   │   ├── Dockerfile                 # Imagem Docker

## 📚 Referências

│   │   └── requirements.txt           # Dependências Python

- [Documentação oficial do Kubernetes](https://kubernetes.io/docs/)

- [Documentação do Rancher](https://rancher.com/docs/)│   │```bash```- **📈 Prometheus**: http://localhost:9090

- [Documentação do Prometheus](https://prometheus.io/docs/)

- [Documentação do Grafana](https://grafana.com/docs/)│   ├── auditoria-service/             # Serviço de liquidação

- [Sistema de Pagamentos Brasileiro (SPB) - BACEN](https://www.bcb.gov.br/estabilidadefinanceira/spb)

- [PIX - Banco Central do Brasil](https://www.bcb.gov.br/estabilidadefinanceira/pix)│   │   ├── app.py                     # Aplicação Flask# Usando arquivo JSON



---│   │   ├── Dockerfile                 # Imagem Docker



## 👨‍💻 Autor│   │   └── requirements.txt           # Dependências Pythoncurl -X POST http://localhost:30050/pix \



**Renan Assi de Freitas**  │   │

RM: 93744  

FIAP - Pós Tech Software Architecture│   └── frontend-pix/                  # Interface web  -H "Content-Type: application/json" \



---│       ├── index.html                 # Página principal



## 📝 Licença│       ├── app.js                     # Lógica JavaScript  -d @test-pix.json## 📁 Estrutura do Projeto---



Este projeto é desenvolvido exclusivamente para fins educacionais como parte do desafio da FIAP.│       ├── style.css                  # Estilos CSS



---│       ├── nginx.conf                 # Configuração Nginx



**🎉 Projeto completo e documentado!**│       └── Dockerfile                 # Imagem Docker



Para acesso rápido a todas as URLs, abra o arquivo `dashboard.html` no navegador.│# Resposta esperada:


├── k8s/                               # Manifestos Kubernetes

│   ├── unifiap-pay-spb.yaml           # Deploy completo (Namespace, ConfigMaps, Deployments, Services)# {

│   └── kube-state-metrics.yaml        # Deployment do kube-state-metrics

│#   "instrucao_id": "uuid-gerado",```### 🚀 OPÇÃO 2: Deploy Kubernetes Tradicional (5 minutos)

├── monitoring/                        # Configurações de observabilidade

│   ├── prometheus.yml                 # Configuração do Prometheus (scrape configs)#   "mensagem": "PIX registrado e aguardando liquidação pelo BACEN",

│   ├── alert_rules.yml                # Regras de alerta (opcional)

│   └── grafana/#   "status": "AGUARDANDO_LIQUIDACAO",unifiap-pay-spb/

│       ├── dashboards/

│       │   └── unifiap-complete.json  # Dashboard completo do sistema#   "sucesso": true,

│       ├── datasources/

│       │   └── prometheus-datasource.yml  # Configuração do datasource#   "timestamp": "2025-11-12T...",├── core/                       # Código fonte dos microsserviços#### Pré-requisitos

│       └── provisioning/

│           └── dashboards/#   "valor": "10.5"

│               └── provider.yml       # Provider de dashboards

│# }│   ├── api-pagamentos/         # API de pagamentos PIX```bash

├── scripts/                           # Scripts de automação

│   ├── import-grafana-dashboard.py    # Importa dashboard via API

│   ├── setup-grafana.ps1              # Configuração manual (PowerShell)

│   ├── build.sh                       # Build das imagens Docker# Teste manual com valores customizados│   ├── auditoria-service/      # Serviço de auditoria# Verificar ferramentas necessárias

│   ├── deploy-k8s.sh                  # Deploy no Kubernetes

│   └── test-complete.sh               # Testes end-to-endcurl -X POST http://localhost:30050/pix \

│

├── docs/                              # Documentação  -H "Content-Type: application/json" \│   └── frontend-pix/           # Interface webdocker --version

│   ├── manual-uso.md                  # Manual de uso do sistema

│   ├── credenciais.md                 # Lista de credenciais  -d '{

│   └── evidencias/                    # Evidências de testes

│    "chave_pix": "11999887766",├── k8s/                        # Manifestos Kuberneteskubectl version --client

├── docker-compose.rancher.yml         # Docker Compose do Rancher

├── dashboard.html                     # Dashboard HTML para acesso rápido    "valor": 50.00,

├── test-pix.json                      # Payload de teste para transações PIX

└── README.md                          # Este arquivo    "descricao": "Pagamento teste"│   └── unifiap-pay-spb.yaml    # Deploy completominikube status  # ou kind get clusters

```

  }'

---

```├── monitoring/                 # Configurações de monitoramento```

## 📚 Informações Adicionais



### Variáveis de Ambiente

### Verificar Métricas│   ├── prometheus.yml

As principais configurações do sistema estão definidas no ConfigMap `unifiap-config` dentro do arquivo `k8s/unifiap-pay-spb.yaml`:



- **RESERVA_BANCARIA_SALDO**: R$ 1.000.000,00 (saldo inicial da reserva)

- **LIQUIDATION_MODE**: continuous (modo de liquidação contínua)```bash│   └── grafana/#### 1️⃣ Build das Imagens

- **MONITORING_INTERVAL**: 15s (intervalo de verificação de liquidação)

# Verificar targets do Prometheus

### Recursos e Limites

curl http://localhost:30090/api/v1/targets | jq '.data.activeTargets[] | {job: .scrapePool, health: .health}'├── docs/                       # Documentação```bash

Todos os deployments possuem `requests` e `limits` definidos:



| Pod | Memória (Request/Limit) | CPU (Request/Limit) |

|-----|------------------------|---------------------|# Verificar métricas do kube-state-metrics│   ├── manual-uso.md# Linux/macOS

| API Pagamentos | 256Mi / 512Mi | 200m / 400m |

| Auditoria | 128Mi / 256Mi | 100m / 200m |curl http://localhost:30090/api/v1/query?query=kube_pod_info

| Frontend | 64Mi / 128Mi | 100m / 200m |

| Prometheus | 256Mi / 512Mi | 200m / 400m |│   └── evidencias/chmod +x scripts/build.sh

| Grafana | 256Mi / 512Mi | 200m / 400m |

| Node Exporter | 64Mi / 128Mi | 100m / 200m |# Verificar métricas de CPU e memória

| Kube State Metrics | 128Mi / 256Mi | 100m / 200m |

curl http://localhost:30090/api/v1/query?query=node_memory_MemAvailable_bytes├── docker-compose.rancher.yml  # Configuração Rancher./scripts/build.sh

### Persistência de Dados

```

- **Logs compartilhados**: Volume `unifiap-logs-pv` compartilhado entre API e Auditoria

- **Dados do Rancher**: Volume Docker `rancher_data` (gerenciado pelo docker-compose)├── Makefile                    # Automação de comandos

- **Métricas do Prometheus**: Armazenadas em `/prometheus/` dentro do container (efêmero)

## 🐛 Troubleshooting

---

└── README.md                   # Este arquivo# Windows

## 👥 Autores

### Pods não iniciam

Projeto desenvolvido para **FIAP - Pós Tech Software Architecture**

```scripts\build.bat

---

```bash

## 📝 Licença

# Verificar eventos do pod```

Este projeto é desenvolvido exclusivamente para fins educacionais.

kubectl describe pod <POD_NAME> -n unifiapay

---

## 🔧 Configuração

## ✨ Resumo Rápido

# Verificar logs completos

```bash

# 1. Deploy completokubectl logs <POD_NAME> -n unifiapay#### 2️⃣ Deploy no Kubernetes

kubectl apply -f k8s/unifiap-pay-spb.yaml

kubectl apply -f k8s/kube-state-metrics.yaml



# 2. Configurar Prometheus# Verificar recursos disponíveis### Variáveis de Ambiente```bash

kubectl create configmap prometheus-config --from-file=monitoring/prometheus.yml -n unifiapay

# (aplicar patch conforme PASSO 2)kubectl top nodes



# 3. Configurar Grafanakubectl top pods -n unifiapay# Linux/macOS

python scripts/import-grafana-dashboard.py

```

# 4. Subir Rancher

docker-compose -f docker-compose.rancher.yml up -dAs principais configurações estão no arquivo `k8s/unifiap-pay-spb.yaml`:./scripts/deploy-k8s.sh



# 5. Importar cluster (via web UI + comando curl)### Rancher não conecta ao cluster

# 6. Testar

curl -X POST http://localhost:30050/pix -H "Content-Type: application/json" -d @test-pix.json

```

**Problema:** "cluster not found" nos logs do cattle-cluster-agent

**🎉 Sistema completo operacional!**

- `RESERVA_BANCARIA_SALDO`: Saldo inicial (padrão: R$ 1.000.000,00)# Windows

Para acesso rápido a todas as URLs, abra o arquivo `dashboard.html` no navegador.

**Solução:**

```bash- `LIQUIDATION_MODE`: Modo de liquidação (padrão: continuous)scripts\deploy-k8s.bat

# 1. Verificar se o patch hostNetwork foi aplicado

kubectl get deployment cattle-cluster-agent -n cattle-system -o yaml | grep hostNetwork- `MONITORING_INTERVAL`: Intervalo de verificação (padrão: 15s)```



# 2. Se não estiver, aplicar novamente

kubectl patch deployment cattle-cluster-agent -n cattle-system -p '{"spec":{"template":{"spec":{"hostNetwork":true}}}}'

### Persistência#### 3️⃣ Testar Sistema Completo

# 3. Aguardar rollout

kubectl rollout status deployment cattle-cluster-agent -n cattle-system```bash

```

O sistema utiliza PersistentVolume para:# Port forward da API

### Namespace cattle-system travado em "Terminating"

- Logs compartilhados entre API e Auditoriakubectl port-forward service/api-pagamentos-service 5000:80 -n unifiapay &

```bash

# 1. Exportar namespace- Dados do Rancher (via Docker volume)

kubectl get namespace cattle-system -o json > ns.json

# Port forward do Frontend (se usando K8s)

# 2. Editar e remover finalizers (usar editor de texto)

# Remover todo o array "finalizers": [...]## 📖 Documentação Adicionalkubectl port-forward service/frontend-pix-service 8080:80 -n unifiapay &



# 3. Aplicar

kubectl replace --raw /api/v1/namespaces/cattle-system/finalize -f ns.json

- [Manual de Uso](docs/manual-uso.md)# Teste rápido da API

# 4. Verificar remoção

kubectl get namespace cattle-system- [Guia de Importação Rancher](RANCHER-IMPORT-GUIDE.md)curl http://localhost:5000/health

```

- [Evidências de Testes](docs/evidencias/)

### Grafana sem métricas

# Acesse o Frontend

**Problema:** Dashboard mostra "No data"

## 🐛 Troubleshooting# http://localhost:8080

**Solução:**

```bash```

# 1. Verificar se kube-state-metrics está rodando

kubectl get pods -n unifiapay -l app=kube-state-metrics### Pods não iniciam



# 2. Verificar se Prometheus está coletando---

curl http://localhost:30090/api/v1/targets | grep kube-state-metrics

```bash

# 3. Verificar se datasource está configurado no Grafana

curl -u admin:admin http://localhost:30300/api/datasources# Verificar eventos### 🚀 OPÇÃO 3: Frontend Local para Desenvolvimento



# 4. Recarregar configuração do Prometheuskubectl describe pod -n unifiapay [POD_NAME]

curl -X POST http://localhost:30090/-/reload

#### Executar Frontend sem Docker

# 5. Aguardar 30 segundos e atualizar dashboard (F5)

```# Ver logs```bash



### Prometheus não coleta métricaskubectl logs -n unifiapay [POD_NAME]cd frontend-pix



```bash```

# 1. Verificar se ConfigMap foi criado

kubectl get configmap prometheus-config -n unifiapay# Servir com Python



# 2. Verificar se está montado no deployment### Rancher não conecta ao clusterpython -m http.server 8080

kubectl describe deployment prometheus -n unifiapay | grep -A 5 Volumes



# 3. Verificar logs do Prometheus

kubectl logs -n unifiapay -l app=prometheus --tail 100```bash# OU com Live Server (VS Code)



# 4. Recriar ConfigMap se necessário# Após importar, aplicar patch de rede# Instalar extensão Live Server

kubectl create configmap prometheus-config --from-file=monitoring/prometheus.yml -n unifiapay --dry-run=client -o yaml | kubectl apply -f -

kubectl patch deployment cattle-cluster-agent -n cattle-system \# Clique direito em index.html > "Open with Live Server"

# 5. Reiniciar Prometheus

kubectl rollout restart deployment prometheus -n unifiapay  -p '{"spec":{"template":{"spec":{"hostNetwork":true}}}}'

```

```# Acesse: http://localhost:8080

## 📁 Estrutura do Projeto

```

```

unifiap-pay-spb/### Remover namespace travado

├── core/                           # Código fonte dos microsserviços

│   ├── api-pagamentos/             # API de pagamentos PIX### 🧪 Teste Completo da API

│   │   ├── app.py                  # Aplicação Flask

│   │   ├── Dockerfile              # Imagem Docker```bash

│   │   └── requirements.txt        # Dependências Python

│   ├── auditoria-service/          # Serviço de auditoria/liquidação# Criar arquivo patch JSON removendo finalizers```bash

│   │   ├── app.py

│   │   ├── Dockerfilekubectl get namespace cattle-system -o json > ns.json# 1. Health check

│   │   └── requirements.txt

│   └── frontend-pix/               # Interface web# Editar ns.json removendo array finalizerscurl -X GET http://localhost:5000/health

│       ├── index.html

│       ├── app.jskubectl replace --raw /api/v1/namespaces/cattle-system/finalize -f ns.json

│       ├── style.css

│       ├── nginx.conf```# 2. Consultar reserva bancária

│       └── Dockerfile

├── k8s/                            # Manifestos Kubernetescurl -X GET http://localhost:5000/saldo-reserva

│   ├── unifiap-pay-spb.yaml        # Deploy completo do sistema

│   └── kube-state-metrics.yaml     # Métricas do Kubernetes## 👥 Autores

├── monitoring/                     # Configurações de monitoramento

│   ├── prometheus.yml              # Config do Prometheus# 3. Processar PIX

│   ├── alert_rules.yml             # Regras de alerta

│   └── grafana/Projeto desenvolvido para FIAP - Pós Tech Software Architecturecurl -X POST http://localhost:5000/pix \

│       ├── dashboards/

│       │   └── unifiap-complete.json  # Dashboard completo  -H "Content-Type: application/json" \

│       ├── datasources/

│       │   └── prometheus-datasource.yml## 📝 Licença  -d '{

│       └── provisioning/

│           └── dashboards/    "valor": 150.00,

│               └── provider.yml

├── scripts/                        # Scripts de automaçãoEste projeto é desenvolvido para fins educacionais.    "chave_pix": "usuario@exemplo.com",

│   ├── import-grafana-dashboard.py # Importa dashboard no Grafana    "banco_destinatario": "001",

│   ├── setup-grafana.ps1          # Configuração manual do Grafana    "descricao": "PIX de teste"

│   ├── build.sh                   # Build de imagens Docker  }'

│   ├── deploy-k8s.sh              # Deploy no Kubernetes

│   └── test-complete.sh           # Testes end-to-end# 4. Listar instruções

├── docs/                           # Documentaçãocurl -X GET http://localhost:5000/instrucoes

│   ├── manual-uso.md              # Manual de uso do sistema```

│   ├── credenciais.md             # Lista de credenciais

│   └── evidencias/                # Evidências de testes---

├── docker-compose.rancher.yml      # Docker Compose do Rancher

├── dashboard.html                  # Dashboard HTML local## 4. Documentação Técnica

├── test-pix.json                   # Payload de teste PIX

├── Makefile                        # Automação de comandos### 📖 Guias Disponíveis

└── README.md                       # Este arquivo- **[📋 Manual de Uso Completo](docs/manual-uso.md)** - Guia técnico detalhado

```- **[🔍 Guia de Evidências](docs/evidencias-README.md)** - Como coletar todas as evidências

- **[🏗️ Arquitetura Técnica](docs/arquitetura-tecnica.md)** - Diagramas e especificações

## 📚 Configurações Importantes

### 🔗 Endpoints da API

### Variáveis de Ambiente

| Método | Endpoint | Descrição |

Definidas em `k8s/unifiap-pay-spb.yaml` no ConfigMap `unifiap-config`:|--------|----------|-----------|

| `GET` | `/health` | Health check da aplicação |

- `RESERVA_BANCARIA_SALDO`: Saldo inicial da reserva (padrão: R$ 1.000.000,00)| `GET` | `/saldo-reserva` | Consulta saldo da reserva bancária |

- `LIQUIDATION_MODE`: Modo de liquidação (padrão: continuous)| `POST` | `/pix` | Processar pagamento PIX |

- `MONITORING_INTERVAL`: Intervalo de verificação (padrão: 15s)| `GET` | `/instrucoes` | Listar todas as instruções |

| `GET` | `/instrucoes/{id}` | Consultar instrução específica |

### Recursos e Limites

### 🔧 Comandos Kubernetes Úteis

Todos os pods têm `requests` e `limits` definidos para garantir alocação adequada:

```bash

- **API Pagamentos**: 256Mi-512Mi RAM, 200m-400m CPU# 📊 Monitoramento

- **Auditoria**: 128Mi-256Mi RAM, 100m-200m CPUkubectl get pods -n unifiapay -w

- **Frontend**: 64Mi-128Mi RAM, 100m-200m CPUkubectl top pods -n unifiapay

- **Prometheus**: 256Mi-512Mi RAM, 200m-400m CPU

- **Grafana**: 256Mi-512Mi RAM, 200m-400m CPU# 📋 Logs

kubectl logs -f deployment/api-pagamentos -n unifiapay

### Portas dos Serviceskubectl logs -f deployment/auditoria-service -n unifiapay



- **API Pagamentos**: NodePort 30050# ⚡ Escala

- **Auditoria**: NodePort 30051kubectl scale deployment api-pagamentos --replicas=3 -n unifiapay

- **Frontend PIX**: NodePort 30082

- **Prometheus**: NodePort 30090# 🔄 Jobs manuais

- **Grafana**: NodePort 30300kubectl create job --from=cronjob/cronjob-fechamento-reserva manual-test -n unifiapay

- **Node Exporter**: NodePort 30100```



## 👥 Autores---



Projeto desenvolvido para **FIAP - Pós Tech Software Architecture**## 5. Evidências e Avaliação



## 📝 Licença### ✅ Checklist de Pontuação



Este projeto é desenvolvido para fins educacionais.| Etapa | Pontos | Status | Evidências |

|-------|--------|--------|------------|

---| **1. Docker e Imagem Segura** | 1,5 pts | ✅ | Multi-stage build, Push v1.93744, Scan vulnerabilidades |

| **2. Rede e Comunicação** | 2,5 pts | ✅ | Rede 172.25.0.0/24, Comunicação containers, ENV vars |

**✨ Sistema 100% Operacional com Kubernetes + Rancher + Prometheus + Grafana!**| **3. Kubernetes Básico** | 3,0 pts | ✅ | 2 réplicas API, Volume compartilhado, CronJob |

| **4. Kubernetes Avançado** | 2,0 pts | ✅ | Resource limits, SecurityContext, RBAC |

Para acessar rapidamente todos os serviços, abra o arquivo `dashboard.html` no navegador.| **TOTAL** | **9,0 pts** | ✅ | **Todos os critérios atendidos** |


### 📸 Coleta Automática de Evidências
```bash
# Script automatizado para gerar todas as evidências
./scripts/collect-evidences.sh

# Resultado: arquivo docs/evidencias_YYYYMMDD_HHMMSS.md
```

### 📁 Organização das Evidências

```
📁 docs/
├── 🔗 evidencias-README.md                    # Guia principal
├── 📊 evidencias_20241110_143022.md          # Relatório automático
├── etapa1-docker-imagem-segura/              # Screenshots Etapa 1
├── etapa2-rede-comunicacao-segmentacao/      # Screenshots Etapa 2  
├── etapa3-kubernetes-estrutura-escala/       # Screenshots Etapa 3
└── etapa4-kubernetes-seguranca-observacao/   # Screenshots Etapa 4
```

---

## 6. Configurações Específicas do RM

### 🏷️ Tags e Identificação
```bash
# Todas as imagens são tagueadas com o RM do aluno
API_IMAGE="codecaman/api-pagamentos:v1.93744"
AUDITORIA_IMAGE="codecaman/auditoria-service:v1.93744"

# ConfigMaps e recursos identificados
NAMESPACE="unifiapay"
RESERVA_BANCARIA_SALDO="1000000.00"
```

### 🔐 Segurança Implementada

#### Docker
- ✅ **Multi-stage builds** (imagens otimizadas)
- ✅ **Usuário não-root** (segurança)
- ✅ **Scan vulnerabilidades** (docker scout)
- ✅ **Rede isolada** (172.25.0.0/24)

#### Kubernetes  
- ✅ **SecurityContext** (runAsNonRoot: true)
- ✅ **Resource Limits** (CPU/Memory)
- ✅ **RBAC** (permissões mínimas)
- ✅ **Network Policies** (isolamento)
- ✅ **Secrets** (dados sensíveis)

---

## 7. Passos de Execução Detalhados

### 2.1. Configuração Local (Docker)

#### 1️⃣ Criar Rede Docker Segmentada

```bash
# Criar rede customizada com subnet isolada
docker network create --driver bridge --subnet=172.25.0.0/24 unifiap_net
```

#### 2️⃣ Preparar Variáveis de Ambiente
```bash
# Editar arquivo docker/.env
cd docker/
cp .env.example .env  # Se necessário
nano .env  # Configurar RESERVA_BANCARIA_SALDO e outras variáveis
```

### 2.2. Build e Publicação das Imagens

#### 🏗️ Build Multi-stage com Segurança
```bash
# Executar script automatizado
./scripts/build.sh  # Linux/macOS
# ou
scripts\build.bat   # Windows

# Ou build manual:
cd api-pagamentos/
docker build -t codecaman/api-pagamentos:v1.93744 .

cd ../auditoria-service/
docker build -t codecaman/auditoria-service:v1.93744 .
```

#### 🔍 Varredura de Vulnerabilidades
```bash
# Scan automático com Docker Scout
docker scout cves codecaman/api-pagamentos:v1.93744
docker scout cves codecaman/auditoria-service:v1.93744
```

#### 📤 Push para Docker Hub
```bash
# Login no Docker Hub
docker login

# Push das imagens
docker push codecaman/api-pagamentos:v1.93744
docker push codecaman/auditoria-service:v1.93744
```

### 2.3. Subindo o Rancher (Opcional)

```bash
# Para interface visual de gerenciamento
docker run -d --restart=unless-stopped \
  -p 80:80 -p 443:443 \
  --privileged \
  rancher/rancher:latest
```

**Acesso:** http://localhost (aguardar inicialização)

### 2.4. Deploy no Kubernetes

#### 🚀 Deploy Completo
```bash
# Script automatizado
./scripts/deploy-k8s.sh  # Linux/macOS
# ou  
scripts\deploy-k8s.bat   # Windows

# Ou deploy manual step-by-step:
kubectl apply -f k8s/01-namespace.yaml
kubectl apply -f k8s/02-configmap.yaml
kubectl apply -f k8s/03-secret.yaml
kubectl apply -f k8s/04-pvc.yaml
kubectl apply -f k8s/05-rbac.yaml
kubectl apply -f k8s/06-api-pagamentos-deployment.yaml
kubectl apply -f k8s/07-api-pagamentos-service.yaml
kubectl apply -f k8s/08-auditoria-service-deployment.yaml
kubectl apply -f k8s/09-cronjob.yaml
kubectl apply -f k8s/10-network-policy.yaml
```

#### ✅ Verificar Status
```bash
# Aguardar pods ficarem prontos
kubectl wait --for=condition=ready pod -l app=api-pagamentos -n unifiapay --timeout=300s

# Status geral
kubectl get all -n unifiapay
```

---

## 8. Evidências e Resultados

### 3.1. Etapa 1: Docker e Imagem Segura (1,5 pts)

#### 📋 Evidências Necessárias:
- ✅ **Print do docker build** mostrando multi-stage
- ✅ **Saída do docker push** com tag v1.93744  
- ✅ **Saída do docker scout** comprovando ausência de vulnerabilidades críticas

#### 🔧 Comandos para Evidências:
```bash
# Build com output detalhado
docker build -t codecaman/api-pagamentos:v1.93744 ./api-pagamentos/ --progress=plain

# Push com confirmação
docker push codecaman/api-pagamentos:v1.93744

# Scan de segurança
docker scout cves codecaman/api-pagamentos:v1.93744
```

### 3.2. Etapa 2: Rede, Comunicação e Segmentação (2,5 pts)

#### 📋 Evidências Necessárias:
- ✅ **docker inspect unifiap_net** mostrando bloco IP 172.25.0.0/24
- ✅ **curl/ping entre containers** comprovando comunicação
- ✅ **Logs da API** lendo RESERVA_BANCARIA_SALDO do .env

#### 🔧 Comandos para Evidências:
```bash
# Inspecionar rede
docker network inspect unifiap_net

# Subir containers e testar comunicação
cd docker/
docker-compose up -d
docker exec unifiap-api-pagamentos curl http://unifiap-auditoria-service:8080/health

# Ver logs de configuração
docker logs unifiap-api-pagamentos | grep RESERVA_BANCARIA
```

### 3.3. Etapa 3: Kubernetes – Estrutura, Escala e Deploy (3,0 pts)

#### 📋 Evidências Necessárias:
- ✅ **kubectl get pods** mostrando API com 2 réplicas e Auditoria rodando
- ✅ **kubectl scale** e subsequente get pods mostrando aumento
- ✅ **Logs de pods** provando leitura/escrita no mesmo arquivo
- ✅ **kubectl get cronjob/job** após execução

#### 🔧 Comandos para Evidências:
```bash
# Ver pods iniciais (2 réplicas da API)
kubectl get pods -n unifiapay

# Escalar para 3 réplicas
kubectl scale deployment api-pagamentos --replicas=3 -n unifiapay
kubectl get pods -n unifiapay

# Ver logs compartilhando volume
kubectl logs deployment/api-pagamentos -n unifiapay
kubectl logs deployment/auditoria-service -n unifiapay

# Executar job manual
kubectl create job --from=cronjob/cronjob-fechamento-reserva manual-evidencia -n unifiapay
kubectl get cronjobs,jobs -n unifiapay
```

### 3.4. Etapa 4: Kubernetes – Segurança, Observação e Operação (2,0 pts)

#### 📋 Evidências Necessárias:
- ✅ **kubectl top pods** mostrando limites CPU/Memória
- ✅ **Manifest YAML** com securityContext (runAsNonRoot: true)
- ✅ **Deploy inseguro** sendo bloqueado por regra
- ✅ **kubectl auth can-i** provando ServiceAccount restrita

#### 🔧 Comandos para Evidências:
```bash
# Verificar uso de recursos
kubectl top pods -n unifiapay

# Ver configuração de segurança
kubectl get deployment api-pagamentos -n unifiapay -o yaml | grep -A 10 securityContext

# Testar permissões RBAC
kubectl auth can-i get pods --as=system:serviceaccount:unifiapay:unifiap-service-account -n unifiapay
kubectl auth can-i delete deployments --as=system:serviceaccount:unifiapay:unifiap-service-account -n unifiapay

# Tentar deploy inseguro (deve falhar)
kubectl apply -f - <<EOF
apiVersion: v1
kind: Pod
metadata:
  name: insecure-test
  namespace: unifiapay
spec:
  containers:
  - name: insecure
    image: nginx
    securityContext:
      runAsUser: 0
      privileged: true
EOF

kubectl describe pod insecure-test -n unifiapay
```

---

## 9. Troubleshooting

### 🔧 Problemas Comuns

#### Docker
```bash
# Container não inicia
docker logs <container_name>
docker inspect <container_name>

# Rede não funciona
docker network ls
docker network inspect unifiap_net

# Rebuild forçado
docker build --no-cache -t <image> .
```

#### Kubernetes
```bash
# Pod não inicia
kubectl describe pod <pod-name> -n unifiapay
kubectl logs <pod-name> -n unifiapay

# PVC não monta
kubectl get pv,pvc -n unifiapay
kubectl describe pvc unifiap-logs-pvc -n unifiapay

# Service não responde
kubectl get svc -n unifiapay
kubectl port-forward service/api-pagamentos-service 5000:80 -n unifiapay
```

#### Limpeza Completa
```bash
# Docker
docker-compose down -v
docker system prune -a

# Kubernetes
kubectl delete namespace unifiapay
```

---

## 10. Links e Recursos

### 📚 Documentação
- **[Manual de Uso Completo](docs/manual-uso.md)**
- **[Guia de Evidências](docs/evidencias-README.md)**
- **[Troubleshooting Avançado](docs/troubleshooting.md)**

### 🔗 URLs Importantes
- **API Local:** http://localhost:5000 (após port-forward)
- **Rancher:** http://localhost (se instalado)
- **Docker Hub:** https://hub.docker.com/u/codecaman

### 🛠️ Ferramentas Necessárias
- [Docker Desktop](https://www.docker.com/products/docker-desktop)
- [Minikube](https://minikube.sigs.k8s.io/docs/start/) ou [Kind](https://kind.sigs.k8s.io/)
- [kubectl](https://kubernetes.io/docs/tasks/tools/)

---

## ✅ Status Final

**🎯 Projeto Status:** ✅ **COMPLETO - 9,0 pts**

| Critério | Status | Pontos |
|----------|--------|--------|
| Docker Multi-stage + Segurança | ✅ | 1,5 pts |
| Rede Customizada + Comunicação | ✅ | 2,5 pts |  
| Kubernetes Deploy + Escala | ✅ | 3,0 pts |
| Kubernetes Segurança + RBAC | ✅ | 2,0 pts |
| **TOTAL** | ✅ | **9,0 pts** |

**🚀 Pronto para Execução e Avaliação!**


**Desenvolvido por:** Renan Assi de Freitas (RM: 93744)  
**Projeto:** UniFIAP Pay SPB - Sistema de Pagamentos Brasileiro

# ⚙️ Kubernetes Configuration & Bootstrapping

Este repositório contém a automação de **Gerenciamento de Configuração** responsável por transformar instâncias "cruas" de Linux (Ubuntu) em um cluster Kubernetes totalmente funcional, moderno e resiliente.

Desenvolvido com **Ansible**, este projeto demonstra o domínio sobre a camada de Sistema Operacional, Container Runtimes e Orquestração de Contêineres, indo muito além de soluções gerenciadas onde essas complexidades são ocultadas.

## 🎯 Visão Executiva

Este repositório reflete o nível de maturidade exigido em certificações de elite como o **CKA / CKS / Kubestronaut**.

O código foi desenhado de forma modular, idempotente e autodocumentada, mostrando a capacidade de padronizar frotas de servidores, resolver conflitos de rede em nível de SO e arquitetar um cluster *Bare-Metal* pronto para produção.

## 🏗️ Stack Tecnológico e Módulos

A automação é dividida em playbooks estratégicos, abordando cada camada crítica do ecossistema Cloud-Native.

| Componente | Ferramenta / Tecnologia | Detalhes da Implementação |
| :--- | :--- | :--- |
| **OS Tuning** | Ubuntu & iptables | Tratamento de conflitos de firewall do provedor, liberação de tráfego bridged e ajustes de Kernel (`sysctl`, `swapoff`). |
| **Container Runtime** | containerd.io | Configuração avançada de CRI (Container Runtime Interface) com integração obrigatória ao `SystemdCgroup = true`. |
| **Kubernetes Base** | `kubeadm`, `kubelet`, `kubectl` | Configuração de repositórios, injeção de chaves GPG e bloqueio de versão de pacotes (apt mark hold) para evitar upgrades acidentais. |
| **Redes de Contêiner (CNI)** | Calico | Automação da instalação do CNI para garantir o roteamento de rede BGP entre os Pods do cluster. |
| **Roteamento Moderno** | Envoy Gateway | Implementação da **Gateway API** (substituindo o obsoleto Ingress-NGINX), alinhando o cluster aos padrões de infraestrutura da próxima geração. |

## 🧠 Maturidade de Engenharia e Decisões

* **Idempotência Garantida:** Os scripts foram construídos para serem rodados múltiplas vezes sem quebrar o estado do servidor. Módulos do Ansible controlam o que já foi criado, instalado ou modificado.
* **Troubleshooting Avançado Resolvido via Código:** Imagens nativas de nuvem frequentemente vêm com regras rígidas de `iptables` que bloqueiam a comunicação do Control Plane, mesmo quando as portas estão abertas no provedor de nuvem. O Ansible foi desenhado para identificar e limpar essa camada restritiva de forma autônoma.
* **Preparação para Infraestrutura Híbrida:** A configuração final permite que as chaves geradas no Control Plane sejam extraídas e mescladas em `kubeconfigs` locais de desenvolvedores, permitindo a gestão simultânea deste cluster *Bare-Metal* em conjunto com clusters GKE/EKS através de uma única CLI.
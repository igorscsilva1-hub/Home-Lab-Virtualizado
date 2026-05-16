# Planejamento

## Objetivo do projeto

Desenvolver um Home Lab virtualizado para estudos práticos de:

- Infraestrutura
- Redes
- Virtualização
- Linux
- Windows Server
- Segurança da Informação

O ambiente busca simular uma infraestrutura corporativa básica utilizando máquinas virtuais e segmentação de rede.

---

## Tecnologias utilizadas

- Oracle VirtualBox
- Ubuntu Server
- OPNsense
- Windows Server
- OpenSSH
- DHCP
- DNS

---

## Estrutura do ambiente

| Componente | Função |
|---|---|
| Ubuntu Server | Serviços Linux e testes de rede |
| OPNsense | Firewall e roteamento |
| Windows Server | Serviços Microsoft (futuro) |
| Internal Network | Rede interna isolada |
| Host-Only | Gerenciamento das VMs |
| Bridge Adapter | Acesso externo |

---

## Fases do projeto

| Fase | Status |
|---|---|
| Preparação do ambiente | Concluído |
| Ubuntu Server | Concluído |
| SSH e acesso remoto | Concluído |
| Redes virtuais | Concluído |
| OPNsense | Em andamento |
| DHCP interno | Pendente |
| Firewall Rules | Pendente |
| Windows Server | Pendente |
| Active Directory | Pendente |
| Hardening | Pendente |
| Documentação final | Em andamento |

---

## Alteração de tecnologia

Inicialmente o projeto utilizaria pfSense.

Durante a instalação ocorreram travamentos utilizando a ISO Netgate no Oracle VirtualBox.

Como alternativa, o ambiente foi migrado para o OPNsense, mantendo os mesmos objetivos de firewall, roteamento e segmentação da infraestrutura.

---

## Próximos passos

- Resolver acesso ao WebGUI do OPNsense
- Configurar DHCP interno
- Criar regras de firewall
- Validar acesso externo das VMs
- Implementar Windows Server
- Integrar Active Directory ao ambiente

---

## Objetivos futuros

- Simular ambiente corporativo básico
- Integrar Linux e Windows Server
- Implementar serviços de autenticação
- Trabalhar segmentação de rede
- Desenvolver habilidades práticas em troubleshooting
- Expandir documentação técnica do laboratório

# Home-Lab-Virtualizado

Projeto de laboratório virtualizado focado em estudos de infraestrutura, redes e segurança da informação.

O ambiente utiliza VirtualBox, pfSense, Ubuntu Server e Windows Server para simular uma rede corporativa básica.

## Objetivos

- Praticar virtualização
- Praticar configuração de redes
- Estudar firewall e roteamento
- Trabalhar com Linux e Windows Server
- Desenvolver documentação técnica
- Desenvolver habilidades práticas de troubleshooting
  
## Tecnologias

- Oracle VirtualBox
- OPNsense
- Ubuntu Server
- Windows Server
- SSH
- NAT
- DHCP
- DNS

## Estado atual do projeto

Atualmente o ambiente possui:

- Ubuntu Server configurado
- OpenSSH funcional
- Comunicação entre VMs funcionando
- Redes Bridge, Internal Network e Host-Only configuradas
- OPNsense parcialmente configurado
- Roteamento interno funcional
- Gateway centralizado via OPNsense
- Documentação técnica em andamento
- Sessão dedicada de troubleshooting

## Topologia atual

| Rede | Finalidade |
|---|---|
| Bridge Adapter | Acesso externo/internet |
| Internal Network | Comunicação interna entre VMs |
| Host-Only | Gerenciamento do firewall |

## Alteração de tecnologia

O projeto inicialmente utilizaria pfSense, porém ocorreram instabilidades durante a instalação da ISO Netgate no ambiente virtualizado.
Como solução, o firewall foi migrado para o OPNsense, mantendo os mesmos objetivos de segmentação, roteamento e segurança da infraestrutura.

## Versões

### v1.0
- Estrutura inicial criada

### v1.1
- Ubuntu Server configurado
- SSH habilitado

### v1.2
- Adaptador de rede Host-Only adicionado ao Ubuntu Server
- SSH mais estável
- Ubuntu Server clonado para teste de conexão entre VMs

### v1.3
- Redes Internal Network configuradas
- Comunicação entre VMs validada
- OPNsense implementado
- WAN, LAN e OPT1 configuradas
- Gateway centralizado via OPNsense
- Documentação expandida


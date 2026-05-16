# Rede

## Objetivo

Documentar a estrutura de rede do Home Lab, incluindo topologia, segmentação, comunicação entre máquinas virtuais e integração com o OPNsense.

---

## Topologia atual

Atualmente o ambiente utiliza três tipos principais de rede no Oracle VirtualBox:

| Rede | Finalidade |
|---|---|
| Bridge Adapter | Acesso externo/internet |
| Internal Network | Comunicação interna entre VMs |
| Host-Only | Gerenciamento entre host e VMs |

---

## Estrutura atual das VMs Ubuntu

### ubuntu-server

| Interface | Rede | IP |
|---|---|---|
| enp0s3 | Bridge | DHCP |
| enp0s8 | Host-Only | 192.168.56.10 |
| enp0s9 | Internal Network | 192.168.100.x |

### ubuntu-server-02

| Interface | Rede | IP |
|---|---|---|
| enp0s3 | Bridge | DHCP |
| enp0s8 | Host-Only | 192.168.56.11 |
| enp0s9 | Internal Network | 192.168.100.x |

---

## Estrutura atual do OPNsense

| Interface | Função | IP |
|---|---|---|
| WAN | Bridge Adapter | 192.168.18.45 |
| LAN | Internal Network | 192.168.100.1 |
| OPT1 | Host-Only | 192.168.56.1 |

---

## Comunicação entre Host e VM

A rede Host-Only é utilizada para:

- Acesso SSH
- Gerenciamento das VMs
- Comunicação estável entre host Windows e ambiente virtualizado

Essa abordagem evita dependência de IPs dinâmicos fornecidos pelo roteador local.

---

## Teste de comunicação entre VMs via Host-Only

### Configuração

| VM | Interface | IP |
|---|---|---|
| ubuntu-server | enp0s8 | 192.168.56.10 |
| ubuntu-server-02 | enp0s8 | 192.168.56.11 |

### Teste realizado

Ping bidirecional entre as VMs:

```bash
# Na ubuntu-server-02
ping 192.168.56.10

# Na ubuntu-server
ping 192.168.56.11
```

### Resultado

Ambos os testes retornaram respostas, confirmando comunicação entre as máquinas virtuais.

![ubuntu-server para ubuntu-server2](../imagens/ubuntu/ping-ubuntuserver-vm2.png)

![ubuntu-server2 para ubuntu-server](../imagens/ubuntu/ping-vm2-ubuntuserver.png)

---

## Teste de comunicação via Internal Network

### Configuração inicial

| VM | Interface | IP |
|---|---|---|
| ubuntu-server | enp0s9 | 10.0.0.1 |
| ubuntu-server-02 | enp0s9 | 10.0.0.2 |

### Modo Internal Network

As VMs se comunicam em uma rede completamente isolada.

O host Windows não participa dessa rede.

Esse modo foi utilizado como preparação para implementação do firewall virtual.

### Teste realizado

```bash
# Na ubuntu-server-02
ping 10.0.0.1

# Na ubuntu-server
ping 10.0.0.2
```

### Resultado

Ambos os testes retornaram sucesso, confirmando isolamento e comunicação entre as VMs.

![ubuntu-server para ubuntu-server-02 e vice-versa](../imagens/ubuntu/ping-vm2-ubuntuserver-redeinterna.png)

---

## Integração com OPNsense

Após a implementação do OPNsense:

- As VMs Ubuntu foram migradas para o range `192.168.100.x`
- O gateway passou a ser `192.168.100.1`
- A comunicação entre as VMs passou a utilizar roteamento interno através do firewall virtual

---

## Comunicação entre VMs via OPNsense

### Objetivo

Validar o funcionamento do roteamento interno utilizando o OPNsense como gateway da rede.

### Resultado

As VMs conseguiram se comunicar corretamente utilizando o OPNsense como gateway da LAN interna.

![Ping entre ubuntu-server e ubuntu-server02](../imagens/ubuntu/ping-ubuntuserver-vm2-opnsensegateway.png)

![Ping entre ubuntu-server02 e ubuntu-server](../imagens/ubuntu/ping-vm2-ubuntuserver-opnsensegateway.png)

---

## Estado atual da infraestrutura

| Serviço | Status |
|---|---|
| Comunicação Host ↔ VM | Funcionando |
| Comunicação VM ↔ VM | Funcionando |
| Internal Network | Funcionando |
| Roteamento via OPNsense | Funcionando |
| WebGUI OPNsense | Pendente |
| DHCP interno | Pendente |

---

## Evolução da infraestrutura

Inicialmente as VMs se comunicavam diretamente via Host-Only e Internal Network.

Com a implementação do OPNsense, o ambiente passou a utilizar um gateway centralizado, aproximando a infraestrutura de um cenário corporativo real.

O objetivo futuro é:

- Implementar DHCP interno
- Configurar regras de firewall
- Integrar Windows Server ao ambiente
- Implementar Active Directory

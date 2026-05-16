# Ubuntu Server

## Objetivo da VM

Servidor Linux base do laboratório, utilizado para estudos de administração de sistemas,
configuração de redes virtuais e integração com os demais componentes do ambiente.

## Configuração da máquina virtual

- 2 vCPUs
- 2 GB RAM
- 20 GB Disco
- Adaptador 1: Internal Network — `intnet` (rede interna controlada pelo OPNsense)
- Adaptador 2: Bridge (acesso à internet)
- Adaptador 3: Host-Only (SSH estável)

## ISO

Ubuntu Server 24.04.4 LTS

## Instalação

Instalação padrão via ISO com usuário `igor` criado durante o processo.

## Configuração de rede

A VM possui três interfaces de rede configuradas simultaneamente:

| Interface | Modo | IP | Função |
|---|---|---|---|
| enp0s3 | Bridge | 192.168.18.39 (dinâmico) | Acesso à internet |
| enp0s8 | Host-Only | 192.168.56.10 (fixo) | SSH estável do host |
| enp0s9 | Internal Network | 192.168.100.10 (fixo) | Rede interna via OPNsense |

### IP fixo via Netplan

As interfaces `enp0s8` e `enp0s9` foram configuradas com IP estático editando o arquivo
`/etc/netplan/50-cloud-init.yaml`:

```yaml
network:
  version: 2
  ethernets:
    enp0s3:
      dhcp4: true
    enp0s8:
      dhcp4: no
      addresses:
        - 192.168.56.10/24
    enp0s9:
      dhcp4: no
      addresses:
        - 192.168.100.10/24
      routes:
        - to: default
          via: 192.168.100.1
```

Após editar, aplicar com:

```bash
sudo netplan apply
```

### Acesso SSH pelo host

```bash
ssh igor@192.168.56.10
```

## Instalação e Configuração SSH

Instalação do serviço OpenSSH para permitir acesso remoto à VM.

```bash
sudo apt install openssh-server
```

Para verificar o status do serviço SSH:

```bash
sudo service ssh status
```

Para liberar as portas do SSH no Firewall UFW do Ubuntu:

```bash
sudo ufw allow ssh
```

## Serviços instalados

Atualização do sistema:

```bash
sudo apt update && sudo apt upgrade -y
```

Ferramenta tree para exibição da estrutura hierárquica de diretórios:

```bash
sudo apt install tree -y
```

## Testes realizados

- Acesso SSH via Host-Only (`192.168.56.10`) — sucesso
- Ping para gateway OPNsense (`192.168.100.1`) — sucesso
- Ping para ubuntu-server-02 (`192.168.100.11`) — sucesso

## Problemas encontrados

### SSH não funcionava entre host Windows e VM Ubuntu Server
Modo de rede NAT não permitia acesso direto do host à VM. Solução: alteração para Bridge
no Adaptador 1 e adição de interface Host-Only com IP fixo para SSH estável.

### IP dinâmico causaria instabilidade no SSH
Interface Bridge usa DHCP do roteador doméstico, podendo mudar o IP a cada reinicialização.
Solução: configuração de IP fixo na interface Host-Only (`enp0s8`) via Netplan.

## Conclusão

VM operacional com três interfaces de rede configuradas. Acesso SSH estável via Host-Only.
Integrada à rede interna do laboratório (`192.168.100.x`) com o OPNsense como gateway.

# Ubuntu Server

## Objetivo da VM

## Configuração da máquina virtual
- 2 vCPUs
- 2 GB RAM
- 20 GB Disco
- Adaptador NAT (posteriormente alterado para Bridge)

## ISO
Ubuntu Server 24.04.4 LS

## Instalação

## Configuração de rede
A VM possui duas interfaces de rede configuradas simultaneamente:

| Interface | Modo | IP | Função |
|---|---|---|---|
| enp0s3 | Bridge | 192.168.18.39 (dinâmico) | Acesso à internet |
| enp0s8 | Host-Only | 192.168.56.10 (fixo) | SSH estável do host |

### IP fixo via Netplan

A interface `enp0s8` foi configurada com IP estático editando o arquivo `/etc/netplan/50-cloud-init.yaml`:

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
Instalação do serviço OpenSSH para permitir acesso remoto a VM.
```bash
sudo apt install openssh-server
```
Para verificar o status do serviço SSH.
```bash
sudo service ssh status
```
Por fim, para liberar as portas do SSH no Firewall UFW do Ubuntu.
```bash
sudo ufw allow ssh
```

## Serviços instalados
Atualização de sistema.
```bash
sudo apt update && sudo apt upgrade -y
```
Ferramenta tree para exibição da estrutura hierárquica dos diretórios e arquivos em formato visual de árvore.
```bash
sudo apt instal tree -y
```
## Testes realizados

## Problemas encontrados
### Serviço SSH não funcionava entre host Windows e a VM Ubuntu Server. 
Após alteração da rede de NAT para Bridge, serviço funcionou corretamente.

## Conclusão

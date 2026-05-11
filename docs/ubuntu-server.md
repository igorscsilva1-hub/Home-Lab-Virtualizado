# Ubuntu Server

## Objetivo da VM

## Configuração da máquina virtual
- 2 vCPUs
- 2 GB RAM
- 20 GB Disco
- Adaptador NAT

## ISO
Ubuntu Server 24.04.4 LS

## Instalação

## Configuração de rede

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

## Testes realizados

## Problemas encontrados

## Conclusão

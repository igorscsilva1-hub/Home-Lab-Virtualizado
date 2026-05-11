# Rede
## Topologia atual

A VM Ubuntu Server utiliza dois adaptadores simultaneamente:
- **Adaptador 1 (Bridge):** conecta a VM à rede local via roteador. IP dinâmico via DHCP. Permite acesso à internet.
- **Adaptador 2 (Host-Only):** conecta a VM diretamente ao host Windows. IP fixo `192.168.56.10`. Usado para conexão SSH mais estável.

Essa configuração garante que o IP não mude entre reinicializações da VM ou do Host.

## Topologia futura (com pfSense)

O pfSense assumirá o controle de roteamento e DHCP interno. As VMs passarão a usar Internal Network, com o pfSense como gateway, assim eliminando a dependência do roteador doméstico para comunicação entre VMs.

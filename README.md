# Laboratório de VLANs, STP e Router-on-a-Stick

Este projeto apresenta a criação de uma rede no Cisco Packet Tracer utilizando VLANs, links trunk, roteamento entre VLANs e redundância com o Spanning Tree Protocol.

## Objetivo

O objetivo do laboratório foi compreender, na prática, como segmentar uma rede utilizando VLANs, permitir a comunicação entre redes diferentes por meio de um roteador e evitar loops em uma topologia com caminhos redundantes.

## Topologia

A topologia foi composta por:

* 1 roteador Cisco 2911;
* 3 switches Cisco 2960;
* 4 computadores;
* enlaces redundantes entre os switches.

## VLANs utilizadas

| VLAN    | Rede            | Gateway      |
| ------- | --------------- | ------------ |
| VLAN 10 | 192.168.10.0/24 | 192.168.10.1 |
| VLAN 20 | 192.168.20.0/24 | 192.168.20.1 |

## Endereçamento dos computadores

| Dispositivo | VLAN | Endereço IP   | Gateway      |
| ----------- | ---: | ------------- | ------------ |
| PC0         |   10 | 192.168.10.10 | 192.168.10.1 |
| PC2         |   10 | 192.168.10.20 | 192.168.10.1 |
| PC1         |   20 | 192.168.20.10 | 192.168.20.1 |
| PC3         |   20 | 192.168.20.20 | 192.168.20.1 |

## Conceitos aplicados

* Criação e configuração de VLANs;
* Configuração de portas access;
* Configuração de links trunk;
* Encapsulamento IEEE 802.1Q;
* Configuração de subinterfaces no roteador;
* Router-on-a-Stick;
* Configuração de gateway padrão;
* Roteamento entre VLANs;
* Spanning Tree Protocol;
* Prevenção de loops;
* Redundância de enlaces;
* Testes com ICMP e ARP;
* Análise de pacotes no modo Simulation.

## Router-on-a-Stick

O roteador foi configurado com subinterfaces para atuar como gateway das VLANs.

```bash
interface gigabitEthernet 0/0
 no shutdown

interface gigabitEthernet 0/0.10
 encapsulation dot1Q 10
 ip address 192.168.10.1 255.255.255.0

interface gigabitEthernet 0/0.20
 encapsulation dot1Q 20
 ip address 192.168.20.1 255.255.255.0
```

## Spanning Tree Protocol

Como os switches foram conectados utilizando caminhos redundantes, o STP foi responsável por bloquear uma das portas para impedir a formação de loops.

Durante o teste, um enlace ativo foi desativado. O STP recalculou a topologia e liberou o caminho alternativo, mantendo a comunicação entre os dispositivos.

Comando utilizado para verificar o STP:

```bash
show spanning-tree vlan 10
show spanning-tree vlan 20
```

## Testes realizados

Foram realizados testes de comunicação:

* entre computadores da mesma VLAN;
* entre computadores de VLANs diferentes;
* entre os computadores e seus gateways;
* após a falha de um enlace;
* durante a convergência do STP.

Exemplo:

```bash
ping 192.168.10.20
ping 192.168.20.10
```

## Resultado

A comunicação dentro das VLANs e entre as diferentes redes ocorreu corretamente.

Também foi possível observar o funcionamento do STP, que impediu loops e manteve a disponibilidade da rede após a falha de um dos enlaces.

## Ferramentas utilizadas

* Cisco Packet Tracer;
* Cisco IOS;
* GitHub.

## Aprendizados

Este laboratório permitiu compreender como VLANs, trunks, roteamento e STP trabalham em conjunto para criar uma rede segmentada, organizada e redundante.


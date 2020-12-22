- [Instalación GNS3 sobre Ubuntu 20.04 LTS](#instalación-gns3-sobre-ubuntu-20.04-lts)
- [Ejercicio Core MPLS con GNS3](#ejercicio-core-mpls-con-gns3)

***

# Instalación GNS3 sobre Ubuntu 20.04 LTS

    sudo add-apt-repository ppa:gns3/ppa
    sudo apt update                                
    sudo apt install gns3-gui gns3-server
    sudo apt install xterm

    sudo usermod -a -G ubridge $USER
    sudo usermod -a -G libvirt $USER
    sudo usermod -a -G kvm $USER
    sudo usermod -a -G wireshark $USER
    reboot

## Iniciamos gns3 Server

    gns3server &

## Iniciamos gns3 GUI

    gns3 & 

## Configuración GUI

Ejecutaremos localmente:

    [ ] Run appliances in a virtual machine
    [X] Run appliances on my local computer

Configuraremos el tipo de terminal de consola:
  
    Edit / Preferences ... / General / Console applications / Console settings 
    [EDIT] Choose a predefined command: Xterm

Finalmente para empezar, crearemos un nuevo proyecto:

    File / New blank project
    
Podemos añadir por ejemplo el firmware de un Cisco que tengamos de la siguiente forma:

    File / Import appliance
      cisco-iosv.gns3a   <-- Cisco Virtual IOS allows user to run IOS on a standard computer.
    Server type: [X] Install the appliance on your local computer
***

# Ejercicio Core MPLS con GNS3

## 1. Activando OSPF en el Core MPLS

El objetivo del ejercicio es que el R4 y R6 se comuniquen entre ellos através de una conexión directa usando una red MPLS.

El core lo componen los tres equipos R1, R2 y R3.

En la capa de abajo activaremos OSPF en el area backbone 0 para los equips R1, R2 y R3.

    R1
    ====
    hostname R1
    int lo0 
    ip add 1.1.1.1 255.255.255.255
    ip ospf 1 area 0   

    int Gi0/3
    ip add 10.0.0.1 255.255.255.0
    no shut
    ip ospf 1 area 0  

    R2
    ====

    hostname R2
    int lo0
    ip add 2.2.2.2 255.255.255.255
    ip ospf 1 are 0 

    int gi0/1
    ip add 10.0.0.2 255.255.255.0
    no shut
    ip ospf 1 area 0

    int gi0/2
    ip add 10.0.1.2 255.255.255.0 
    no shut 
    ip ospf 1 area 0 

    R3
    ====
    hostname R3
    int lo0 
    ip add 3.3.3.3 255.255.255.255
    ip ospf 1 are 0 

    int Gi0/3 
    ip add 10.0.1.3 255.255.255.0 
    no shut 
    ip ospf 1 area 0 

Verificaremos que desde R1 llegamos a la loopback de R3.

    R1#ping 3.3.3.3 source lo0

## 2. Activaremos LDP en todas las interfaces del Core MPLS

Activando `mpls ldp autoconfig` en el proceso OSPF, activar el protocolo de distibución de etiquetas ( `LDP`, `Label Distribution Protocol` ) de mpls en cada interface que tenga ospf activado en el este proceso específico.

    R1
    router ospf 1
    mpls ldp autoconfig

    R2
    router ospf 1
    mpls ldp autoconfig

    R3
    router ospf 1
    mpls ldp autoconfig


***

# URLs referencia:
- https://docs.gns3.com/docs/getting-started/installation/linux
- https://www.rogerperkin.co.uk/ccie/mpls/cisco-mpls-tutorial/

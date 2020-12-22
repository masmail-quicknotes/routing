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

***

# URLs referencia:
- https://docs.gns3.com/docs/getting-started/installation/linux
- https://www.rogerperkin.co.uk/ccie/mpls/cisco-mpls-tutorial/

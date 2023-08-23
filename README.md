# a-simple-scan-with-python

#!/bin/bash

Mensajes(){
        if [ $# -eq 1 ]
        then
                mensaje=$1
                case $mensaje in
                        0)
                                ;;
                        1)
                                echo
                                echo -n "Introduce una IP :"
                                ;;
                        2)
                                echo
                                echo -n "Introduce el Puerto :"
                                ;;
                        3)
                                echo
                                echo -n "Introduce el puerto que usara Netcat :"
                                ;;
                        6)
                                echo
                                echo -n "Saliendo...."
                                echo
                                ;;
                        *)
                                ;;
                esac
        else
                echo "Error en los argumentos"
        fi
}

LeerIP(){
        read ip
        echo $ip
}

LeerPuerto(){
        read puerto
        echo $puerto
}


if [ $# -eq 0 ]
then
        salida=0
        while [ $salida -ne 6 ]
        do
                echo "Script bash menu CF"
                echo "==================="
                echo 
                echo "1) metasploit" 
                echo "2) dirbuster"
                echo "3) nmap"
                echo "4) ofrecer shell a traves de netcat en un puerto"
                echo "5) conectar con una shell remota a traves de netcat"
                echo "6) Salir"
                echo
                echo -n "introduce opcion:"
                read opcion
        case $opcion in
                1)
                        Mensajes 0
                        exec msfconsole 
                        ;;
                2)
                        Mensajes 0
                        exec dirbuster
                        ;;
                3)
                        Mensajes 1
                        ip=$(LeerIP)
                        Mensajes 2
                        puerto=$(LeerPuerto)
                        nmap -p $puerto -sS $ip
                        ;;
                4)
                        Mensajes 3
                        puerto=$(LeerPuerto)
                        netcat -v -lp $puerto
                        ;;
                5)
                        Mensajes 1
                        ip=$(LeerIP)
                        Mensajes 2
                        puerto=$(LeerPuerto)
                        netcat -n $ip -p $puerto
                        ;;
                6)
                        Mensajes 6
                        salida=6
                        ;;
        esac

        done
else
        echo "Usage: $0"
fi

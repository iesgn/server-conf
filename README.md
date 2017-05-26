# server-conf
Libros de jugadas de ansible para la configuración automatizada de servidores

## Punto de partida

Servidores con IP dinámica del rango 172.22.0.0/16 con acceso como usuario/usuario con sudo

## Copiar la clave pública al servidor

Copiamos nuestra clave pública al servidor utilizando la IP dinámica:

    ssh-copy-id -i ~/.ssh/clave.pub usuario@IP

## Añadir el servidor al inventario de ansible

Añadimos el servidor al fichero de inventario de ansible (ansible_hosts), por ejemplo:

    172.22.5.78 ansible_become_pass="usuario"

## Ejecutar el libro de jugadas

Ejecutamos el libro de jugadas que deshabilita el nombre de interfaces "raro/malo" por las habituales eth? y configura el fichero interfaces con las IPs estáticas que le proporcionemos como variable:

    ansible-playbook site.yml --extra-vars "eth0_address=172.22.X.Y eth1_address=192.168.X.Y"

## Reiniciar el servidor

Para que los cambios en los nombres de las interfaces de red se apliquen, reiniciamos el servidor, ya que ese cambio lo realiza GRUB.

TallerFebrero2026
Guía simple para usar los playbooks

============================================================

¿De qué trata este proyecto?

Este repositorio permite configurar servidores Linux de forma automática usando Ansible.

En lugar de entrar a cada máquina y hacer todo manualmente (instalar programas, cambiar configuraciones, crear usuarios, etc.), se ejecuta un comando y el sistema hace el trabajo por vos.

La idea es ahorrar tiempo y evitar errores repetitivos.

============================================================

¿Qué necesito para usarlo?

Antes de empezar, necesitás:

Una computadora con Linux (o Windows con WSL).

Ansible instalado.

Acceso por SSH a las máquinas que querés configurar.

Que esas máquinas estén encendidas y conectadas a la red.

============================================================

Instalar Ansible

En Ubuntu o Debian:

sudo apt update
sudo apt install ansible

Para verificar que quedó instalado:

ansible --version

============================================================

Cómo está organizado el proyecto

El proyecto tiene algunas carpetas importantes:

inventories/
Contiene la lista de servidores donde se aplicarán los cambios.

playbooks/
Contiene los archivos que indican qué tareas se van a ejecutar.

files/
Archivos que se copian directamente a los servidores.

templates/
Archivos que se generan dinámicamente antes de enviarse.

============================================================

El inventario

El inventario es simplemente una lista de las máquinas que van a recibir los cambios.

Ejemplo:

[ubuntu]
192.168.1.10
192.168.1.11

[centos]
192.168.1.20

Esto permite agrupar servidores y aplicar tareas solo a ciertos grupos si es necesario.

============================================================

Probar la conexión

Antes de ejecutar cambios, conviene comprobar que Ansible puede conectarse:

ansible all -i inventories/hosts.ini -m ping

Si todo está bien configurado, debería responder correctamente.

============================================================

Ejecutar un playbook

Un playbook es el archivo que contiene las instrucciones.

Para ejecutarlo:

ansible-playbook -i inventories/hosts.ini playbooks/nombre.yml

Ejemplo:

ansible-playbook -i inventories/hosts.ini playbooks/site.yml

Ansible se conectará a los servidores y aplicará las tareas definidas.

============================================================

Ejecutar solo en un grupo

Si querés aplicar cambios únicamente a un grupo específico:

ansible-playbook -i inventories/hosts.ini playbooks/site.yml --limit ubuntu

============================================================

Modo prueba (sin hacer cambios)

Si querés ver qué pasaría antes de ejecutar realmente:

ansible-playbook -i inventories/hosts.ini playbooks/site.yml --check

Esto permite detectar posibles problemas sin modificar nada.

============================================================

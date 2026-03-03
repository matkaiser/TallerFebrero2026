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

Instalar requirements necesarios

ansible-galaxy collections install -r collecctions/requirements.yaml

Esto instala las dependencias que el proyecto necesita para funcionar.


============================================================

Cómo está organizado el proyecto

El proyecto tiene algunas carpetas importantes:

collections/
Contiene la lista de dpendencias necesesarias para que funcione el proyecto.

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

En el la carpeta "inventories" está el archivo "hosts.ini" en el cual puedes ver la configuracion que deben de tener las maquinas a configurar:

[ubuntu]
Hostname: ubuntu01 
IP: 192.168.1.21
Hostname: ubuntu02 
IP: 192.168.1.22

[centos]
Hostname: centos01 
IP: 192.168.1.11
Hostname: centos02 
IP: 192.168.1.12

Usuario necesario

Es necesario que las todas las maquinas tengan un usuario sysadmin, con permisos de root. Con contrasenia: lxtaller
Para poder ejecutar los playbooks.

============================================================

Probar la conexión

Antes de ejecutar cambios, conviene comprobar que Ansible puede conectarse:

ansible all -i inventories/hosts.ini -m ping

Si todo está bien configurado, debería responder correctamente.

============================================================

Ejecutar un playbook

Para ejecutar el proyecto se utiliza:
Parado en el repositorio raiz.

ansible-playbook -i inventories/hosts.ini site.yml --ask-become-pass

Este playbook contiene todos los playbooks del proyecto concatenados.
De esta forma ansible se conectará a los servidores y aplicará las tareas definidas.

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

Disclaimer uso IA

Se utilizo IA como base de conocimiento para la mayoria de modulos utilizados en este proyecto.
Tanto gramaticalmente hablando como sus posibles atributos.

============================================================
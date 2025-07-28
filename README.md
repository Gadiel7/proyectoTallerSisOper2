Proyecto InnovaSys – Automatización con Ansible
Este proyecto automatiza la configuración de un servidor interno para la startup ficticia InnovaSys, utilizando Ansible y la organización por roles.

Se configuran dos servicios principales en un servidor Ubuntu 24.04:

🌐 Servidor Web (Intranet) con Apache

📁 Servidor de Archivos con Samba

📁 Estructura del Proyecto
proyecto-innovasys/

├── inventario.ini

├── site.yml
├── roles/
│   ├── apache/
│   │   ├── tasks/
│   │   │   └── main.yml
│   │   ├── handlers/
│   │   │   └── main.yml
│   │   └── templates/
│   │       └── index.html.j2
│   └── samba/
│       ├── tasks/
│       │   └── main.yml
│       ├── handlers/
│       │   └── main.yml
├── group_vars/
│   └── all.yml
└── README.md
🖥️ Requisitos
🧪 Entorno de pruebas
Controlador Ansible: Linux Lite (con Ansible instalado)

Nodo gestionado: Ubuntu Server 24.04 (servidor-innovasys)

Red: enp0s3 (NAT) y enp0s8 (Red interna)

✅ Software requerido
En la máquina controladora (Linux Lite):
sudo apt update
sudo apt install -y ansible openssh-client
En el servidor gestionado (Ubuntu Server):

sudo apt update
sudo apt install -y openssh-server
Asegúrate de que el nodo gestionado tenga conectividad SSH desde el nodo de control.

⚙️ Variables configurables (group_vars/all.yml)

nombre_empresa: "InnovaSys"
usuario_samba: "devuser1"
grupo_samba: "desarrolladores"
password_samba: "Innova.2025"
🧾 Inventario (inventario.ini)

[innovasys]
192.168.100.10 ansible_user=operador ansible_ssh_private_key_file=~/.ssh/id_rsa
Reemplaza operador por el nombre del usuario que usas para conectarte al servidor gestionado.

🚀 Cómo ejecutar el playbook
Clona el repositorio en tu nodo de control:

git clone https://github.com/tuusuario/proyecto-innovasys.git
cd proyecto-innovasys
Ejecuta el playbook:

ansible-playbook -i inventario.ini site.yml --ask-become-pass
Se te pedirá la contraseña sudo del usuario remoto para ejecutar tareas privilegiadas.

Verificación Final
1. Verificar la intranet (Apache)
Desde Linux Lite (nodo de control), abre un navegador:

http://192.168.100.10
Deberías ver una página con:

html
<h1>Bienvenidos a la Intranet de InnovaSys</h1>
2. Verificar el recurso compartido Samba
En el gestor de archivos de Linux Lite, accede a:


smb://192.168.100.10/Proyectos
Inicia sesión con:

Usuario: devuser1

Contraseña: Innova.2025

Crea un archivo dentro del recurso compartido para confirmar acceso completo.

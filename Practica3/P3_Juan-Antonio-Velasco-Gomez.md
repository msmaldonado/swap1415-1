**Práctica 3**
==================

- Realizado por:
	+ Juan Antonio Velasco Gómez
	+ Miguel Sanchez Maldonado

Instalando Nginx como balanceador
------------------

Primero buscamos configurar una máquina e instalarle nginx como el balanceador de carga.

Creamos una nueva máquina virtual réplica de las anteriores y la llamamos "Balanceador". Procedemos a instalar nginx en Ubuntu Server 12.04.

Lo primero que debemos hacer es importar la clave del repositorio de software:

	cd /tmp/
	wget http://nginx.org/keys/nginx_signing.key
	apt-key add /tmp/nginx_signing.key
	rm -f /tmp/nginx_signing.key

Escribimos las dos siguientes órdenes que añaden el repositorio.

	echo "deb http://nginx.org/packages/ubuntu/ lucid nginx" >> /etc/apt/sources.list
	echo "deb-src http://nginx.org/packages/ubuntu/ lucid nginx" >> /etc/apt/sources.list

Ahora ya podemos instalar el paquete del nginx:

	apt-get update
	apt-get install nginx

Uso de Nginx como balanceador
------------------

La configuración inicial de nginx no nos vale tal cual está, modificamos el fichero * /etc/nginx/conf.d/default.conf *

![Captura 1](images/nginx.png)



![Captura 2](images/haproxy.png)
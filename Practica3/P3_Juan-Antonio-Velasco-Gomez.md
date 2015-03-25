**Práctica 3:** Balanceo de carga
==================

- Realizado por:
	+ Juan Antonio Velasco Gómez
	+ Miguel Sanchez Maldonado

1. Instalando Nginx como balanceador
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

2. Uso de Nginx como balanceador
------------------

La configuración inicial de nginx no nos vale tal cual está, modificamos el fichero */etc/nginx/conf.d/default.conf*

	upstream apaches {
	 server 172.16.168.130;
 	 server 172.16.168.131;
	}

Configuramos nginx para indicarle que use ese grupo definido para pasarle las peticiones.

	server{
	 listen 80;
	 server_name m3lb;
	 access_log /var/log/nginx/m3lb.access.log;
	 error_log /var/log/nginx/m3lb.error.log;
	 root /var/www/;
	 location /
	 {
	 proxy_pass http://apaches;
	 proxy_set_header Host $host;
	 proxy_set_header X-Real-IP $remote_addr;
	 proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
	 proxy_http_version 1.1;
	 proxy_set_header Connection "";
	 }
	}

Y **reiniciamos nginx**

	sudo service nginx restart

![Captura 1](images/nginx.png)

3. Instalando haproxy como balanceador
------------------



![Captura 2](images/haproxy.png)
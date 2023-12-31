# Apache + Virtual Host

- Empezamos añadiendo en el docker compose un contenedor **apache**, un **servidor DNS** y un **cliente**.

Cuyo script quedará tal que así:

```

services:
  servidor_apache:
    container_name: asir_apache_web
    image: httpd:latest
    ports:
      - "80:80"
    # Mapeamos el directorio raíz (equipo:contenedor)  
    volumes:
      - ./paginas:/usr/local/apache2/htdocs
      - ./conf:/usr/local/apache2/conf   
    networks:
      red:
        ipv4_address: 192.168.1.14

  servidor_dns:
    container_name: asir_servidor_dns
    image: ubuntu/bind9
    ports:
      - "53:53/tcp"
      - "53:53/udp"
      #Mapeo de puertos
    volumes:
      - ./configuracion:/etc/bind
      - ./zonas:/var/lib/bind
      #Para mapear los directorios
    networks:
      red:
        ipv4_address: 192.168.1.1

  
  cliente:
    container_name: asir_cliente_web
    image: ubuntu
    platform: linux/amd64
    tty: true
    stdin_open: true
    dns:
      - 192.168.1.1
    networks:
      red:
        ipv4_address: 192.168.1.33

networks:
  red:
    external: true

```
# Apache-Virtual-Host
# Apache-Virtual-Host

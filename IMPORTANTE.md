Antes de iniciar el laboratorio se debe tener en cuenta lo siguiente:

1. Al momento de crear la primera instancia de kathara yo utilize una imagen de debian 12 descargada del sitio oficial y luego en VMbox seleccione debian 1 como imagen predeterminada,
ademas de que solo instale servicios SSH y funciones generales del sistema, nada de interfaz grafica.

2. Para instalar Kathara debera referirse a la propia wiki oficial de la misma. Instalando tambien Docker ya que es el servicio que corre los contenedores de kathara.

3. Este laboratorio y todo lo que instale lo hice en LINUX, no puedo asegurar su funcioamiento en otro SO.

Ahora si, lo importante. Para que todas las funciones del laboratorio operen de forma debida se deben instalar los siguientes servicios:

1. bind9 - apt-get install bind9, aunque es probable que se instale por defecto dependiendo de la version de debian.

2. quagga - para esto se debe elegir otra imagen por defecto en el debian utilizando el comando "kathara settings", luego navegando hacia "elegir imagen por defecto" y por ultimo
   elegir "kathara/quagga" y guardar.

3. dhcp - para este servicio lo que hice fue extender la imagen de kathara utilizando esta cadena de comandos:

docker pull kathara/quagga

docker run -tid --name quagga_dhcp kathara/quagga

docker exec -ti quagga_dhcp bash

apt-get update

apt-get install isc-dhcp-server

docker commit quagga_dhcp kathara/quagga_dhcp

docker rm -f quagga_dhcp

Es importante que se mantenga el mismo nombre o no iniciara debido a que esta aclarado en lab.conf que "router c" iniciara con la imagen por defecto de kathara/quagga_dhcp

5. apache - apt-get install apache2

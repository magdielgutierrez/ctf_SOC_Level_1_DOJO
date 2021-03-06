# ctf_SOC_Level_1_DOJO
Respuestas al CTF de análisis de trafico con Wireshark. Certificación como Analista de SOC Nivel 1

## ./challenges

- [PCAP01](#PCAP01_ejercicios)
- [PCAP02](#PCAP02)
- [PCAP03](#PCAP03)
- [PCAP04](#PCAP04)
- [PCAP05](#PCAP05-ejercicios)


    

# PCAP01 ejercicios
### Reto 0 (50 pts)
➸Favor descargar el PCAP e Importar a Wireshark , para completar el reto coloque el nombre de la archivo incluyendo la extensión.
>➟Flag: PCAP-Exercise-01.pcapng

### Reto 1 (100 pts)
➸¿Cuántos paquetes tiene el archivo PCAP?

Al abrir el archivo PCAP-Exercise-01.pcapng en Wireshark, podemos inmediantamente conocer cuantos paquetes contiene en la parte inferior.

![pc01_reto1](https://user-images.githubusercontent.com/46491988/142672097-496925df-4fdc-4cef-a13e-ffbb67465ed6.jpg)

Y rapidamente obtenemos la respuesta:
>➟Flag: 172

### Reto 2 (100 pts)
➸¿En qué página http entró el host con IP 192.168.188.128?

Usamos el siguiente filtro **ip.addr == 192.168.188.128 && http** para visualizar los paquetes capturados por HTTP.

![pc01_reto2](https://user-images.githubusercontent.com/46491988/142672509-f7f94629-bacc-4c3b-a10f-e7d68c5d82e2.jpg)

Explorando en el paquete HTPP podemos visualar el host visutado por la IP.

>➟Flag: www.facebook.com

### Reto 3 (100 pts)
➸¿Cuántos paquetes HTTPS hay en la captura?

Usamos el filtro **tcp.port==443** para visualizar todos los paquetes con HTTPS
![image](https://user-images.githubusercontent.com/46491988/142686083-2ebd655f-4a5b-41b9-ac07-4cba57b53b45.png)

En la parte inferior podemos ver la cantidad de paquetes HTTPS
>➟Flag: 144

### Reto 4 (200 pts)
➸¿Qué versión de TLS se utilizó en la mayoría de los paquetes HTTPS?

Con el filtro anterior, exploramos en el paquete y podemos identificar la version TLS
>➟Flag: TLSv1.2

# PCAP02
### Reto 0 (50 pts)
➸Favor descargar el PCAP e Importar a Wireshark , para completar el reto coloque el nombre de la archivo incluyendo la extensión.
>➟Flag: PCAP-Exercise-02.pcapng

### Reto 1 (100 pts)
➸¿Qué protocolo se utilizó en el puerto 3942?

Usamos el filtro por puerto **tcp.port==3942** y **udp.port==3942**. Solo obtenemos resultado con el filtro por UDP
![image](https://user-images.githubusercontent.com/46491988/142675608-03e3ea29-58df-4b01-96e3-0ef8dc85badf.png)

Nos fijalos en la columna _Protocol_ e identificamos cual es protocolo utilizado: SSDP (Simple Service Discovery Protocol)

>➟Flag:SSDP

### Reto 2 (100 pts)
➸¿Cuál es la dirección IP del host al que se le hizo ping dos veces?

Usamos el filtro **icmp** e identificamos  _ping request_ , podemos hacerlo mas especifico usando el filtro **icmp.type == 8**
![image](https://user-images.githubusercontent.com/46491988/142676275-73258f57-79c6-4e88-ba4d-6666da3de393.png)

Identificamos que el host destino al que se le hizo ping 2 veces.

>➟Flag:8.8.4.4

### Reto 3 (100 pts)
➸¿Cuántos paquetes de respuesta a la consulta DNS fueron capturados?

_No process_

>➟Flag:99

### Reto 4 (200 pts)
➸¿Cuál es la dirección IP del host que envió el mayor número de bytes?

_No process_
>➟Flag:No anwers


# PCAP03
### Reto 0 (50 pts)
➸Favor descargar el PCAP e Importar a Wireshark , para completar el reto coloque el nombre de la archivo incluyendo la extensión.
>➟Flag: PCAP-Exercise-03.pcapng

### Reto 1 (100 pts)
➸¿Cuál es la contraseña de WebAdmin?

Buscamos alguna tranferencia o inicio de sesion en los paquetes capturados. 

Para descubrir algun archivo en los paquetes realizamos los siguiente :

_Archivo>Extraer objetos> HTPP_ 
![image](https://user-images.githubusercontent.com/46491988/142676701-da80f530-3abe-47f4-b444-b1e7f11415ce.png)

Esto nos muestra los siguientes resultados y nos centramos en el docuemnto _password.txt_ , tenemos la opcion de guardar el archivo o obtener una vista previa del contenido:
![image](https://user-images.githubusercontent.com/46491988/142676528-9d57beac-4a55-471d-bbca-eacb1abf402a.png)

El contenido del _password.txt_ nos muestra la clave de WebAdmin 

>➟Flag: sbt123


### Reto 2 (100 pts)
➸¿Cuál es el número de versión del servidor FTP del atacante?

Buscamos una comunicacion por FTP en los paquetes capturados con el filtro *ftp* y obtenemos lo siguiente:
![image](https://user-images.githubusercontent.com/46491988/142677800-aff43852-6963-45b2-a316-1feab79ffc41.png)

Dentro de los paquetes vemos el modulo **_pyftpdlib_** utilizado para crear un servidor FTP con Phyton, esto nos indica que el atacante implemento un servidor FTP con Phyton y obtenemos la version explorando en el apartado _File Tranfers Protocol_

>➟Flag: 1.5.5


### Reto 3 (100 pts)
➸¿Qué puerto se utilizó para acceder al host Windows víctima?

Con el filtro anterior podemos revisar el apartado TCP y conocer el puerto de conexion.

![image](https://user-images.githubusercontent.com/46491988/142697053-4623f332-5441-4764-b189-dde101964f71.png)

Destination Port: 49183

>➟Flag:49183


### Reto 4 (100 pts)
➸¿Cuál es el nombre de un archivo confidencial que se encuentra en el host de Windows?


>➟Flag:



# PCAP04
## Reto 0 (50 pts)
Favor descargar el PCAP e Importar a Wireshark , para completar el reto coloque el nombre de la archivo incluyendo la extensión.
>➟Flag: PCAP-Exercise-04.pcapng

### Reto 1 (100 pts)
➸¿Con cuántos hosts diferentes se comunicó la 10.0.6.187 en el rango 10.0.6.200-253?

Vamos a ir a la pestaña de _Estadisticas>Conversaciones>IPv4_ ordenamos ascendetemente y visualizamos la comunicacion de _Address A -> Address B_ del IP 10.0.6.187 y contamos los IP en el rango indicado.

![image](https://user-images.githubusercontent.com/46491988/142682925-be0d8426-3280-42fe-b2b0-9fb6c3ed90a8.png)

Finalmente obtenemos el flag.
>➟Flag:8


### Reto 2 (100 pts)
➸¿Cuál fue la primera dirección IP con la que 10.0.6.187 inició la comunicación?

Usamos el filtro **ip.addr == 10.0.6.187** e identificar la comunicación del host, ordenamos ascendentemente para obtener la repuesta.
![image](https://user-images.githubusercontent.com/46491988/142687309-7892eeba-e148-48f2-b5f1-8773bce6a05a.png)

>➟Flag: 10.0.6.1


### Reto 3 (100 pts)
➸¿Cuál es el nombre de la estación de trabajo del controlador de dominio?

revisnado los paquetes capturadpos podemos notar que hace referencia a un active directory administrado por Kerberos 

Usamos el filtro **smb && ntlmssp**  haciendo referencia a protocolos que se utilizan para kerberos esto solo nos muestra 15 paquetes.


![image](https://user-images.githubusercontent.com/46491988/142694050-c02160be-14e4-49c2-ad6f-75e01966cdb5.png)

Revisando cada paquete podemos identificar que el paquete 3524 es un equipo con un Windows Server 2012 R2 y encontramos la respuesta explorando en el apartado SMB 

>➟Flag:212-C6S-DC1


### Reto 4 (100 pts)
➸¿Cuál es la dirección MAC del controlador de dominio?

Previamente hemos identificado el nombre del controlador de dominio, por lo que solo necesitamos buscar en el apartado de Ethernet II para identificar la MAC del Host

![image](https://user-images.githubusercontent.com/46491988/142694432-8bddf0fe-202d-43d1-b3bc-d454c159c789.png)

>➟Flag:06:90:56:51:62:12


### Reto 5 (100 pts)
➸¿Cuántos puertos UDP diferentes se utilizaron en la comunicación?

Vamos a ir a la pestaña de _Estadisticas>Conversaciones>UDP_ y contamos los puertos que se repiten en la comunicación.

![image](https://user-images.githubusercontent.com/46491988/142688262-bfee3bee-6e9a-4fa8-8b9c-dbd7f2e62b7f.png)

Identificamos los puertos _53, 137, 161, 1124, 3289, 8610, 8612_

>➟Flag: 7********************


# PCAP05 ejercicios
## Reto 0 (50 pts)
Favor descargar el PCAP e Importar a Wireshark , para completar el reto coloque el nombre de la archivo incluyendo la extensión.
>➟Flag: PCAP-Exercise-05.pcap

### Reto 1 (100 pts)
➸¿Cuál es el nombre de dominio del servidor de nombres autorizado de Atwola que tiene la dirección IP 199.7.69.1?

Vamos a la pestaña _Estadisticas>Direcciones resultas_ , luego filtramos por el IP 199.7.69.1

![image](https://user-images.githubusercontent.com/46491988/142695053-ab4f16db-d9c5-406a-8a52-83021da338b5.png)

EL filtro nos muestra el nombre de dominio.

>➟Flag:pdns4.ultradns.org


### Reto 2 (100 pts)
➸Cuando el host de la dirección IP 192.168.1.157 utiliza el servicio de nombres NetBIOS (NBNS) para anunciarse en la red, ¿qué nombre de host emite?

Usamos el filtro **ip.addr == 192.168.1.157 && nbns** esto nos muestra 24 paquetes.

![image](https://user-images.githubusercontent.com/46491988/142696385-972b780c-42e0-4c38-88ae-86687db6816a.png)

Revisando el apartado NetBIOS encontramos 2 nombres SANS y HERVIBORE que se muestra como un Workstation. 

>➟Flag:SANS


### Reto 3 (100 pts)
➸ 
>➟Flag:No anwers

### Reto 4 (100 pts)
➸¿Cuántos paquetes del protocolo de transferencia de hipertexto (HTTP) se encuentran en la captura de paquetes?

Usamos el filtro **http** y nos muestra 4 paquetes.

>➟Flag:4



Implementación de microservicios en AWS con Docker:

En este proyecto se integran tres servicios usando docker-compose para lograr el envío de notificaciones con persistencia en base de datos. Los servicios usados son: Servidor web (apache), Base de datos(mysql) y PhpMyAdmin (para visualizar en una interfaz más amigable la persistencia de datos), también usaremos para las notificaciones el Simple Notification Service de AWS (SNS).

Instrucciones: 

Necesitará una EC2 para utilizar el servicio SNS (de usarla puede abrir los puertos del punto 3 durante su creación además del 22 si se conectará a la ec2 por ssh).

1-	Instalar Docker 
Ejemplo: a) Actualizar librerías: sudo yum update –y
     b)  Instalar: sudo yum install -y docker  
    	      c) Iniciar el proceso: sudo service docker start
	
2-	Instalar Docker-compose 
Ejemplo: a) Descargar el binario: sudo curl -L "https://github.com/docker/compose/releases/latest/download/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
	  b) Darle permisos de ejecución: sudo chmod +x /usr/local/bin/docker-compose

3-	Abrir los puertos 3036, 80 , 8080  .

4-	Crear un tópico SNS y copiar su arn  .

5-	Crear una subscripción al tópico del sevicio a usar (Email, SMS ….) y confirmarla desde el servicio seleccionado (Si usó su email debe confirmarla en la solicitud recibida en el mismo). 

6-	Buscar y editar el fichero submit.php y sustitir el arn del fichero por el  que acaba de copiar en el punto 4 (El fichero se encuentra en el directorio html).

7-	Crear un rol a la EC2 y desde el IAM del rol, en los permisos agregar la política de acceso total al servicio SNS (SNSFULLACCESS).

8-	En la raíz del proyecto ejecutar: sudo docker-compose up  . 

9-	Con la ip pública de su EC2 podrá acceder al formulario de envío de mensajes, accediendo a esa ip:8080 podrá acceder a phpmyadmin  (usuario: root , password: example_password)  y en: my_database ,  tabla: form_data , podrá comprobar la persistencia de datos le los mensajes enviados. 



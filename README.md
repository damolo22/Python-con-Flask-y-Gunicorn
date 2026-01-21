# Practica Realizada por :
DAVID MORENO LÓPEZ

# Practica Tomcat y Maven: Aplicaciones Java #
Primero para esta actividad he reutilizado la maquina virtual que creé en Nginx. El primer paso ha sido instalar tanto OpenJDK, como Tomcat (el cual ha habido que crear grupos y usuarios).

Tras esto lanzamos el servidor Tomcat y le hacemos status:
![Imagen status nginx](img/cap1.png)

Pero al estar en una máquina virtual no podemos acceder al  http://localhost:8080/ para ver si funciona, asi que tenemos que modificar context.xml, y la ip para ver es esta: 192.168.56.101:8080

![Imagen status nginx](img/cap2.png)


## Configuración de la administración ##
Tenemos que definir ahora el usuario con acceso a Tomcat, para ello tenemos que modificar el archivo tomcat-users.xml.

Tras esto instalamos el administrador web:
sudo apt install -y tomcat9-admin

Y entramos en: http://192.168.56.101:8080/manager/html donde podemos ver lo siguiente:

![Imagen status nginx](img/cap3.png)

## Despliegue manual mediante GUI ##
Ahora en el administrador web tenemos que añadir el archivo WAR manualmente:
![Imagen status nginx](img/cap4.png)

## Despliegue Maven ##
Debemos instalar maven:
sudo apt-get update && sudo apt-get -y install maven
![Imagen status nginx](img/cap5.png)


Tras esto modificamos el tomcat-users.xml otravez para añadir otro usuario y los roles necesarios al usuario alumno.

Después se lo tenemos que indicar a maven con un identificador, modificamos /etc/maven/settings.xml  y añadimos:

```
<servers>
  <server>
    <id>Tomcat</id>

   <username>deploy</username>

   <password>1234</password>
  </server>
 </servers>
```

Tras esto ya podemos generar la aplicacion, con el siguiente comando:
```
mvn archetype:generate -DgroupId=org.zaidinvergeles \
                         -DartifactId=tomcat-war \
                         -Ddeployment \
                         -DarchetypeArtifactId=maven-archetype-webapp \
                         -DinteractiveMode=fa
```

![Imagen status nginx](img/cap6.png)

Tras esto entramos en tomcat-war y tendremos que modificar el archivo pom.xml añadiendo contenido, despues ejecutamos el comando para lanzarlo:
mvn tomcat7:deploy

![Imagen status nginx](img/cap7.png)
![Imagen status nginx](img/cap8.png)

## Tarea ##
Todo esto ha sido en la aplicación de prueba, ahora con la Tarea, que para ello he tenido que instalar git y hacer el clone dentro de la máquina virtual, tras esto ha habido que cambiar el pom.xml añadiendo el bloque <plugin>. Después de haber hecho todo esto el juego de piedra papel y tijera está integrado:
![Imagen status nginx](img/cap9.png)
![Imagen status nginx](img/cap10.png)

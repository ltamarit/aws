

**Índice** 

[COMENZANDO](#comenzando)  
[INSTALANDO AWS CLI](#instalando-aws-cli)  
[EL LABORATORIO](#el-laboratorio)

 

## COMENZANDO

Cuando os registréis, os llevará a vuestro panel de control general 

![](../images/ud01/Aspose.Words.e395b7c6-1e26-49fd-b372-52b960032aa8.006.png)

Y allí ya os mostrará el curso en el que estáis matriculados, haciendo click en él, veréis un lab estándar. 

![](../images/ud01/Aspose.Words.e395b7c6-1e26-49fd-b372-52b960032aa8.007.png)

En el cual para empezar a funcionar haremos click en Contenidos. 

![](../images/ud01/Aspose.Words.e395b7c6-1e26-49fd-b372-52b960032aa8.008.png)

El siguiente paso será lanzar el laboratorio para poder acceder al panel de control de AWS y poder empezar a usar sus servicios. 

Previamente tendremos que conceder permisos y decir que nos hemos leído los términos de uso: 

![](../images/ud01/Aspose.Words.e395b7c6-1e26-49fd-b372-52b960032aa8.009.png)

Una vez aceptemos se empezará a lanzar el lab.  

![](../images/ud01/Aspose.Words.e395b7c6-1e26-49fd-b372-52b960032aa8.010.png)

Ahora ya tendremos casi preparado el entorno: 

![](../images/ud01/Aspose.Words.e395b7c6-1e26-49fd-b372-52b960032aa8.011.png)

En este momento ya podremos iniciarlo, una vez iniciado tienen una duración de 4horas de trabajo, habrá que esperar un poco ya que durante el tiempo que se inicia también está preparando las credenciales para poder conectarnos por ejemplo por ssh 

![](../images/ud01/Aspose.Words.e395b7c6-1e26-49fd-b372-52b960032aa8.012.png)

Y cuando se marque en verde haciendo click en AWS podremos acceder al panel de 

control. 

![](../images/ud01/Aspose.Words.e395b7c6-1e26-49fd-b372-52b960032aa8.013.png)

![](../images/ud01/Aspose.Words.e395b7c6-1e26-49fd-b372-52b960032aa8.014.png)

## INSTALANDO AWS CLI 

AWS CLI, es el cliente de AWS mediante el cual podremos utilizar la terminal para poder trabajar con nuestro entorno en lugar de utilizar la herramienta gráfica. 

En este apartado indicaré la página de la documentación desde donde podremos ir siguiendo las instrucciones de instalación: 

[https://docs.aws.amazon.com/es_es/cli/latest/userguide/getting-started-install.html ](https://docs.aws.amazon.com/es_es/cli/latest/userguide/getting-started-install.html)

Desde aquí podremos seleccionar el sistema operativo en el que trabajamos y poder seguir las instrucciones de instalación. 

![](../images/ud01/Aspose.Words.e395b7c6-1e26-49fd-b372-52b960032aa8.015.png)

Una vez finalizada la instalación podremos comprobar la versión instalada. 

![](../images/ud01/Aspose.Words.e395b7c6-1e26-49fd-b372-52b960032aa8.016.png)

## EL LABORATORIO 

Bien, ya tenemos un laboratorio en marcha y el cliente instalado, el siguiente paso es conectarlos, para ello hay que seguir los siguientes pasos: 

Ver credenciales del laboratorio: 

![](../images/ud01/Aspose.Words.e395b7c6-1e26-49fd-b372-52b960032aa8.017.png)

Haremos click en show: 

![](../images/ud01/Aspose.Words.e395b7c6-1e26-49fd-b372-52b960032aa8.018.png)

Ahora utilizaremos el siguiente comando para enlazar la terminal con el lab. 

``aws configure``  

E iremos copiando y pegando la información que nos vaya pidiendo: 

![](../images/ud01/Aspose.Words.e395b7c6-1e26-49fd-b372-52b960032aa8.020.png)

Una vez configurado comprobaremos si podemos recuperar la información del usuario: 

``aws sts get-caller-identity``

![](../images/ud01/Aspose.Words.e395b7c6-1e26-49fd-b372-52b960032aa8.022.png)

En el caso de los labs vemos que no logra conectarse y devuelve un error. Para paliar este error accederemos a la carpeta personal del usuario y dentro de ésta hay una carpeta oculta .aws (creada cuando hemos hecho aws configure), y dentro de esta carpeta tenemos el archivo credentials, el cual tiene la información que hemos introducido antes. Ahora bien, para arreglarlo vaciaremos el contenido del archivo y copiaremos toda la información de AWS Details dentro del archivo: 

![](../images/ud01/Aspose.Words.e395b7c6-1e26-49fd-b372-52b960032aa8.023.png)

![](../images/ud01/Aspose.Words.e395b7c6-1e26-49fd-b372-52b960032aa8.024.png)

Y una vez hecho comprobaremos si nos devuelve las credenciales: 

![](../images/ud01/Aspose.Words.e395b7c6-1e26-49fd-b372-52b960032aa8.025.png)

Al ser un entorno preparado de laboratorio las credenciales devueltas son de un perfil general  (Estudiante  de  prueba)  pero  si  fueran  credenciales  reales  devolvería  el  nombre correspondiente. Destacar que Arn significa Amazon Resource Name que es el identificador que genera AWS para identificar recursos/servicios. 
9

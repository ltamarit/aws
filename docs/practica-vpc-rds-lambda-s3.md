# VPC con Subredes, Base de Datos RDS, Lambda y S3

## Objetivo General

En esta práctica se integran varios servicios de AWS para simular un entorno real y completo:

1. Creación de una **VPC con subredes públicas y privadas**.
2. Despliegue de una **instancia EC2 pública**.
3. Creación de una **base de datos RDS** en subredes privadas.
4. Creación y ejecución de una **función AWS Lambda sencilla**.
5. **Monitorización con CloudWatch** y creación de una alarma.
6. Creación y uso de un **bucket S3**. Este apartado lo haces sólo si tienes suspendido el RA4 de la primera evaluación


---

# 1. Arquitectura en AWS

La arquitectura será la siguiente:

- Una **VPC** de nombre VPC-iniciales con CIDR `10.0.0.0/16`
- Subredes:
  - Públicas:
    - `10.0.1.0/24`
    - `10.0.2.0/24`
  - Privadas:
    - `10.0.3.0/24`
    - `10.0.4.0/24`
- Componentes:
  - Internet Gateway
  - Instancia EC2 pública
  - Base de datos RDS MySQL
  - Función Lambda
  - Bucket S3
  - CloudWatch

---

# 2. Creación de la VPC

## Parámetros

- CIDR: `10.0.0.0/16`
- Dos zonas de disponibilidad
- Subredes públicas y privadas según lo especificado arriba
- Internet Gateway asociado
- Justifica por qué no se crea NAT Gateway

---

# 3. Tablas de Enrutamiento

## Subredes públicas

- `10.0.0.0/16` → local
- `0.0.0.0/0` → Internet Gateway

## Subredes privadas

- `10.0.0.0/16` → local
- Sin salida a Internet

---

# 4. Creación de la Instancia EC2 Pública

## Configuración

- AMI: Ubuntu Server 24.04 LTS
- Tipo: `t2.micro`
- Subred: pública
- IP pública habilitada

## Grupo de seguridad

- SSH (22) desde Internet
- HTTP (80) desde Internet

## Datos de usuario

```bash
#!/bin/bash
apt update
apt install -y apache2 mysql-client-core-8.0
```

---

# 5. Creación del Grupo de Subredes para RDS

Antes de crear la base de datos RDS es obligatorio crear un **Database Subnet Group**.

## Configuración

- Subredes incluidas:
  - `10.0.3.0/24`
  - `10.0.4.0/24`
- Zonas de disponibilidad distintas
- Nombre:
  - `subnet-group-rds-apellido`

Este grupo asegura que la base de datos solo se despliegue en subredes privadas.

---

# 6. Configuración de la Base de Datos RDS

## Parámetros

- Motor: **MySQL**
- Plantilla: **Entorno de pruebas**
- Identificador:
  - `bbddapellido`
- Usuario administrador:
  - Definido por el alumno
- Contraseña:
  - Definida por el alumno
- Acceso público:
  - **No**
- VPC:
  - La creada en la práctica
- Database Subnet Group:
  - El del punto 5
- Grupo de seguridad:
  - Permitir acceso solo desde la EC2 pública

---

# 7. Conexión desde EC2 a la Base de Datos

Obtener el endpoint desde la consola de RDS.

Desde la EC2 ejecutar:

```bash
mysql -h <endpoint-rds> -u admin -p
```

---

# 8. Creación de un Bucket S3. Este apartado lo haces sólo si tienes suspendido el RA4 de la primera evaluación

## Creación

- Servicio: **S3**
- Nombre del bucket:
  - `bucket-apellido-nombre`
- Región:
  - La misma que el resto de recursos
- Acceso público:
  - Bloqueado

## Prueba

- Subir un archivo `prueba.txt`
- Comprobar que aparece en el bucket

---

# 9. Creación de una Función AWS Lambda

## Configuración

- Servicio: **Lambda**
- Crear función → Desde cero
- Nombre:
  - `lambda-practica-apellido`
- Lenguaje:
  - Python 3.12
- Rol:
  - Nuevo rol con permisos básicos de CloudWatch Logs

## Código

```python
def lambda_handler(event, context):
    return {
        "statusCode": 200,
        "message": "Hola, soy nombre apellidos"
    }
```

---

# 10. Ejecución de la Función Lambda

1. Crear un evento de prueba
2. Ejecutar la función al menos **5 veces**
3. Verificar que todas las ejecuciones son correctas

---

# 11. Monitorización con CloudWatch

1. Acceder a **CloudWatch**
2. Métricas → Lambda
3. Seleccionar la función creada
4. Visualizar la métrica **Invocations**

---

# 12. Creación de una Alarma en CloudWatch

## Parámetros

- Métrica: **Invocations**
- Condición:
  - Mayor o igual que 1
- Periodo:
  - 5 minutos
- Evaluación:
  - 1 periodo
- Acciones:
  - No configurar notificaciones

Nombre de la alarma:

- `alarma-lambda-apellido`

---

# 13. Pruebas de Verificación para entregar

- Justifica por qué no has creado NAT Gateway
- Acceso web a la EC2
- Acceso por SSH a la EC2.
- Conexión MySQL desde EC2 a RDS
- RDS no accesible desde Internet
- Archivo visible en S3
- Ejecuciones de Lambda registradas
- Alarma visible en CloudWatch

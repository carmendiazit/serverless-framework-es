# serverless-framework-es

![Serverless Framework Logo](https://img.shields.io/badge/Serverless%20Framework-000000?style=for-the-badge&logo=serverless&logoColor=white)
![Node.js](https://img.shields.io/badge/Node.js-339933?style=for-the-badge&logo=node.js&logoColor=white)
![AWS Lambda](https://img.shields.io/badge/AWS%20Lambda-FF9900?style=for-the-badge&logo=awslambda&logoColor=white)
![Amazon API Gateway](https://img.shields.io/badge/Amazon%20API%20Gateway-FF9900?style=for-the-badge&logo=amazonapigateway&logoColor=white)
![Amazon SQS](https://img.shields.io/badge/Amazon%20SQS-FF9900?style=for-the-badge&logo=amazonsqs&logoColor=white)
![Amazon DynamoDB](https://img.shields.io/badge/Amazon%20DynamoDB-FF9900?style=for-the-badge&logo=amazondynamodb&logoColor=white)

Sistema de pedidos en NodeJS para correr en AWS Lambda.

## 📄 Índice

- [Descripción](#descripción)
- [Tecnologías Utilizadas](#tecnologías-utilizadas)
- [Instalación](#instalación)
- [Uso](#uso)
- [Configuración AWS](#configuración-aws)
- [Contribuciones](#contribuciones)
- [Licencia](#licencia)

---

## 📝 Descripción

Este proyecto implementa un sistema de pedidos desarrollado en Node.js, diseñado para desplegarse en AWS Lambda mediante Serverless Framework. Utiliza servicios clave de AWS como **API Gateway**, **SQS** (Simple Queue Service) y **DynamoDB** para gestionar las órdenes de manera escalable y sin servidor.

## 🚀 Tecnologías Utilizadas

* **Node.js**: Entorno de ejecución de JavaScript.
* **Serverless Framework**: Para el despliegue y gestión de aplicaciones sin servidor.
* **AWS Lambda**: Servicio de computación sin servidor.
* **Amazon API Gateway**: Para crear, publicar, mantener, monitorear y asegurar APIs a cualquier escala.
* **Amazon SQS (Simple Queue Service)**: Servicio de cola de mensajes para desacoplar componentes de aplicaciones.
* **Amazon DynamoDB**: Base de datos NoSQL completamente administrada.
* **DynamoDB Streams**: Para capturar un flujo ordenado de cambios a nivel de elemento en una tabla de DynamoDB.
* **AWS IAM (Identity and Access Management)**: Para gestionar el acceso a los servicios y recursos de AWS.

## ⚙️ Instalación

Sigue estos pasos para configurar y preparar el proyecto localmente:

1.  **Clona el repositorio:**

    ```bash
    git clone [https://github.com/carmendiazit/serverless-framework-es.git](https://github.com/carmendiazit/serverless-framework-es.git)
    cd serverless-framework-es
    ```

2.  **Verifica la versión de Node.js:**
    Asegúrate de tener Node.js instalado (se recomienda la versión 14 o superior):

    ```bash
    node -v
    ```

3.  **Instala el Framework Serverless globalmente:**

    ```bash
    npm install -g serverless
    ```

4.  **Configura tus credenciales de AWS:**
    Crea un archivo en `~/.aws/credentials` con tus claves de acceso. Reemplaza `TU_ACCESS_KEY_ID` y `TU_SECRET_ACCESS_KEY` con tus credenciales de AWS:

    ```ini
    [default]
    aws_access_key_id = TU_ACCESS_KEY_ID
    aws_secret_access_key = TU_SECRET_ACCESS_KEY
    ```

    *Alternativamente, puedes configurar las credenciales usando [AWS CLI](https://aws.amazon.com/cli/).*

5.  **Verifica la instalación de Serverless:**

    ```bash
    serverless -v
    ```

6.  **Verifica los archivos imprescindibles:**
    Asegúrate de que los siguientes archivos estén presentes en la raíz del repositorio:
    * `serverless.yml`
    * `package.json`
    * `handler.js`

## 🚀 Uso

### Despliegue del sistema

Para desplegar el sistema en AWS utilizando Serverless Framework, ejecuta el siguiente comando desde la raíz del proyecto:

```bash
serverless deploy


###Eliminación del stack
##Para eliminar completamente el stack y todos los recursos asociados de AWS:
```bash
serverless remove

☁️ Configuración AWS
Este proyecto hace uso de los siguientes servicios de Amazon Web Services:

AWS Lambda: Para la ejecución de las funciones sin servidor.
Amazon API Gateway: Como punto de entrada para las APIs REST.
Amazon SQS: Para la gestión de colas de mensajes, asegurando un procesamiento asíncrono y resiliente.
Amazon DynamoDB: Como base de datos NoSQL para almacenar la información de los pedidos.
DynamoDB Streams: Para reaccionar a los cambios en la base de datos de DynamoDB.
AWS IAM: Para la gestión de permisos y roles de los recursos.
🤝 Contribuciones
¡Las contribuciones son bienvenidas! Si deseas contribuir a este proyecto, por favor:

Haz un "fork" del repositorio.
Crea una nueva rama (git checkout -b feature/AmazingFeature).
Realiza tus cambios y commitea (git commit -m 'Add some AmazingFeature').
Sube tus cambios (git push origin feature/AmazingFeature).
Abre un "Pull Request".



📄 Licencia
Este proyecto está bajo la Licencia MIT. Consulta el archivo LICENSE para más detalles.


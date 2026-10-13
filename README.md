# Práctica 01: SecureCorp - Identidad y Cifrado

Este repositorio contiene la resolución de la Práctica 01 de la asignatura Seguridad y Alta Disponibilidad (ASIR). En ella, actuamos como administradores de sistemas de la empresa ficticia **SecureCorp** (`securecorp.local`), configurando desde cero su infraestructura de identidad, autenticación y cifrado.

## 🛠️ Tecnologías utilizadas
* **OpenLDAP**: Para el servicio de directorio de la empresa.
* **OpenSSL**: Para la creación de la Autoridad de Certificación (CA) y los certificados digitales.
* **Kerberos (MIT KDC)**: Para la autenticación segura mediante tickets sin enviar contraseñas por la red.
* **Docker y Docker Compose**: Para la virtualización ligera y el despliegue del entorno de red y servidores.

## 📋 Objetivos y Bloques de la práctica

### Bloque A: Certificados y LDAP
En este bloque configuramos el directorio de usuarios asegurando que toda comunicación esté cifrada:
1. **Autoridad de Certificación (CA):** Creación de la CA raíz de SecureCorp para firmar certificados de confianza.
2. **Certificado del Servidor LDAP:** Generación de clave privada, CSR y certificado firmado por la CA para el servidor LDAP.
3. **Directorio LDAP:** Población del directorio creando grupos (como `rrhh` y `sistemas`) y usuarios utilizando archivos LDIF.
4. **LDAPS (TLS):** Securización del servidor LDAP para que deje de escuchar en claro (puerto 389) y obligue a usar cifrado mediante TLS (puerto 636).

### Bloque B: Kerberos
Implementación de un sistema de autenticación centralizada:
1. **Reino Kerberos:** Inicialización del KDC y creación del reino `SECURECORP.LOCAL`.
2. **Principals:** Alta de usuarios y servicios (como `host/web.securecorp.local`) en la base de datos de Kerberos.
3. **Tickets:** Comprobación del funcionamiento solicitando el Ticket Granting Ticket (TGT) con `kinit` y tickets de servicio (TGS) para validación.

### Parte C: Infraestructura (Docker)
Análisis e intervención en la infraestructura subyacente del laboratorio:
* Comprensión del funcionamiento interno del script `lab.sh`.
* Creación de un `Dockerfile` personalizado para desplegar una nueva máquina que actuará como servidor web.
* Modificación del archivo `docker-compose.yml` para integrar esta nueva máquina en la red privada de la empresa y montarle los volúmenes necesarios.

### Mini-reto: Gestión de acceso
* Bloqueo temporal de una cuenta de usuario en Kerberos (simulación de vacaciones) denegando la obtención de tickets sin llegar a eliminar el usuario del sistema.

## 🚀 Uso del entorno (Script lab.sh)
El entorno está automatizado con un script para facilitar su despliegue sin comandos complejos de Docker
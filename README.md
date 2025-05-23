Sistema de Gestión de Biblioteca Digital "Letras y Páginas"
Requisitos Previos

Java Development Kit (JDK) 8 o superior
MySQL/MariaDB (incluido en XAMPP)
IDE recomendado: Visual Studio Code o IntelliJ IDEA

Estructura del Proyecto
plaintextBibliotecaDigital/
│
├── src/                # Código fuente
│   ├── modelo/         # Clases de entidades
│   ├── dao/            # Acceso a datos
│   ├── conexion/       # Gestión de conexión
│   ├── ui/             # Interfaz de usuario
│   └── util/           # Utilidades
│
├── lib/                # Librerías externas
├── bin/                # Clases compiladas
├── config/             # Configuraciones
└── scripts_sql/        # Scripts de base de datos
Configuración Inicial
Configurar Base de Datos

Iniciar XAMPP
Activar servicios MySQL/Apache
Crear base de datos:

Abrir phpMyAdmin (http://localhost/phpmyadmin/)
Crear base de datos biblioteca_digital
Ejecutar script SQL scripts_sql/creacion_bd.sql



Configuración de Conexión
Editar archivo config/db.properties:
propertiesdb.host=localhost
db.port=3306
db.name=biblioteca_digital
db.user=root
db.password=
Ejecución sin Interfaz Web (Consola)
Compilación
Crear directorio para archivos compilados y compilar clases:
powershell# Crear directorio bin
mkdir bin

# Compilar clases
javac -cp "lib/mysql-connector-j-9.2.0.jar" -d bin src/conexion/*.java
javac -cp "bin;lib/mysql-connector-j-9.2.0.jar" -d bin `
    src/dao/*.java `
    src/modelo/*.java `
    src/util/*.java `
    src/ui/*.java
Copiar config --> bin
powershellCopy-Item -Path "src/config" -Destination "bin/" -Recurse
Ejecutar Aplicación
powershell# Desde directorio del proyecto
java -cp "bin;lib/mysql-connector-j-9.2.0.jar" ui.Principal
Despliegue de Aplicación Web
Preparación del Frontend
Estructura del Proyecto Web
plaintextweb/
├── client/
│   ├── css/
│   │   └── style.css
│   └── js/
│       └── script.js
└── index.html
Conexión de Archivos Estáticos en index.html
html<link rel="stylesheet" href="./client/css/style.css">
<script src="./client/js/script.js"></script>
Bibliotecas Adicionales
Para el desarrollo del proyecto web, se han añadido las siguientes bibliotecas al directorio lib:

gson-2.1.0.jar: Biblioteca de Google para serialización y deserialización de objetos JSON
javax.servlet-api-4.0.1.jar: API de Servlet para desarrollo de aplicaciones web Java
mysql-connector-j-9.2.0.jar: Conector JDBC para MySQL
servlet-api.jar: API adicional para servlets

Uso de las Bibliotecas

Gson: Permite convertir objetos Java a JSON y viceversa
Servlet API: Proporciona clases e interfaces para crear servlets
MySQL Connector: Permite la conexión con bases de datos MySQL
Servlet API adicional: Complementa las funcionalidades de servlets

Manejo de Endpoints con LibroServlet
En el proyecto, hemos agregado la clase LibroServlet en el paquete src/handlers. Este servlet gestiona los endpoints (puntos finales) para interactuar con la aplicación de gestión de biblioteca a través de solicitudes HTTP.
¿Qué es un Servlet?
Un servlet es una clase Java que se utiliza para procesar solicitudes HTTP y generar contenido dinámico en aplicaciones web. Permite:

Recibir y procesar solicitudes HTTP
Interactuar con bases de datos
Generar respuestas para el cliente

Compilación del Proyecto Web
Compilar Clases Java
powershelljavac -cp "lib/*" -d web/WEB-INF/classes `
    src/conexion/*.java `
    src/dao/*.java `
    src/handlers/*.java `
    src/modelo/*.java `
    src/ui/*.java `
    src/util/*.java
Despliegue en Tomcat
Copiar Proyecto a Tomcat
powershell# Copiar carpeta web a webapps de Tomcat
Copy-Item -Path "web" -Destination "C:\xampp\tomcat\webapps\BibliotecaDigital" -Recurse
Acceder a la Aplicación

Navegar a: http://localhost:8080/BibliotecaDigital/web/

Notas Importantes

La carpeta lib en WEB-INF puede ser opcional
El archivo web.xml no siempre es necesario

Contribución

Reportar issues en GitHub
Pull requests son bienvenidos

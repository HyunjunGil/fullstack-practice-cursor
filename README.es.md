# 🌍 Aplicación Todo Full-Stack con Verificación de Email

Una aplicación Todo integral construida con backend Spring Boot y frontend React, que incluye autenticación segura a través de un sistema de verificación de email.

## 🌐 Idiomas Disponibles / Available Languages / 言語選択

- [🇰🇷 한국어](README.md) (Predeterminado)
- [🇺🇸 English](README.en.md)
- [🇯🇵 日本語](README.ja.md)
- [🇨🇳 中文](README.zh.md)
- [🇪🇸 Español](README.es.md)

---

## 🚀 Características Principales

### Funciones Principales
- **Autenticación de Usuario**: Sistema seguro de registro e inicio de sesión
- **Verificación de Email**: Códigos de verificación de 6 dígitos vía SMTP
- **Gestión de Todos**: Crear, leer, actualizar, eliminar y alternar estado de completado
- **Perfil de Usuario**: Gestión de información personal y configuraciones
- **Autenticación JWT**: Autenticación sin estado con tokens de actualización

### Sistema de Verificación de Email
- **Códigos de 6 Dígitos**: Códigos de verificación numéricos seguros
- **Expiración de 10 Minutos**: Expiración automática de códigos para seguridad
- **Limitación de Tasa**: Prevención de bombardeo de emails (1 minuto de espera)
- **Funcionalidad de Reenvío**: Los usuarios pueden solicitar nuevos códigos
- **Plantillas Profesionales**: Hermosas plantillas de email HTML
- **Activación de Cuenta**: Verificación de email requerida antes del login

### Características de Seguridad
- **Hash de Contraseñas**: Encriptación BCrypt
- **Validación de Entrada**: Validación integral del lado del servidor
- **Configuración CORS**: Solicitudes seguras de origen cruzado
- **Acceso Basado en Roles**: Gestión de roles de usuario y administrador
- **Rutas Protegidas**: Protección de rutas del frontend

## 🛠️ Stack Tecnológico

### Backend
- **Framework**: Spring Boot 3.x
- **Lenguaje**: Java 17+
- **Base de Datos**: H2 (en memoria)
- **Seguridad**: Spring Security con JWT
- **Email**: Spring Boot Mail con plantillas Thymeleaf
- **Herramienta de Construcción**: Gradle

### Frontend
- **Framework**: React 18+
- **Lenguaje**: JavaScript/JSX
- **Cliente HTTP**: Axios con interceptores
- **Enrutamiento**: React Router v6
- **Gestión de Estado**: Context API
- **Estilos**: Módulos CSS con diseño responsivo

## 📋 Prerrequisitos

Antes de ejecutar esta aplicación, necesitas:

- **Java 17+** instalado y configurado
- **Node.js 16+** y npm instalados
- **Gradle 7+** (o usar el wrapper incluido)
- **Cuenta de Email** para configuración SMTP (Gmail recomendado)

## 🚀 Instalación y Configuración

### 1. Clonar Repositorio
```bash
git clone <repository-url>
cd fullstack-practice-cursor
```

### 2. Configuración del Backend

#### Navegar al Directorio del Backend
```bash
cd backend
```

#### Configurar Ajustes de Email
Crear un archivo `.env` en el directorio del backend o configurar variables de entorno:

```bash
# Configuración SMTP de Gmail
export EMAIL_USERNAME=your-email@gmail.com
export EMAIL_PASSWORD=your-app-password
export EMAIL_FROM=noreply@todoapp.com

# O crear archivo .env:
EMAIL_USERNAME=your-email@gmail.com
EMAIL_PASSWORD=your-app-password
EMAIL_FROM=noreply@todoapp.com
```

#### Configuración de Contraseña de Aplicación de Gmail
1. Habilitar autenticación de 2 factores en tu cuenta de Gmail
2. Generar contraseña de aplicación:
   - Ir a configuración de cuenta de Google
   - Seguridad → Verificación en 2 pasos → Contraseñas de aplicación
   - Generar contraseña para "Correo"
   - Usar esta contraseña como `EMAIL_PASSWORD`

#### Construir y Ejecutar Backend
```bash
# Usar wrapper de Gradle
./gradlew build
./gradlew bootRun

# O usar Gradle del sistema
gradle build
gradle bootRun
```

El backend inicia en `http://localhost:8080`

### 3. Configuración del Frontend

#### Navegar al Directorio del Frontend
```bash
cd app
```

#### Instalar Dependencias
```bash
npm install
```

#### Iniciar Servidor de Desarrollo
```bash
npm start
```

El frontend inicia en `http://localhost:3000`

## 📧 Configuración de Email

### Configuración SMTP
La aplicación está preconfigurada para SMTP de Gmail:

```properties
spring.mail.host=smtp.gmail.com
spring.mail.port=587
spring.mail.username=${EMAIL_USERNAME}
spring.mail.password=${EMAIL_PASSWORD}
spring.mail.properties.mail.smtp.auth=true
spring.mail.properties.mail.smtp.starttls.enable=true
```

### Proveedores de Email Alternativos
Puedes modificar `application.properties` para otros proveedores:

#### Outlook/Hotmail
```properties
spring.mail.host=smtp-mail.outlook.com
spring.mail.port=587
```

#### Yahoo
```properties
spring.mail.host=smtp.mail.yahoo.com
spring.mail.port=587
```

## 🔐 Cuenta de Administrador Predeterminada

La aplicación crea un usuario administrador predeterminado al iniciar:

- **Nombre de Usuario**: `admin`
- **Contraseña**: `Admin123!`
- **Email**: `admin@example.com`
- **Estado**: Email verificado y habilitado

## 📱 Endpoints de API

### Autenticación
```
POST   /api/auth/register           - Registro de usuario
POST   /api/auth/verify-email       - Verificar email con código
POST   /api/auth/resend-verification - Reenviar código de verificación
POST   /api/auth/login              - Login de usuario
POST   /api/auth/logout             - Logout de usuario
GET    /api/auth/me                 - Obtener información del usuario actual
```

### Todos (Rutas Protegidas)
```
GET    /api/todos          - Obtener todos del usuario
GET    /api/todos/{id}     - Obtener todo específico
POST   /api/todos          - Crear nuevo todo
PUT    /api/todos/{id}     - Actualizar todo
DELETE /api/todos/{id}     - Eliminar todo
PATCH  /api/todos/{id}/toggle - Alternar estado de completado
```

## 🔄 Flujo de Verificación de Email

### 1. Registro de Usuario
1. El usuario completa el formulario de registro
2. El sistema crea la cuenta (deshabilitada)
3. Se genera y envía el código de verificación
4. El usuario es redirigido a la página de verificación

### 2. Verificación de Email
1. El usuario recibe el código de 6 dígitos vía email
2. El usuario ingresa el código en el formulario de verificación
3. El sistema valida el código y tiempo de expiración
4. La cuenta se activa y habilita
5. Se envía email de bienvenida
6. El usuario es redirigido a la página de login

### 3. Acceso de Login
1. El usuario inicia sesión con credenciales
2. El sistema verifica el estado de verificación de email
3. Si está verificado, se genera token JWT
4. Se permite acceso del usuario a rutas protegidas

## 🎨 Plantillas de Email

La aplicación incluye tres plantillas de email profesionales:

1. **Email de Verificación**: Mensaje de bienvenida con código de verificación
2. **Email de Bienvenida**: Enviado después de verificación exitosa
3. **Restablecimiento de Contraseña**: Para funcionalidad futura de restablecimiento

Todas las plantillas son responsivas e incluyen:
- Marca profesional
- Botones claros de llamada a la acción
- Avisos de seguridad y advertencias de expiración
- Diseño amigable para móviles

## 🧪 Pruebas

### Pruebas del Backend
```bash
cd backend
./gradlew test
```

### Pruebas del Frontend
```bash
cd app
npm test
```

### Pruebas de Email
1. Usar cuenta de email real para pruebas
2. Verificar carpeta de spam si los emails no llegan
3. Verificar que las credenciales SMTP sean correctas
4. Probar limitación de tasa enviando múltiples solicitudes

## 🐛 Solución de Problemas

### Problemas Comunes

#### Emails No Se Envían
- Verificar credenciales SMTP
- Asegurar que la contraseña de aplicación de Gmail sea correcta
- Verificar que 2FA esté habilitado en Gmail
- Verificar restricciones de firewall/red

#### Problemas de Código de Verificación
- Los códigos expiran después de 10 minutos
- Máximo 5 intentos de verificación
- 1 minuto de espera entre solicitudes de reenvío
- Verificar carpeta de spam del email

#### Errores de Construcción
- Asegurar que Java 17+ esté instalado
- Verificar compatibilidad de versión de Gradle
- Verificar que todas las dependencias estén resueltas

#### Problemas del Frontend
- Limpiar caché del navegador y localStorage
- Verificar consola para errores de JavaScript
- Asegurar que el backend esté ejecutándose en puerto 8080

### Modo Debug
Habilitar logging de debug en `application.properties`:
```properties
logging.level.com.example.todoapp=DEBUG
logging.level.org.springframework.mail=DEBUG
```

## 🔒 Consideraciones de Seguridad

- **Los códigos de verificación expiran después de 10 minutos**
- **Limitación de tasa** previene bombardeo de emails
- **Límites máximos de intentos** previenen ataques de fuerza bruta
- **HTTPS requerido en producción**
- **Variables de entorno para datos sensibles**
- **Validación de entrada en todos los endpoints**

## 🚀 Despliegue en Producción

### Variables de Entorno
Configurar valores de producción:
- `jwt.secret`: Clave secreta fuerte y única
- `spring.mail.username`: Cuenta de email de producción
- `spring.mail.password`: Contraseña de aplicación de producción
- Detalles de conexión de base de datos

### Headers de Seguridad
Habilitar headers de seguridad en producción:
- Forzar HTTPS
- Restricciones CORS
- Limitación de tasa
- Sanitización de entrada

## 📝 Contribuir

1. Hacer fork del repositorio
2. Crear rama de funcionalidad
3. Hacer cambios
4. Agregar pruebas para nueva funcionalidad
5. Enviar pull request

## 📄 Licencia

Este proyecto está licenciado bajo la Licencia MIT - ver el archivo LICENSE para detalles.

## 🤝 Soporte

Para soporte y preguntas:
- Crear issue en el repositorio
- Verificar sección de solución de problemas
- Revisar documentación de API

## 🎯 Hoja de Ruta

- [ ] Funcionalidad de restablecimiento de contraseña
- [ ] Autenticación de dos factores
- [ ] Integración de login social
- [ ] Desarrollo de aplicación móvil
- [ ] Funciones avanzadas de todo (categorías, prioridades)
- [ ] Funciones de colaboración en equipo
- [ ] Limitación de tasa de API
- [ ] Cobertura integral de pruebas

---

**¡Feliz Programación! 🎉**

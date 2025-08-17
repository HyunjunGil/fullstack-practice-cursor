# 🌍 Full-Stack Todo Application with Email Verification

A comprehensive Todo application built with Spring Boot backend and React frontend, featuring secure authentication through an email verification system.

## 🌐 Available Languages / 언어 선택 / 言語選択

- [🇰🇷 한국어](README.md) (Default)
- [🇺🇸 English](README.en.md)
- [🇯🇵 日本語](README.ja.md)
- [🇨🇳 中文](README.zh.md)
- [🇪🇸 Español](README.es.md)

---

## 🚀 Key Features

### Core Features
- **User Authentication**: Secure registration and login system
- **Email Verification**: 6-digit verification codes via SMTP
- **Todo Management**: Create, read, update, delete, and toggle completion status
- **User Profile**: Personal information and settings management
- **JWT Authentication**: Stateless authentication with refresh tokens

### Email Verification System
- **6-Digit Codes**: Secure numeric verification codes
- **10-Minute Expiry**: Automatic code expiration for security
- **Rate Limiting**: Email bombing prevention (1-minute cooldown)
- **Resend Functionality**: Users can request new verification codes
- **Professional Templates**: Beautiful HTML email templates
- **Account Activation**: Email verification required before login

### Security Features
- **Password Hashing**: BCrypt encryption
- **Input Validation**: Comprehensive server-side validation
- **CORS Configuration**: Secure cross-origin requests
- **Role-Based Access**: User and admin role management
- **Protected Routes**: Frontend route protection

## 🛠️ Technology Stack

### Backend
- **Framework**: Spring Boot 3.x
- **Language**: Java 17+
- **Database**: H2 (in-memory)
- **Security**: Spring Security with JWT
- **Email**: Spring Boot Mail with Thymeleaf templates
- **Build Tool**: Gradle

### Frontend
- **Framework**: React 18+
- **Language**: JavaScript/JSX
- **HTTP Client**: Axios with interceptors
- **Routing**: React Router v6
- **State Management**: Context API
- **Styling**: CSS modules with responsive design

## 📋 Prerequisites

Before running this application, you need:

- **Java 17+** installed and configured
- **Node.js 16+** and npm installed
- **Gradle 7+** (or use the included wrapper)
- **Email Account** for SMTP configuration (Gmail recommended)

## 🚀 Installation & Setup

### 1. Clone Repository
```bash
git clone <repository-url>
cd fullstack-practice-cursor
```

### 2. Backend Setup

#### Navigate to Backend Directory
```bash
cd backend
```

#### Configure Email Settings
Create a `.env` file in the backend directory or set environment variables:

```bash
# Gmail SMTP Configuration
export EMAIL_USERNAME=your-email@gmail.com
export EMAIL_PASSWORD=your-app-password
export EMAIL_FROM=noreply@todoapp.com

# Or create .env file:
EMAIL_USERNAME=your-email@gmail.com
EMAIL_PASSWORD=your-app-password
EMAIL_FROM=noreply@todoapp.com
```

#### Gmail App Password Setup
1. Enable 2-factor authentication in your Gmail account
2. Generate app password:
   - Go to Google Account settings
   - Security → 2-Step Verification → App passwords
   - Generate password for "Mail"
   - Use this password as `EMAIL_PASSWORD`

#### Build and Run Backend
```bash
# Use Gradle wrapper
./gradlew build
./gradlew bootRun

# Or use system Gradle
gradle build
gradle bootRun
```

Backend starts at `http://localhost:8080`

### 3. Frontend Setup

#### Navigate to Frontend Directory
```bash
cd app
```

#### Install Dependencies
```bash
npm install
```

#### Start Development Server
```bash
npm start
```

Frontend starts at `http://localhost:3000`

## 📧 Email Configuration

### SMTP Settings
The application is pre-configured for Gmail SMTP:

```properties
spring.mail.host=smtp.gmail.com
spring.mail.port=587
spring.mail.username=${EMAIL_USERNAME}
spring.mail.password=${EMAIL_PASSWORD}
spring.mail.properties.mail.smtp.auth=true
spring.mail.properties.mail.smtp.starttls.enable=true
```

### Alternative Email Providers
You can modify `application.properties` for other providers:

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

## 🔐 Default Admin Account

The application creates a default admin user on startup:

- **Username**: `admin`
- **Password**: `Admin123!`
- **Email**: `admin@example.com`
- **Status**: Email verified and enabled

## 📱 API Endpoints

### Authentication
```
POST   /api/auth/register           - User registration
POST   /api/auth/verify-email       - Verify email with code
POST   /api/auth/resend-verification - Resend verification code
POST   /api/auth/login              - User login
POST   /api/auth/logout             - User logout
GET    /api/auth/me                 - Get current user info
```

### Todos (Protected Routes)
```
GET    /api/todos          - Get user's todos
GET    /api/todos/{id}     - Get specific todo
POST   /api/todos          - Create new todo
PUT    /api/todos/{id}     - Update todo
DELETE /api/todos/{id}     - Delete todo
PATCH  /api/todos/{id}/toggle - Toggle completion status
```

## 🔄 Email Verification Flow

### 1. User Registration
1. User fills out registration form
2. System creates account (disabled)
3. Verification code generated and sent
4. User redirected to verification page

### 2. Email Verification
1. User receives 6-digit code via email
2. User enters code in verification form
3. System validates code and expiry time
4. Account activated and enabled
5. Welcome email sent
6. User redirected to login page

### 3. Login Access
1. User logs in with credentials
2. System checks email verification status
3. If verified, JWT token generated
4. User access granted to protected routes

## 🎨 Email Templates

The application includes three professional email templates:

1. **Verification Email**: Welcome message with verification code
2. **Welcome Email**: Sent after successful verification
3. **Password Reset**: For future password reset functionality

All templates are responsive and include:
- Professional branding
- Clear call-to-action buttons
- Security notices and expiry warnings
- Mobile-friendly design

## 🧪 Testing

### Backend Testing
```bash
cd backend
./gradlew test
```

### Frontend Testing
```bash
cd app
npm test
```

### Email Testing
1. Use a real email account for testing
2. Check spam folder if emails don't arrive
3. Verify SMTP credentials are correct
4. Test rate limiting by sending multiple requests

## 🐛 Troubleshooting

### Common Issues

#### Emails Not Sending
- Verify SMTP credentials
- Ensure Gmail app password is correct
- Check if 2FA is enabled in Gmail
- Verify firewall/network restrictions

#### Verification Code Issues
- Codes expire after 10 minutes
- Maximum 5 verification attempts
- 1-minute cooldown between resend requests
- Check email spam folder

#### Build Errors
- Ensure Java 17+ is installed
- Check Gradle version compatibility
- Verify all dependencies are resolved

#### Frontend Issues
- Clear browser cache and localStorage
- Check console for JavaScript errors
- Ensure backend is running on port 8080

### Debug Mode
Enable debug logging in `application.properties`:
```properties
logging.level.com.example.todoapp=DEBUG
logging.level.org.springframework.mail=DEBUG
```

## 🔒 Security Considerations

- **Verification codes expire after 10 minutes**
- **Rate limiting** prevents email bombing
- **Maximum attempt limits** prevent brute force attacks
- **HTTPS required in production**
- **Environment variables for sensitive data**
- **Input validation on all endpoints**

## 🚀 Production Deployment

### Environment Variables
Set production values:
- `jwt.secret`: Strong and unique secret key
- `spring.mail.username`: Production email account
- `spring.mail.password`: Production app password
- Database connection details

### Security Headers
Enable security headers in production:
- HTTPS enforcement
- CORS restrictions
- Rate limiting
- Input sanitization

## 📝 Contributing

1. Fork the repository
2. Create a feature branch
3. Make your changes
4. Add tests for new functionality
5. Submit a pull request

## 📄 License

This project is licensed under the MIT License - see the LICENSE file for details.

## 🤝 Support

For support and questions:
- Create an issue in the repository
- Check the troubleshooting section
- Review the API documentation

## 🎯 Roadmap

- [ ] Password reset functionality
- [ ] Two-factor authentication
- [ ] Social login integration
- [ ] Mobile app development
- [ ] Advanced todo features (categories, priorities)
- [ ] Team collaboration features
- [ ] API rate limiting
- [ ] Comprehensive test coverage

---

**Happy Coding! 🎉**

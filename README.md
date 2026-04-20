# SecureDocs - Enterprise Document Vault

![Python](https://img.shields.io/badge/Python-3.8+-blue.svg)
![Flask](https://img.shields.io/badge/Flask-2.0+-red.svg)
![SQLite](https://img.shields.io/badge/SQLite-3.x-green.svg)
![AES-256](https://img.shields.io/badge/Encryption-AES--256-purple.svg)
![2FA](https://img.shields.io/badge/2FA-TOTP-orange.svg)
![OAuth](https://img.shields.io/badge/OAuth-2.0-yellow.svg)
![License](https://img.shields.io/badge/License-MIT-green.svg)

---

## 📋 Overview

**SecureDocs** is a comprehensive enterprise-grade document management system with military-grade security features. It provides a secure platform where users can upload, sign, store, and manage documents with full protection through modern authentication, multi-factor authentication, document encryption, digital signatures, and role-based access control.

This system simulates a real-world document management application often used in legal, HR, healthcare, or enterprise settings.

---

## 🎯 Problem Statement

Organizations face critical challenges in document management:

- Unauthorized access to sensitive documents
- Lack of document integrity verification
- No digital signature authentication
- Weak authentication mechanisms
- No audit trail for document access
- Insecure document storage

**SecureDocs** addresses these challenges with a zero-trust security architecture.

---

## ✨ Features

### 🔐 Authentication & Access Control

| Feature | Description |
|---------|-------------|
| OAuth 2.0 Login | Google & GitHub integration |
| SSO Login | Auth0/Okta integration |
| Multi-Factor Authentication | TOTP-based 2FA (Google Authenticator) |
| Session Management | 15-minute token expiration |
| Role-Based UI | Dynamic interfaces per role |

### 📄 Document Vault

| Feature | Description |
|---------|-------------|
| Upload Documents | Support for PDF, DOCX, TXT |
| AES-256 Encryption | Military-grade encryption |
| SHA-256 Hashing | Document integrity verification |
| Digital Signatures | RSA-PSS with 2048-bit keys |
| HMAC Authentication | Message authentication codes |

### 👤 User Profile Management

- View and edit user profile
- Secure password policies (12+ chars, mixed case, numbers, special chars)
- Password change with current password verification

### 🛡️ Security Features

| Security Layer | Implementation |
|----------------|----------------|
| Password Hashing | PBKDF2-SHA256 |
| Document Encryption | AES-256 in EAX mode |
| Digital Signatures | RSA-2048 with PSS padding |
| Key Management | Fernet symmetric encryption |
| Audit Logging | Complete action tracing |
| Session Security | HTTPOnly, Secure, SameSite cookies |

### 👑 Role-Based Permissions

#### Admin
- Add/edit/delete users
- Manage roles
- View system audit logs
- Upload/edit/delete any document

#### User
- Register/login
- Upload/download own documents
- Sign documents digitally
- View and update own profile
- Track mood and wellness
- Manage to-do lists

---

## 🏗️ Project Structure

- **SecureDocs-Enterprise-Document-Vault/**
  - `main.py` - Main Flask application
  - `.env` - Environment variables

  - **templates/**
    - `login.html` - User login page
    - `signup.html` - Registration page
    - `dashboard.html` - User dashboard
    - `doctor_dashboard.html` - Healthcare dashboard
    - `upload.html` - Document upload
    - `documents.html` - Document list
    - `profile.html` - User profile
    - `setup_2fa.html` - 2FA setup
    - `verify_2fa.html` - 2FA verification
    - `disable_2fa.html` - 2FA removal
    - `doctor_visits.html` - Medical visits
    - `diagnoses.html` - Diagnosis records
    - `prescriptions.html` - Prescription management
    - `todo.html` - To-do list
    - `mood.html` - Mood tracking

    - **admin/**
      - `users.html` - User management
      - `edit_user.html` - Edit user
      - `add_user.html` - Add user
      - `audit_logs.html` - Audit log viewer

    - **errors/**
      - `403.html` - Forbidden
      - `404.html` - Not found
      - `500.html` - Server error

  - **static/** - CSS stylesheets and images
  - **Uploads/** - Encrypted document storage
  - **instance/** - SQLite database and instance files

---

## 🗄️ Database Schema

| Table | Description |
|-------|-------------|
| `user` | User accounts with roles, 2FA secrets, public/private keys |
| `document` | Encrypted document metadata, hashes, HMACs, signatures |
| `audit_log` | Complete system audit trail |
| `doctor_visit` | Patient appointment records |
| `diagnosis` | Medical diagnoses linked to visits |
| `prescription` | Medication prescriptions |
| `todo_item` | User to-do list items |
| `mood_entry` | Daily mood tracking entries |

---

## 🔧 How It Works

### Document Security Flow

- User Upload → File Encryption (AES-256-EAX) → Digital Signature (RSA-PSS)
- Hash Generation (SHA-256) → HMAC Generation → Secure Storage
- Integrity Verification on Download → Signature Verification → Decryption & Delivery

### Authentication Flow

- User Login → Password Verification (PBKDF2-SHA256)
- 2FA Challenge (if enabled) → TOTP Verification
- Session Creation (15-minute timeout) → Role-Based Access Control

---

## 🚀 Installation

### Requirements

- Python 3.8+
- SQLite3 (built-in with Python)
- Modern Browser (Chrome/Firefox/Edge)
- Internet connection for OAuth (optional)

### Environment Variables

Create a `.env` file in the project root:
```
Flask Configuration
SECRET_KEY=your-secret-key-here
ENCRYPTION_KEY=your-32-byte-encryption-key
HMAC_KEY=your-32-byte-hmac-key

OAuth Configuration (Optional)
GITHUB_CLIENT_ID=your-github-client-id
GITHUB_CLIENT_SECRET=your-github-secret
AUTH0_CLIENT_ID=your-auth0-client-id
AUTH0_CLIENT_SECRET=your-auth0-secret
AUTH0_DOMAIN=your-domain.us.auth0.com

Admin Configuration
ADMIN_EMAIL=admin@example.com
ADMIN_PASSWORD=AdminSecure123!
DEFAULT_ADMIN_PASSWORD=AdminSecure123!

Server Configuration
FLASK_DEBUG=False
USE_SSL_DEV=False
HOST=0.0.0.0
PORT=5000
```

### Generate Encryption Keys

```python
# Run this in Python to generate secure keys
import base64
import os

# Generate Fernet key for ENCRYPTION_KEY
fernet_key = base64.urlsafe_b64encode(os.urandom(32))
print(f"ENCRYPTION_KEY={fernet_key.decode()}")

# Generate HMAC key
hmac_key = base64.urlsafe_b64encode(os.urandom(32))
print(f"HMAC_KEY={hmac_key.decode()}")

# Generate Flask SECRET_KEY
import secrets
print(f"SECRET_KEY={secrets.token_hex(32)}")
```

### Installation Steps

1. Clone the repository
```
git clone https://github.com/yourusername/SecureDocs-Enterprise-Document-Vault.git
cd SecureDocs-Enterprise-Document-Vault
```

2. Create virtual environment
```
python -m venv venv
source venv/bin/activate # On Windows: venv\Scripts\activate
```
3. Install dependencies
```
pip install flask flask-sqlalchemy flask-login werkzeug authlib python-dotenv pyotp qrcode pycryptodome cryptography email-validator matplotlib
```

4. Create required directories
```
mkdir Uploads instance
```

5. Run the application
```
python main.py
```

6. Access the application

- Open browser to: `http://localhost:5000`

---
## 💻 Usage

### First Time Setup

1. Register a new account
2. Log in with your credentials
3. Set up Two-Factor Authentication (recommended)
4. Start uploading documents

### Default Admin Account

After first run, a default admin is created:

- **Email:** `admin@example.com`
- **Password:** `AdminSecure123!`

**⚠️ CHANGE THIS PASSWORD IMMEDIATELY AFTER FIRST LOGIN**

### Document Operations

| Action | Description |
|--------|-------------|
| Upload | Upload and encrypt documents |
| Download | Decrypt and download documents with integrity check |
| Verify | Check document integrity (hash + HMAC) |
| Delete | Remove documents (admin only for others) |
| Edit Name | Rename documents (admin only) |

---

## 🔐 Security Best Practices

- Use strong passwords (12+ chars, mixed case, numbers, symbols)
- Enable 2FA for all accounts
- Regularly review audit logs
- Use HTTPS in production
- Rotate encryption keys periodically
- Backup the SQLite database regularly
- Never commit `.env` file to version control

---

## 📊 Audit Logging

All system actions are logged with:

- Timestamp
- User ID and email
- Action performed
- Detailed metadata

### Logged Actions Include

- Login attempts (success/failure)
- Document uploads, downloads, deletions
- 2FA setup and verification
- User management (create, edit, delete)
- Role changes
- Profile updates

---

## 🔧 Future Improvements

- [ ] Implement end-to-end encrypted document sharing
- [ ] Add blockchain-based audit trail
- [ ] Integrate with cloud storage (AWS S3, Google Cloud)
- [ ] Add document versioning and history
- [ ] Implement document expiration policies
- [ ] Add watermarking for downloaded documents
- [ ] Create mobile application
- [ ] Add AI-powered document classification
- [ ] Implement biometric authentication

---

## 👥 Team Members

| Name | ID |
|------|-----|
| Mayssoune Hussein Elmasry | 2205251 |
| Maryam Waheed Zamel | 2205154 |
| Amina Ahmed Ferra | 2205225 |
| Karen Alfred | 2205236 |

---

## 📚 Technologies Used

| Technology | Purpose |
|------------|---------|
| Flask | Web framework |
| SQLAlchemy | ORM for database operations |
| SQLite | Lightweight database |
| AES-256-EAX | Document encryption |
| RSA-2048 | Digital signatures |
| PBKDF2-SHA256 | Password hashing |
| TOTP | Two-factor authentication |
| OAuth 2.0 | Social login |
| PyOTP | 2FA code generation |
| QRCode | 2FA QR code generation |
| Cryptography | Cryptographic operations |
| Bootstrap 5 | Frontend styling |

---

## 📄 License

This project is licensed under the MIT License.

---

## 🙏 Acknowledgments

- Flask and SQLAlchemy communities
- Cryptography.io for encryption libraries
- Auth0 and GitHub for OAuth integration
- Course instructors for security best practices guidance

---

## ⚠️ Disclaimer

This system is designed for educational purposes. For production deployment, additional security hardening, penetration testing, and compliance with relevant regulations (HIPAA, GDPR, etc.) are required.

---

⭐ If you find this project useful, please consider giving it a star on GitHub!

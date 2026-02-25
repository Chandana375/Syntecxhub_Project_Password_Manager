Password Manager
Overview

Password Manager is a desktop-based secure credential storage application built using Python and CustomTkinter.
The application allows users to securely store, encrypt, and retrieve account passwords using a master password system combined with strong cryptographic protection.

The project follows a modular architecture with separate components for authentication, encryption, database management, and user interface.

Features

Master password based authentication

Secure password hashing with bcrypt

AES-GCM encryption for stored credentials

Password strength analysis

Automatic password generation

Local SQLite database storage

OTP simulation during login

Cooldown protection after repeated failed login attempts

Clean GUI built with CustomTkinter

Technology Stack
Programming Language

Python 3.x

Libraries and Frameworks

CustomTkinter (GUI)

SQLite3 (Database)

bcrypt (Password hashing)

cryptography (AES encryption)

hashlib (Key derivation)

Project Structure
password_manager/
│
├── main.py                      # Application entry point
│
├── database/
│   └── db.py                    # Database logic and schema
│
├── security/
│   ├── auth.py                  # Authentication logic
│   ├── encryption.py            # AES encryption/decryption
│   ├── password_generator.py    # Password generation
│   ├── password_validator.py    # Password strength check
│   └── session.py               # Session handling
│
├── ui/
│   ├── login_ui.py              # Login interface
│   └── dashboard_ui.py          # Vault dashboard
│
├── utils/
│   ├── clipboard.py             # Clipboard handling
│   └── logger.py                # Logging utilities
│
├── requirements.txt
└── vault.db                     # Local SQLite database
Security Architecture
Master Password

The user creates a master password during first-time setup.

Passwords are hashed using bcrypt before storage.

Raw passwords are never stored.

Key Derivation

Encryption keys are generated using:

PBKDF2-HMAC-SHA256

100,000 iterations

32-byte key length

Unique salt per user

Encryption

Stored passwords are encrypted using:

AES-GCM mode

Random IV generation

Base64 encoding for storage

Installation
1. Clone the Repository
git clone <repository_url>
cd password_manager
2. Install Dependencies
pip install -r requirements.txt
Running the Application
python main.py
How It Works

On first launch, the user creates a master password.

The master password hash and salt are stored in SQLite.

Encryption key is derived from the master password.

Password entries are encrypted before being stored.

During login:

Master password is verified

Key is re-derived

OTP simulation is displayed

Dashboard allows:

Adding new credentials

Auto-generating strong passwords

Viewing decrypted credentials

Database Schema
Users Table
Field	Type	Description
id	INTEGER	Primary key
master_hash	BLOB	bcrypt hash
salt	BLOB	Random salt
Vault Table
Field	Type	Description
id	INTEGER	Primary key
website	TEXT	Website name
username	TEXT	Account username
encrypted_password	TEXT	Encrypted password
iv	TEXT	Initialization vector
notes	TEXT	Optional notes
created_at	TEXT	Timestamp
Security Notes

Data is encrypted locally.

No cloud storage or external servers are used.

Master password cannot be recovered if forgotten.

Authentication includes cooldown protection after repeated failures.

Future Improvements

Real OTP via email or authenticator app

Search and filter vault entries

Password auto-copy to clipboard

Export and backup functionality

Multi-user support

Secure session timeout

Biometric authentication integration

Author

Developed as a secure desktop credential management project using modern cryptographic practices and modular software design.

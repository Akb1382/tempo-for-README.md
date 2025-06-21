
# Secure File Transfer System over TLS with SCTP

A project for secure file transfer between client and server using the SCTP protocol and TLS encryption.

##  Project Objective
To implement a secure client-server system with user authentication and file transfer functionality, based on SCTP and using TLS for added security.

---

##  Technologies and Libraries
- Python 3
- `socket` + `ssl` for TLS
- `bcrypt` for password hashing
- `json` for user management
- SCTP (`pysctp`)
- `logging` for activity logging
- OS: Ubuntu

---

##  Features
- Secure communication via TLS
- Uses SCTP with:
  - **Multi-Homing**
  - **Multi-Streaming**
- Authentication with `username/password` (passwords stored as `bcrypt hash`)
- File operations:
  - `list` (list files on server)
  - `get` (download file)
  - `put` (upload file)
  - `delete` (delete file - admin only)
- Logs are stored in `server.log`

---

##  How to Run

### Prerequisites:

#### Before Everything

```bash 
sudo apt install libsctp-dev
sudo apt install lksctp-tools
sudo modprobe sctp
lsmod | grep sctp
```

#### Create & Activate Virtual Environment
```bash
python3 -m venv venv-sctp
source venv-sctp/bin/activate
pip install bcrypt
pip install pysctp
```

### Generate TLS Certificate:
```bash
openssl req -X509 -newkey rsa:4096 -keyout key.pm -out cert.pem -days 365 -nodes
```

### Create Users
Run the `create_users.py` file to create users with their roles.
All user data will be saved in the `users.json` file.


### Run the Server:
```bash
python3 server.py
```

### Run the Client:
```bash
python3 client.py
```

---

##  Team Members

| Role     | Name                  |
|----------|-----------------------|
| Team Lead | Amirhossein Akbari   |
| Member   | Amirhossein Alizamani |
| Member   | Mohammadhasan Khaksari |
| Member   | Seyed Ehsan Mousavi   |

---

##  Project Structure

```
├── server.py          # Server code
├── client.py          # Client code
├── create_users.py    # Users Creator 
├── users.json         # User information (hashed passwords)
├── server_files/      # Server-side file storage
├── server.log         # Server log file
├── cert.pem           # TLS certificate
├── key.pem            # TLS private key
├── requirements.txt   # Requirements lib
├── venv-sctp/         # virtual environment        
└── README.md          # This file
```

## Technical details

```
sequenceDiagram
    Client->>Server: Connect (TLS Handshake)
    Server->>Client: Request username
    Client->>Server: Send username
    Server->>Client: Request password
    Client->>Server: Send password
    Server->>Database: Verify credentials
    Database->>Server: Return auth status
    Server->>Client: Send auth result
```

---

##  Additional Notes
- Only users with the `admin` role can delete files.
- Users must log in with valid credentials (passwords are stored securely in `users.json`).
- All activities are logged in `server.log`.
- activate the `venv-sctp`(virtual environment) Before running the server and client.

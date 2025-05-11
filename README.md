# Chat-App
# Secure Java Group Chat Application

This is a secure, SSL/TLS-encrypted group chat application written in Java. It allows multiple users to connect to a server and chat in real time. All communication is encrypted, and users choose a username when joining.

## Features

- **Group chat:** All connected clients see all messages.
- **Usernames:** Users pick a name when connecting.
- **Encrypted communication:** Uses SSL/TLS with Java keystore and truststore.
- **Cross-platform:** Works on Windows, Linux, and Mac (Java required).

## Getting Started

### Prerequisites

- Java JDK 8 or higher installed on all machines.
- [keytool](https://docs.oracle.com/javase/8/docs/technotes/tools/unix/keytool.html) utility (comes with JDK).

### Folder Structure

```
ChatApp/
├── src/
│   ├── client/
│   │   └── ChatClient.java
│   └── server/
│       └── ChatServer.java
├── resources/
│   ├── keystore.jks
│   └── truststore.jks
├── bin/
```

### 1. Generate Keystore and Truststore

From your project root:

```sh
# Generate server keystore
keytool -genkeypair -alias serverkey -keyalg RSA -keysize 2048 -validity 365 -keystore resources/keystore.jks

# Export server certificate
keytool -export -alias serverkey -file resources/server.crt -keystore resources/keystore.jks

# Create client truststore and import server certificate
keytool -import -alias servercert -file resources/server.crt -keystore resources/truststore.jks
```

Use `changeit` as the password when prompted (or update your code if you use a different password).

### 2. Compile the Project

From your project root:

```sh
javac -d bin src/server/ChatServer.java src/client/ChatClient.java
```

### 3. Run the Server

```sh
java -cp bin src.server.ChatServer
```

### 4. Run the Client (in a new terminal)

```sh
java -cp bin src.client.ChatClient
```

### 5. Usage

- When prompted, enter your username.
- Type messages and press Enter to send.
- All connected users will see all messages.

## Security

- All communication is encrypted using SSL/TLS.
- Only users with the correct truststore can connect to the server.

## License

This project is for educational purposes. You may use and modify it as you wish.

---

**Enjoy secure group chatting with your friends!**

# Anonymous Chat LLD (Low Level Design)

## Intended audience

The intended audience for this document includes individuelas across the world who are interested in or affected by the -Anonymous Chat- code base.

## Intended propouse

The intended propouse of this document is to create a Low-level Design (LLD) to explain the functionality of the first iteration of -Anonymous Chat-

## Solution

### Description

*Anonymouse Chat* is a codebase designed to facilitate secure, private conversations between users while ensuring anonymity. The system aims to create a safe 
environment for users to comunicate without revealing their identities, using end-to-end encyrption and privacy-preserving techniques. The application will 
include features like real-time messaging, user authentication with anonymity preservation, and a lightweight interface. 

### Deliverable

#### Encrypter
The Encrypter module is responsible for ensuring the secure transmission of messages within the application by leveraging the RSA encryption method. This module will generate a unique pair of cryptographic keys: a private key, which remains securely stored within the user’s device, and a public key, which can be shared with other users for message encryption.

When a user sends a message, the module will utilize the recipient's public RSA key to encrypt the content, ensuring that only the intended recipient, who holds the corresponding private key, can decrypt and read the message. The Encrypter module also handles the storage and management of foreign public RSA keys received from other users, enabling seamless and secure communication between parties.

By incorporating robust encryption techniques, this module plays a critical role in maintaining privacy and data security, ensuring that sensitive information is protected against unauthorized access or interception.

##### Key Generator
The Key Generator method is a crucial component of the Encrypter module, responsible for generating a cryptographic key pair: a private key and a public key.
This process is vital for ensuring secure communication within the application.

```mermaid
flowchart
A("START") --> B("Generates private key")
B --> C{"There was an error?"}
C -->|yes| D("Returns a 'NotGeneratedKeyError'")
C -->|No| G("Stores private and public key in RAM memory")
G --> H("Returns public key")
H --> I("END")
D --> I

```

##### Foreing public key storage
The Foreign Public Key Storage method is a vital component of the Encrypter module, designed to securely handle and store public keys received from other users. 
This process ensures that the application can facilitate encrypted communication by maintaining a repository of valid public keys.

```mermaid
flowchart

A("Start") --> B("Receives the public Key as a param")
B --> C{"Is a empty key"}
C --> |Yes| D("Returns a 'NotKeyProvidedError'")
C --> |No| F{"Is it a valid key"}
F --> |No| G("Returns a 'NotValidKeyProvidedError'")
F --> |Yes| H("Stores key in memory")
H --> I("Returns stored key")
I --> J("END")
G --> J
D --> J
```

#### Message encryption
The Message Encryption method is a critical function within the Encrypter module, responsible for securely encrypting messages before they are transmitted between users.
This process ensures that the content of the messages remains confidential and can only be read by the intended recipient.

```mermaid
flowchart
Z("END")
A("START") --> B("Receives a non ecrypted message")
B --> C{"Is an empty string"}
C -->|Yes| D("Returns an 'EmptyMessageError'")
C -->|No| F("Encrypts message")
F --> G{"Encrypted successfully"}
G --> |No| H("Returns a 'MessageEncryptionError'")
G -->|Yes| I("Returns encrypted message")
H --> Z
I --> Z
D --> Z
```

### Viewer
### Server

#### Connection
```mermaid
flowchart
A("START")
Z("END")

A -->|Shows user Ip| B("Asks if waits or request a connection")
B --> C{"Waits for connection?"}
C --> |No| D("Request client IP")
D --> F("Connect")
C --> |Yes| G("Waits foreign connection request")
G --> H{"Accept incomming connection?"}
H --> |No| Z
H --> |Yes| I("Opens chat box")
F --> J{"Connected successfully"}
J -->|Yes| K("Opens chat box")
J --> |No| Z
K --> Z 
I --> Z

```

#### Message sending
This module is going to allow to send messages and store those in the database
```mermaid
flowchart

A("START")
Z("END")

```

#### Message receiving

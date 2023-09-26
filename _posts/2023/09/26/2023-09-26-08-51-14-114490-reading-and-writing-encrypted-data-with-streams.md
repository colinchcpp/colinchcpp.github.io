---
layout: post
title: "Reading and writing encrypted data with streams"
description: " "
date: 2023-09-26
tags: [encryption, datasecurity]
comments: true
share: true
---

In today's digital age, data security is of utmost importance. Encrypting sensitive information ensures that even if it falls into the wrong hands, it remains inaccessible. In this blog post, we will explore how to read and write encrypted data using streams in various programming languages.

## Using Java Streams

Java provides the `Cipher` class in the `javax.crypto` package to encrypt and decrypt data. We can leverage this class along with input and output streams to read and write encrypted data.

### Encrypting Data

```java
import javax.crypto.Cipher;
import javax.crypto.CipherOutputStream;
import javax.crypto.KeyGenerator;
import javax.crypto.SecretKey;
import java.io.FileInputStream;
import java.io.FileOutputStream;
import java.io.InputStream;
import java.io.OutputStream;

public class EncryptionExample {

    public static void encryptData(String sourceFile, String destinationFile) throws Exception {
        // Generate a secret key
        KeyGenerator keyGenerator = KeyGenerator.getInstance("AES");
        SecretKey secretKey = keyGenerator.generateKey();

        // Initialize the cipher with the secret key
        Cipher cipher = Cipher.getInstance("AES");
        cipher.init(Cipher.ENCRYPT_MODE, secretKey);

        // Create input and output streams
        InputStream inputStream = new FileInputStream(sourceFile);
        OutputStream outputStream = new FileOutputStream(destinationFile);

        // Wrap the output stream with CipherOutputStream for encryption
        CipherOutputStream cipherOutputStream = new CipherOutputStream(outputStream, cipher);

        // Read data from the input stream and write encrypted data to the output stream
        byte[] buffer = new byte[1024];
        int bytesRead;
        while ((bytesRead = inputStream.read(buffer)) != -1) {
            cipherOutputStream.write(buffer, 0, bytesRead);
        }

        // Close all streams
        cipherOutputStream.close();
        outputStream.close();
        inputStream.close();
    }

    public static void main(String[] args) throws Exception {
        String sourceFile = "data.txt";
        String destinationFile = "encrypted.bin";
        encryptData(sourceFile, destinationFile);
        System.out.println("Data encrypted successfully!");
    }
}
```

### Decrypting Data

```java
import javax.crypto.Cipher;
import javax.crypto.CipherInputStream;
import javax.crypto.SecretKey;
import javax.crypto.spec.SecretKeySpec;
import java.io.FileInputStream;
import java.io.FileOutputStream;
import java.io.InputStream;
import java.io.OutputStream;

public class DecryptionExample {

    public static void decryptData(String encryptedFile, String destinationFile, SecretKey secretKey) throws Exception {
        // Initialize the cipher with the secret key
        Cipher cipher = Cipher.getInstance("AES");
        cipher.init(Cipher.DECRYPT_MODE, secretKey);

        // Create input and output streams
        InputStream inputStream = new FileInputStream(encryptedFile);
        OutputStream outputStream = new FileOutputStream(destinationFile);

        // Wrap the input stream with CipherInputStream for decryption
        CipherInputStream cipherInputStream = new CipherInputStream(inputStream, cipher);

        // Read encrypted data from the input stream and write decrypted data to the output stream
        byte[] buffer = new byte[1024];
        int bytesRead;
        while ((bytesRead = cipherInputStream.read(buffer)) != -1) {
            outputStream.write(buffer, 0, bytesRead);
        }

        // Close all streams
        cipherInputStream.close();
        outputStream.close();
        inputStream.close();
    }

    public static void main(String[] args) throws Exception {
        String encryptedFile = "encrypted.bin";
        String destinationFile = "decrypted.txt";
        // Provide the secret key used for encryption
        SecretKey secretKey = new SecretKeySpec("yourSecretKey".getBytes(), "AES");
        decryptData(encryptedFile, destinationFile, secretKey);
        System.out.println("Data decrypted successfully!");
    }
}
```

## Using Python Streams

Python provides the `pycryptodome` library, a self-contained cryptographic library, for encrypting and decrypting data. We can use this library along with file streams to read and write encrypted data.

### Encrypting Data

```python
from Crypto.Cipher import AES

def encrypt_data(source_file, destination_file, secret_key):
    cipher = AES.new(secret_key, AES.MODE_ECB)

    with open(source_file, 'rb') as input_file:
        with open(destination_file, 'wb') as output_file:
            while True:
                data_chunk = input_file.read(16)  # Read 16 bytes at a time
                if len(data_chunk) == 0:
                    break
                elif len(data_chunk) % 16 != 0:
                    # Padding the last chunk if necessary
                    data_chunk += b' ' * (16 - (len(data_chunk) % 16))
                encrypted_data = cipher.encrypt(data_chunk)
                output_file.write(encrypted_data)

    print("Data encrypted successfully!")

if __name__ == '__main__':
    source_file = "data.txt"
    destination_file = "encrypted.bin"
    secret_key = b'your_secret_key'
    encrypt_data(source_file, destination_file, secret_key)
```

### Decrypting Data

```python
from Crypto.Cipher import AES

def decrypt_data(encrypted_file, destination_file, secret_key):
    cipher = AES.new(secret_key, AES.MODE_ECB)

    with open(encrypted_file, 'rb') as input_file:
        with open(destination_file, 'wb') as output_file:
            while True:
                data_chunk = input_file.read(16)  # Read 16 bytes at a time
                if len(data_chunk) == 0:
                    break
                decrypted_data = cipher.decrypt(data_chunk)
                output_file.write(decrypted_data.rstrip())

    print("Data decrypted successfully!")

if __name__ == '__main__':
    encrypted_file = "encrypted.bin"
    destination_file = "decrypted.txt"
    secret_key = b'your_secret_key'
    decrypt_data(encrypted_file, destination_file, secret_key)
```

## Conclusion

Encrypting and decrypting data using streams is an effective way to protect sensitive information. By leveraging the provided examples in Java and Python, you can ensure that your data remains secure throughout its lifecycle.

#encryption #datasecurity
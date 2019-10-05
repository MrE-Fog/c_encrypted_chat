# c_encrypted_chat

## Encrypted Chat System in C

Chat System where the messages are encrypted locally from one client, sent through an intermidiary server node, and decrypted at arrival by the other client, thus securing the connection from potential attacks of the server, or package sniffing. It is using a symmetric key encryption since both clients are using the same key.

## Usage:

Before running, make sure you have the required packages installed: `gcc` and `OpenSSL`.

To compile the files run the Makefile:

	$ make

Now open 3 terminal windows in this directory. On one of them, run the server:

	$ ./chat_server

On the other two, run the client to setup a connection with the server:

	$ ./chat_client

When prompted, enter your username and the key you will be using for the session. Make sure both clients have the exact same key in order to be able to communicate. Even though OpenSSL derives a SHA256 hash key from your password, for optimal security, you are recommended to use a strong key.

## Encryption:

By default, the encryption used is `AES256-CBC`, if you wish to use other types of encryption, modify the global string literal `ENCRYPTION_MODE` in the `chat_client.c` file.

In the console you will see the `BASE64` hash of the OpenSSL `AES256-CBC` ciphertext, because transfering the unrecognisable characters in the cipher text created some issues with the the strings they were stored in (i.e. added newline characters, or quotation marks).

## Real World Application:

If you would like to use this Chat System on your local network, you must set up the server on a static machine and run it through a port (you can change ports in the Makefile). If you would like to access it remotely from outside the Network, you can port forward the connection through your router, You will need to modify the `chat_client.c` files with the correct IP.

## Problem(s) Encountered:

The buffer currently is very small and can only send messages of 24 characters of length or less at a time, if you try to send more you will get a `bad magic number` OpenSSL error because the base 64 hash was not transfered completely. 
# XOR CLI Tool with Argon2 and SHA3-512

This is a command-line utility written in Rust that performs XOR-based encryption and decryption using a deterministic key derived from a user-provided password. The key is generated using Argon2 for password-based key derivation and SHA3-512 for deterministic salt derivation, making it secure and reproducible.

## Features

- **Symmetric encryption/decryption** using the XOR operation.
- **Deterministic key generation** with Argon2 and SHA3-512 to ensure the key is always the same for a given password and file.
- **Memory-based processing**, suitable for large files if sufficient RAM is available.
- Simple and easy to understand.

## Prerequisites

To run this project, you will need:

- Rust and Cargo installed. You can get them using [rustup](https://rustup.rs/).

## Building the Project

1. Clone this repository or create a new project:
   
   ```bash
   git clone <repository-url>
   cd xor
   ```

2. Build the project in release mode:
   
   ```bash
   cargo build --release
   ```

3. The compiled executable will be available in the `target/release` directory.

## Usage

The tool requires an input file, an output file, and a password. The same command can be used for both encryption and decryption because XOR is symmetric.

```bash
./target/release/xor <input_file> <output_file> <password>
```

### Example

To encrypt a file:

```bash
./target/release/xor plaintext.txt encrypted.txt mypassword
```

To decrypt the encrypted file, run the same command with the encrypted file as input:

```bash
./target/release/xor encrypted.txt decrypted.txt mypassword
```

If the password is correct, the `decrypted.txt` file will have the same content as `plaintext.txt`.

## How It Works

- **Key Generation**: The key is generated by first creating a deterministic salt from the password using SHA3-512. The password and salt are then passed to Argon2 to derive a secure key. This ensures that the same password always produces the same key, allowing decryption.
- **XOR Operation**: The XOR operation is applied byte-by-byte between the file data and the corresponding key byte. This makes the encryption and decryption processes symmetric: applying XOR again with the same key restores the original content.

## Limitations and Security Considerations

- This tool is **not recommended for highly sensitive data**. While Argon2 and SHA3-512 are strong components, the XOR operation itself is not secure against sophisticated cryptographic attacks if the same password is reused.
- The use of a deterministic key makes this method more secure than a simple repeating password but is still vulnerable if the password is weak.
- Modern cryptographic methods, like AES, are recommended for use cases where strong security is needed.

## Disclaimer

This project is for educational purposes only. Do not use it for protecting sensitive data.

## License

This project is licensed under the MIT License. Feel free to use, modify, and distribute it as needed.

## Contribution

Contributions are welcome! Feel free to open issues or submit pull requests to improve the project.

## Contact

If you have any questions or suggestions, feel free to contact me at [your-email@example.com].


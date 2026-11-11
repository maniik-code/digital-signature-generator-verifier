# Digital Signature Generator and Verifier

A Java Spring Boot web application for a Cryptography and Cyber Security mini project.

## Features
- Generate a 2048-bit RSA public/private key pair.
- Sign an uploaded file using `SHA256withRSA`.
- Verify a file's digital signature using the matching RSA public key.
- Display the SHA-256 digest of the file.
- Demonstrate tamper detection: changing the file after signing should make verification fail.

## Requirements
- JDK 17 or later
- Maven 3.6.3 or later
- A modern web browser

## Run on Windows
1. Install JDK 17 and Maven.
2. Extract this ZIP file.
3. Open Command Prompt in the extracted `digital-signature-verifier` folder.
4. Check installation:
   ```bash
   java -version
   mvn -version
   ```
5. Start the application:
   ```bash
   mvn spring-boot:run
   ```
6. Open `http://localhost:8080` in your browser.

The first Maven run may need an internet connection to download dependencies.

## Demonstration steps
1. Click **Generate RSA Keys**.
2. Download and securely keep both keys. Do not share the private key.
3. Choose a small PDF or TXT file under 10 MB in **Sign a document**.
4. Click **Generate Digital Signature** and download `signature.txt`.
5. Choose the same original file in **Verify a document**. Paste the signature and public key.
6. Click **Verify Signature**. The result should be VALID.
7. Make a copy of the file and change its contents. Select the changed copy and verify again. The result should be INVALID.

## Cryptographic concepts
- RSA-2048: asymmetric public-key algorithm.
- SHA-256: cryptographic hash function.
- SHA256withRSA: digital-signature algorithm that hashes the document and signs the digest using the RSA private key.

## API endpoints
- `POST /api/keys` — generate an RSA key pair; returns Base64-encoded PKCS#8 private key and X.509 public key.
- `POST /api/sign` — multipart fields `file` and `privateKey`.
- `POST /api/verify` — multipart fields `file`, `signature`, and `publicKey`.

## Important security notes
This is an educational local demo, not a production signing service.
- The private key is sent from the browser to the local Java backend for signing. Run locally and do not expose this demo to the public internet.
- The demo does not encrypt documents; digital signatures prove authenticity and integrity, not confidentiality.
- Protect private-key files with appropriate access controls. Never email or publish a private key.
- For real deployments, use authenticated users, HTTPS, secure key storage or hardware-backed keys, CSRF protections, audit controls, and strict upload validation.

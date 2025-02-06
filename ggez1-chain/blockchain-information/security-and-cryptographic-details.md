# Security & Cryptographic Details

**Address Generation & Format:**\
The Cosmos SDK uses Bech32 encoding with a custom prefix (e.g., ggez for GGEZ1 Chain). Bech32 encoding provides error-detection and human-readable parts (HRP), making addresses recognizable and compatible within the ecosystem.

**Offline Address & Private Key Generation:**\
Use the SECP256k1 curve for key generation. Derive the public key from the private key using elliptic curve multiplication. Address Derivation

**Regular Verification Rules for Addresses:** /^ggez\[A-Za-z0-9]{30,80}$/

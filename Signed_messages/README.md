<img width="1100" height="595" alt="1_uLPKsIZCJEBKF4iyHEt2jg" src="https://github.com/user-attachments/assets/e5e041f8-035a-4e6a-916f-8d6608306d33" />
This is a challenge that helps up understand the concept of encryption used in the most advanced RSA techniques. Even this can be exploited and be decrypted if the algorithm is not secure.

This is a site where we can send messages to others that is encrypted in the transit and can’t be accesses by others. Each user who has the account in the site will have a private and a public key that will be used to decrypt the message. Also the decrypted messages are hashed and salted.

After creating our account we will have can send messages and also we can verify our digital signature of the message in the verify section.

So first we can go with the traditional method of reconnaissance. NMAP tool can be used..

Press enter or click to view image in full size
<img width="840" height="510" alt="1_g48mAOrS2TvSESKjrGxpWg" src="https://github.com/user-attachments/assets/1472e768-1ad6-47a9-ba60-46b82a99b100" />
Since we are sure that the there is only 2 services and the UPnP is service a networking protocol that allows devices like gaming consoles, smart home gadgets, and computers to automatically configure routers to open specific network ports. So we can try to do directory search and find is there any vulnerable endpoints.
<img width="846" height="552" alt="1_jddbrg20_B8bLs0nmBumuw" src="https://github.com/user-attachments/assets/acce4a51-9fdb-4d8a-9e68-386aaace4ee2" />
Here we found a endpoint named (/debug) and it displayed the method that is used to get the digital signature. So by analyzing the method and with the help of AI we can make a exploit script and be executed and get the digital signature of a message that is sent.
So with this logic, we get the digital signature of the admin. In the site we can see a message that was sent by the admin, we can use that message to get the digital signature and get the flag.

The admin message “Welcome to LoveNote! Send encrypted love messages this Valentine’s Day. Your communications are secured with industry-standard RSA-2048 digital signatures.”

The code that was used to exploit the encryption..

“””
CTF Exploit: Forging RSA signatures via deterministic key derivation.

Vulnerability: Private keys are derived from username using a known seed pattern:
seed = f”{username}_lovenote_2026_valentine”
p = next_prime(SHA256(seed))
q = next_prime(SHA256(seed + b”pki”))

Since this is fully deterministic and the pattern is known,
we can reconstruct any user’s private key and forge signatures.
“””

import hashlib
import base64
from sympy import nextprime
from cryptography.hazmat.primitives.asymmetric import padding, rsa
from cryptography.hazmat.primitives.asymmetric.rsa import (
RSAPrivateNumbers, RSAPublicNumbers, rsa_crt_iqmp, rsa_crt_dmp1, rsa_crt_dmq1
)
from cryptography.hazmat.primitives import hashes
from cryptography.hazmat.backends import default_backend

# ─────────────────────────────────────────────
# Step 1: Reconstruct private key from username
# ─────────────────────────────────────────────

def reconstruct_private_key(username: str):
“””
Reproduce the broken key generation exactly.
Anyone who knows the username can do this.
“””
seed = f”{username}_lovenote_2026_valentine”.encode()

# Derive p
hash_p = hashlib.sha256(seed).hexdigest()
p = nextprime(int(hash_p, 16))

# Derive q
hash_q = hashlib.sha256(seed + b”pki”).hexdigest()
q = nextprime(int(hash_q, 16))

# RSA math
n = p * q
e = 65537
phi = (p — 1) * (q — 1)
d = pow(e, -1, phi) # modular inverse

# Build key object
public_numbers = RSAPublicNumbers(e, n)
private_numbers = RSAPrivateNumbers(
p, q, d,
rsa_crt_dmp1(d, p),
rsa_crt_dmq1(d, q),
rsa_crt_iqmp(p, q),
public_numbers
)
private_key = private_numbers.private_key(default_backend())

print(f”[✓] Private key reconstructed for username: ‘{username}’”)
print(f” n = {hex(n)[:60]}…”)
return private_key

# ─────────────────────────────────────────────
# Step 2: Forge a signature for any message
# ─────────────────────────────────────────────

def forge_signature(username: str, message: str) -> dict:
“””
Forge a valid RSA-PSS signature for any message,
for any user whose key was generated with the broken scheme.
“””
private_key = reconstruct_private_key(username)

signature = private_key.sign(
message.encode(),
padding.PSS(
mgf=padding.MGF1(hashes.SHA256()),
salt_length=padding.PSS.MAX_LENGTH
),
hashes.SHA256()
)

sig_hex = signature.hex()
print(f”[✓] Signature forged for message: ‘{message}’”)
print(f” Signature (hex): {sig_hex[:60]}…”)

return {
“username”: username,
“message”: message,
“forged_signature”: sig_hex
}

# ─────────────────────────────────────────────
# Step 3: Verify the forged signature passes
# ─────────────────────────────────────────────

def verify_forged_signature(bundle: dict) -> bool:
“””
Confirm the forged signature verifies correctly
against the reconstructed public key.
“””
private_key = reconstruct_private_key(bundle[“username”])
public_key = private_key.public_key()
signature = bytes.fromhex(bundle[“forged_signature”])

try:
public_key.verify(
signature,
bundle[“message”].encode(),
padding.PSS(
mgf=padding.MGF1(hashes.SHA256()),
salt_length=padding.PSS.MAX_LENGTH
),
hashes.SHA256()
)
print(“[✓] Forged signature VERIFIED — exploit successful!”)
return True
except Exception as e:
print(f”[✗] Verification failed: {e}”)
return False

# ─────────────────────────────────────────────
# Run the exploit
# ─────────────────────────────────────────────

if __name__ == “__main__”:
TARGET_USER = “admin” # ← change to CTF target username
TARGET_MESSAGE = “Welcome to LoveNote! Send encrypted love messages this Valentine’s Day. Your communications are secured with industry-standard RSA-2048 digital signatures.” # ← change to CTF target message

print(“=” * 55)
print(“ CTF Exploit: Deterministic RSA Key Forge”)
print(“=” * 55)

bundle = forge_signature(TARGET_USER, TARGET_MESSAGE)
verify_forged_signature(bundle)

print(“\n[Bundle to submit]”)
print(f” username : {bundle[‘username’]}”)
print(f” message : {bundle[‘message’]}”)
print(f” signature : {bundle[‘forged_signature’]}”)
print(f”\n (hex, {len(bundle[‘forged_signature’])//2} bytes)”)

The output we get from this code is the digital signature and by the /verify endpoint we can use this digital signature and get the flag.

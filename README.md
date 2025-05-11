Generate private and public key pair, so that the broker can sign commands
after it verifies the credentials.

```
# 1) Generate a 2048-bit RSA private key (unencrypted)
openssl genrsa -out private.pem 2048

# 2) Derive the public key from that private key
openssl rsa -in private.pem -pubout -out public.pem
```

for shorter keys and signatures, use the following commands to generate the
keys:

```
# Generate a new EC private key on the prime256v1 curve
openssl genpkey \
  -algorithm EC \
  -pkeyopt ec_paramgen_curve:prime256v1 \
  -pkeyopt ec_param_enc:named_curve \
  -out p256_private.pem

# Extract the matching public key
openssl pkey -in p256_private.pem -pubout -out p256_public.pem
```

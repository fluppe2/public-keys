# Public Cryptographic Keys and Certificates

This repository contains my public cryptographic keys and certificates for integrity protection, authenticity, and confidentiality of e-mail communication.

Prof. Dr. Stavros Kousidis  
Cyber Security Engineering  
TH Köln – University of Applied Sciences

Email: [stavros.kousidis@th-koeln.de](mailto:stavros.kousidis@th-koeln.de)  

Webpage: <https://www.th-koeln.de/en/person/stavros.kousidis/>

---

# Choosing a Certificate

For **traditional OpenPGP (v4)**-compatible email software, use:

[`openpgp/stavros-kousidis-openpgp-v4-public-governikus.asc`](openpgp/stavros-kousidis-openpgp-v4-public-governikus.asc)

This certificate provides:

- Ed25519 for certifications and signatures
- Curve25519 for encryption
- third-party identity certification by Governikus

For **post-quantum OpenPGP (v6)** based on RFC 9580 and RFC 9980, use:

[`openpgp/stavros-kousidis-openpgp-v6-rfc9980-public.asc`](openpgp/stavros-kousidis-openpgp-v6-rfc9980-public.asc)

This certificate provides composite:

- ML-DSA-65 + Ed25519 for certifications, signatures and authentications
- ML-KEM-768 + X25519 for encryption

For **traditional S/MIME**-capable email software, use either:

[`smime/stavros-kousidis-smime-public.pem`](smime/stavros-kousidis-smime-public.pem)

or the DER-encoded equivalent:

[`smime/stavros-kousidis-smime-public.cer`](smime/stavros-kousidis-smime-public.cer)

This certificate provides:

- RSA public key with 4096-bit modulus for digital signatures and key encipherment
- RSASSA-PKCS1-v1_5 with SHA-256 certificate signature

---

## Repository Contents

```text
public-keys/
├── README.md
├── openpgp/
│   ├── governikus-openpgp-public-key.asc
│   ├── stavros-kousidis-openpgp-v4-public-governikus.asc
│   └── stavros-kousidis-openpgp-v6-rfc9980-public.asc
└── smime/
    ├── stavros-kousidis-smime-public.cer
    └── stavros-kousidis-smime-public.pem
```

## OpenPGP tooling

The OpenPGP examples in this repository use Sequoia PGP and its `sq`
command-line tool. This keeps the inspection workflow consistent across the
traditional OpenPGP v4 certificate and the RFC 9980 post-quantum v6 certificate.

---

# OpenPGP – Traditional (v4)

Public certificate:

[`openpgp/stavros-kousidis-openpgp-v4-public-governikus.asc`](openpgp/stavros-kousidis-openpgp-v4-public-governikus.asc)

Identity

```text
Stavros Kousidis <stavros.kousidis@th-koeln.de>
```

Primary-key fingerprint

```text
8274 22C9 50AA 8230 021C 2416 4069 B017 6EDD 44BE
```

Key ID:

```text
4069B0176EDD44BE
```

Validity:

```text
2026-09-10 – 2029-12-31
```

Algorithms and key structure 

```text
Ed25519 primary key [Certifications and signatures]
│
├── User ID
│   ├── self-certification
│   └── Governikus certification
│
└── Curve25519 encryption subkey
    └── subkey binding signature
```

## Governikus certification

The User ID

```text
Stavros Kousidis <stavros.kousidis@th-koeln.de>
```

has been certified by the [Governikus OpenPGP key authentication service](https://pgp.governikus.de/?lang=EN) using the online identification function of my German identity card.

The corresponding Governikus public certification key is included in this repository for convenience:

[`openpgp/governikus-openpgp-public-key.asc`](openpgp/governikus-openpgp-public-key.asc)

Further information about the certification key, including its fingerprint and validity, is available on the [official Governikus website](https://www.governikus.de/loesungen/kundenprojekte/open-pgp-schluessel/#openpgp).

## Inspection with Sequoia PGP

Inspect my conventional OpenPGP certificate using:

```bash
sq inspect openpgp/stavros-kousidis-openpgp-v4-public-governikus.asc
```

Inspect the Governikus certification key using:

```bash
sq inspect openpgp/governikus-openpgp-public-key.asc
```

---

# OpenPGP – Post-Quantum (v6)

This setup is based on OpenPGP v6 as specified in RFC 9580 and extended with post-quantum cryptographic algorithms defined in RFC 9980.

Public certificate:

[`openpgp/stavros-kousidis-openpgp-v6-rfc9980-public.asc`](openpgp/stavros-kousidis-openpgp-v6-rfc9980-public.asc)

The certificate contains two User IDs:

```text
Stavros Kousidis
<stavros.kousidis@th-koeln.de>
```

Primary-key fingerprint

```text
535399223B32DDA0F12EC002108684C52754390AEE8342267EB7A017CFA348DE
```

Validity:

```text
2026-09-11 – 2031-09-11
```

Algorithms and key structure

```text
ML-DSA-65 + Ed25519 primary key [Certification]
│
├── User ID
│   ├── Stavros Kousidis
│   └── self-certification
│
├── User ID
│   ├── <stavros.kousidis@th-koeln.de>
│   └── self-certification
│
├── ML-DSA-65 + Ed25519 signature subkey
│   └── subkey binding signature
│
├── ML-DSA-65 + Ed25519 authentication subkey
│   └── subkey binding signature
│
└── ML-KEM-768 + X25519 encryption subkey
    └── subkey binding signature
```

## Software support

As of September 2026, support for RFC 9980 and these post-quantum OpenPGP
algorithms is not generally available in mainstream graphical email clients.

A current version of Sequoia PGP's `sq` command-line tool is required
for full RFC 9980 support. Use `sq` 1.4.0 or later.

## Inspection with Sequoia PGP

```bash
sq inspect openpgp/stavros-kousidis-openpgp-v6-rfc9980-public.asc
```

Traditional OpenPGP implementations that do not support OpenPGP v6 keys or RFC
9980 algorithms may not be able to parse or use this certificate.

## Certification status

Unlike my traditional OpenPGP certificate, this RFC 9980 certificate has not
been certified by the Governikus OpenPGP signature service because RFC 9980 is
not yet supported.

---

# S/MIME

The S/MIME certificate is provided in two encodings.

### PEM

[`smime/stavros-kousidis-smime-public.pem`](smime/stavros-kousidis-smime-public.pem)

### DER

[`smime/stavros-kousidis-smime-public.cer`](smime/stavros-kousidis-smime-public.cer)

Both files contain the same X.509 end-entity certificate.

## Identity

Subject:

```text
emailAddress=stavros.kousidis@th-koeln.de
```

Subject Alternative Name:

```text
stavros.kousidis@th-koeln.de
```

## Issuer

```text
C=GR
O=Hellenic Academic and Research Institutions CA
CN=GEANT S/MIME RSA 1
```

The certificate was issued through HARICA (Hellenic Academic and Research
Institutions Certification Authority).

## Algorithms

Public key:

- RSA-4096

Certificate signature:

- RSASSA-PKCS1-v1_5 with SHA-256
- `sha256WithRSAEncryption`

Key usage:

- Digital Signature
- Key Encipherment

Extended key usage includes:

- E-mail Protection
- TLS Web Client Authentication

## Validity

```text
Not Before: 2026-09-10 12:34:58 UTC
Not After:  2028-09-09 12:34:58 UTC
```

## SHA-256 fingerprint

```text
E9:49:97:AE:1B:7C:DD:80:D9:84:F0:D5:28:74:C3:8C:2C:5F:B3:10:B7:CF:B4:53:5D:38:E0:26:BA:0E:33:2A
```

## Verification with OpenSSL

The PEM certificate can be inspected using:

```bash
openssl x509 \
    -in smime/stavros-kousidis-smime-public.pem \
    -noout \
    -subject \
    -issuer \
    -dates \
    -fingerprint \
    -sha256
```

For a complete certificate dump:

```bash
openssl x509 \
    -in smime/stavros-kousidis-smime-public.pem \
    -noout \
    -text
```

---

# Note on authorship

Parts of this documentation were drafted with the assistance of generative AI
and subsequently reviewed and verified by the repository owner.

## Overview
This methodology is based on the multi-factor recovery. This assumes that there is no a single location where the private key, its backup, or encrypted form, can be stored. Instead, the private key is encrypted with multiple user secrets. Each user secret is stored in a different, secure location. This makes it harder for an attacker to steal the private key, since they would have to compromise multiple locations in order to recover it.

Consider the following two functions:

> f(pk, password, us<sub>1</sub>, us<sub>2</sub>, ..., us<sub>n</sub>) = signature
>
> g(signature, password, us<sub>1</sub>, us<sub>2</sub>, ..., us<sub>n</sub>) = pk

where
- **pk** is the private key
- **password** is the user's password
- **us<sub>1</sub>, us<sub>2</sub>, ..., us<sub>n</sub>** are the user secrets
- **signature** is the signature of the message

For any give private key `pk`, the user provides the password `password` and the system generates random user secrets `us`. The function `f` is used to generate a signature `signature`.
The signature is stored on chain. The user secrets are stored in secure locations. The password is stored in the user's memory or password manager. The password might be optional.

In order to recover the private key `pk`, the user provides the password `password` and retrieves user secrets `us` from secure locations. The function `g` is used to reverse the process and recover the private key `pk`.

## Implementations

ESCDS - https://en.wikipedia.org/wiki/Elliptic_Curve_Digital_Signature_Algorithm
Secp256k1
Schnorr - https://en.wikipedia.org/wiki/Schnorr_signature
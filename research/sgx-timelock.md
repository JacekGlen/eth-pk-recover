## Introduction

Intel Software Guard Extensions (SGX) is a set of security features provided by Intel processors to protect sensitive data and code from unauthorized access. SGX allows developers to create secure enclaves, which are isolated regions of memory that can be used to store and execute sensitive code and data.

SGX provides several key features to ensure the security of enclaves:

Memory Encryption: SGX encrypts the contents of the enclave's memory, preventing unauthorized access even if the physical memory is compromised.

Remote Attestation: SGX allows enclaves to prove their integrity to remote parties, ensuring that the code running inside the enclave has not been tampered with.

Sealing and Unsealing: SGX provides mechanisms to securely seal and unseal data, allowing enclaves to persistently store sensitive information while ensuring its confidentiality and integrity.

Secure Provisioning: SGX enables the secure provisioning of enclaves, ensuring that only trusted code and data are loaded into the enclave.

Overall, Intel SGX provides a hardware-based solution for protecting sensitive data and code, allowing developers to build secure applications that can resist attacks even on compromised systems.

## User Secret Management

The idea is to store the user's secret in the enclave. This can be done using Sealing/Unsealing mechanism. The user's secret is encrypted using a key derived from the enclave's measurement. The sealed data can only be unsealed by the same enclave, ensuring that the secret is only accessible to the enclave that created it.



https://en.wikipedia.org/wiki/Trusted_Computing

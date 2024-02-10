 
# Starfish Protocol
Distributed, multi-factor private key backup for the Ethereum ecosystem

## Features

- **Security**: The backup, and its parts called User Secrets, all have the same security grade as the private key itself. Access channels are of user's choice, and they are secured with the top industry standards.
- **Multi-factor recovery**: The backup parts (User Secrests) are each secured in an individual way using different mechanisms. The private key can be recovered if at least m out of n User Secrets are available. For example, the private key can be recovered if 2 out of 3 User Secrets are available.
- **Social recovery**: User Secrets can be entrusted to friends and family. The retrieval process is verified through channels provided by social networks, blockchain or other means.
- **Decentralization**: Much effort is put into securing User Secrets in a decentralized way, avoiding single points of failure. While individual secrets _might_ be stored in centralized locations, the recovery process is decentralized.
- **Expandability**: The protocol is designed to be flexible and modular. Additionally it can work with the exisitng solutions, such as web3auth, magic.link, account abstraction, etc.
- **Future-proof**: The protocol is designed to adapt to the future changes in the Ethereum ecosystem. Its modular design allows for easy integration with new technologies and standards, e.g. new User Secret locations, quantum-resistant cryptography, etc.
- **Wallet integration**: The protocol can be integrated into wallets for a seamless user experience. It can be used as a backup mechanism for the private keys, or for dynamic transaction signing.

## Motivation

The private keys give unlimited access to the Ethereum accounts. It is vital to keep them secure and protect them from either being lost or stolen. But these two requirements are often in conflict with each other. This creates a dilemma for users: the more secure the private key is, the less accessible it is and the higher the chance of losing access. On the other hand, increasing accessibility leads to decreased security. This is a tradeoff that users have to make when deciding how to store their private keys.

A lot of effort has been put into securing private keys. Mnemonics made it easier for the users to manage their private keys. The introduction of hardware wallets made it easier to store them securely. However, there are still many cases where private keys cannot be stored in hardware wallets. Account abstraction ([ERC-4337](https://eips.ethereum.org/EIPS/eip-4337)) can help to alleviate some of these issues. However, it has not been widely adopted yet. Even then, account abstraction only works in some scenarios.

## Methodology

The Starfish Protocol offers a solution to this dilemma. Users can store their private keys in a more secure, less accessible way. Then they can create a secure backup and use it to recover private keys when they need it. The distributed and multi-factor recovery mechanism ensures that the private key is not exposed to any single point of failure.

The creation of the private key backup is a two-step process.

Firstly, the system creates recovery data for the private key. This could be either a new, system-generated key or an existing, user-provided key. The recovery data is then split into multiple shares, known as User Secrets. A single User Secret is not enough to recover the private key. It does not even reduce the effort required to brute-force the private key. The recovery is only possible when all required User Secrets are available and recovery data is reconstructed. See [algorithm](research/algorithm.md) page for more details on cryptography and algorithms used in this step.

Secondly, the User Secrets are distributed to multiple locations. This step allows full flexibility, it is up to the users to decide which locations work best for them. Each location applies its own security mechanisms. This makes it harder for an attacker to steal the private key since they would have to compromise multiple locations in order to recover it. Our [workflow](research/workflow.md) document describes the workflow in more detail. It also explains the rationale behind the design decisions.

To recover the private key from the backup, the users must access all required secure locations to retrieve User Secrets. Once available, the User Secrets are used to reconstruct the recovery data. The recovery data is then used to reconstruct the private key. For additional protection from losing access to private keys, this approach also supports [m-out-of-n](research/m-out-of-n.md) recovery. This means that the private key can be recovered if at least m out of n User Secrets are available. For example, the private key can be recovered if 2 out of 3 User Secrets are available.

## User Secret Locations

User Secrets are key to recovering the private key. They are stored in multiple locations. Each location is secured with a different security mechanism. This makes it harder for an attacker to steal the private key since they would have to compromise multiple locations in order to recover it.

Currently, the following locations for User Secrets are supported, but more can be added in the future:
- Self-Custody: User Secret is saved in a file. This is the most naive approach, but it is also the most flexible one. It is up to the user to decide how to secure the file. For example, it can be encrypted with a password or stored on a USB drive.
- [Social](research/social.md): This utilises the power of social media and social networks. User Secrets are entrusted to friends and family. The retrieval process is verified through channels provided by social networks.
- [On-chain](research/on-chain.md): Storing User Secrets on the chain is in the spirit of the distributed and trustless nature of Ethereum. The user secret is protected by another ETH account.
- [Password Managers](research/password-manager.md): These services are popular and widely used. If a user already uses a password manager that they can trust, they can store their User Secrets there as well.
- [Key Valuts](research/key-vault.md): User secret is saved in a key vault.
- [OAuth2](research/oauth2.md): User secret is saved in an OAuth2 provider.
- [SGX](research/sgx-timelock.md): User secret is saved in an Intel SGX enclave.
- [Eth-pk-recovery Providers](research/centralized-provider.md): These services are hosted by third parties. They implement the methodology described in this repository. They provide a user interface to help navigate through the recovery process, but they can also be used as a convenient way to store User Secrets. However, they are centralized and trustful.

## Implementations

The following implementations are currently available:


## Notes

- User secrets are backups for a private key. Keyword: backup.
- You derive several independent user secrets from a private key. Each user secret should be placed in different locations, in terms of geography, services and providers. Keywords: decentralization, distribution.
- Having user secrets, a private key can be got back. The scheme is similar to multisig, for instance, it is enough to have 3 out of 5 user secrets. Keyword: multisig.
- On the other hand, the fact that an adversary knows some but an insufficient number of user secrets does not weaken a private key. Keyword: security.
- This can be applied to both newly created and existing private keys.
- Three steps: generate user secrets, distribute user secrets, and optionally recover a private key.


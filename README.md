# eth-pk-recover
Ethereum network private key recovery: methodology and implementations

## Motivation

The private key gives unlimited access to the Ethereum account. It is vital to keep them secure and protect them from either being lost or stolen. But these two requirements are often in conflict with each other. This creates a dilemma for users: the more secure the private key is, the less accessible it is and the higher the chance of losing the access. On the other hand, increasing accessibility leads to decreased security. This is a tradeoff that users have to make when deciding how to store their private keys.

A lot of effort has been put into securing private keys. The introduction of hardware wallets has made it easier to store them securely. However, there are still many cases where private keys cannot be stored in hardware wallets. Account abstraction ([ERC-4337](https://eips.ethereum.org/EIPS/eip-4337)) can help to alleviate some of these issues. However, it has not been widely adopted yet. Even then, account abstraction does not work in every scenario.

## Methodology

This repository offers a solution to this problem. Users can store their private keys in the most secure, least accessible way. Then they can enable private key recovery and use it to recover the private key when they need it. The unique multi-factor recovery mechanism ensures that the private key is not exposed to any single point of failure.

Firstly, users create private key recovery. For this, the private key is encoded and recovery data is generated. The recovery data is then split into multiple shares, known as User Secrets. Then, the User Secrets are stored in multiple locations. Each location is secured with a different security mechanism. This makes it harder for an attacker to steal the private key since they would have to compromise multiple locations in order to recover it. Our [research/workflow.md](research/workflow.md) document describes the workflow in more detail. It also explains the rationale behind the design decisions.

When the user needs to recover the private key, they need to access all required User Secrets. Once available, the User Secrets are combined to recreate the recovery data. The recovery data is then used to recover the private key. A single User Secret is not enough to recover the private key.

For additional protection from losing access to private keys, this approach also supports [m-out-of-n](research/m-out-of-n.md) recovery. This means that the private key can be recovered if at least m out of n user secrets are available. For example, the private key can be recovered if 2 out of 3 user secrets are available.

Please see [research/algorithm.md](research/algorithm.md) for more details on the algorithm.

## User secrets

User secrets are key to recovering the private key. They are stored in multiple locations. Each location is secured with a different security mechanism. This makes it harder for an attacker to steal the private key since they would have to compromise multiple locations in order to recover it.

Currently, the following user secrets are supported, but more can be added in the future:
- Self-Custody: User secret is saved in a file. It is the user's responsibility to keep the file secure.
- Password Manager: User secret is saved in a password manager. See [research/password-manager.md](research/password-manager.md).
- On-chain: User secret is saved on the Ethereum chain and protected by another ETH account. See [research/on-chain.md](research/on-chain.md).
- Key Valut: User secret is saved in a key vault. See [research/key-vault.md](research/key-vault.md).
- OAuth2: User secret is saved in an OAuth2 provider. See [research/oauth2.md](research/oauth2.md).
- Social: User secret is saved in a social network. See [research/social.md](research/social.md).
- SGX: User secret is saved in an Intel SGX enclave. See [research/sgx-timelock.md](research/sgx-timelock.md).
- Centralized Provider: User secret is saved in a centralized provider. See [research/centralized-provider.md](research/centralized-provider.md).


## Implementations

The following implementations are currently available:


## Notes

- User secrets are backups for a private key. Keyword: backup.
- You derive several independent user secrets from a private key. Each user secret should be placed in different locations, in terms of geography, services and providers. Keywords: decentralization, distribution.
- Having user secrets, a private key can be got back. The scheme is similar to multisig, for instance, it is enough to have 3 out of 5 user secrets. Keyword: multisig.
- On the other hand, the fact that an adversary knows some but an insufficient number of user secrets does not weaken a private key. Keyword: security.
- This can be applied to both newly created and existing private keys.
- Three steps: generate user secrets, distribute user secrets, and optionally recover a private key.

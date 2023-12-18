# eth-pk-recover
Ethereum network private key recovery: methodology and implementations

## Motivation

Private key give an unlimited access to the Ethereum account. It is vital to keep them secure and protect from either being lost or stolen. But these two requirements are often in conflict with each other. 

So users are faced with a dillema: the more secured the private key is, the less accessible it is. The less secured the private key is, the more accessible it is. This is a tradeoff that users have to make when deciding how to store their private keys. 

A lot of effort has been put into securing private keys. The introduction of hardware wallets has made it easier to store them securely. However, there are still many cases where private keys cannot be stored in hardware wallets. Account abstraction has been proposed to alleviate some of theses issues. However it has not been widely adopted yet. Even then, account abstraction does not meet every scenario. 

This leads to another problem: how to make sure that legitimate actor can recover their private keys in case of loss? 

## Methodology

See [research/workflow.md](research/workflow.md) and [research/algorithm.md](research/algorith.md) for more details.

## User secrets

User secrets are key to recovering the private key. They are stored in multiple locations. Each location is secured with a different security mechanism. This makes it harder for an attacker to steal the private key, since they would have to compromise multiple locations in order to recover it. 

Currently, the following user secrets are supported, but more can be added in the future:
- Self Custody: User secret is saved in a file. It is the user's responsibility to keep the file secure.
- Password Manager: User secret is saved in a password manager. See [research/password-manager.md](research/password-manager.md).
- On-chain: User secret is saved on Ethereum chain and protected by another eth account. See [research/on-chain.md](research/on-chain.md).
- Key Valut: User secret is saved in a key vault. See [research/key-vault.md](research/key-vault.md).
- OAuth2: User secret is saved in an OAuth2 provider. See [research/oauth2.md](research/oauth2.md).
- Social: User secret is saved in a social network. See [research/social.md](research/social.md).
- SGX: User secret is saved in an Intel SGX enclave. See [research/sgx-timelock.md](research/sgx-timelock.md).
- Centralized Provider: User secret is saved in a centralized provider. See [research/centralized-provider.md](research/centralized-provider.md).


## Implementations

The following implementations are available:
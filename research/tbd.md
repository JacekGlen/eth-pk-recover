Different scenarios to consider:

## Invalidate User Secret
The private key is split into `n` User Secrets and stored in secure locations. The location `x` becomes compromised and the User Secret stored in location `x` is invalidated. How can we replace the invalidated User Secret without affecting the other User Secrets?
How to guarantee that revoked User Secret cannot be used? List of revoked User Secrets? Private verification token?

## Sub-key (Account Abstraction style)
The private key is backed up by `n` User Secrets. The user creates a sub-key and a 'token'. The sub-key plus the token can be used to sign transactions as if it were the private key. 
When the sub-key is compromised, the user can revoke the token and create a new pair of sub-key and token. The original private key and its backup (User Secrets) are not affected.
What is the best way to implement this? Token private or public? How to revoke the token?

## Dynamic signing
The wallet keeps one User Secret. When signing the transaction it prompts the user to access other `m-1` secrets. The user can choose which secrets to use for the signing. The wallet recovers the private key and signs the transaction. The private key is not exposed to the wallet. The wallet does not store the private key. The wallet does not store the User Secrets.
How to implement this? How to recover the private key without exposing it to the wallet? 

## Soft Authenitication 
For low trust actions, e.g. confirming wallet address, not all `m` secrets are required. Insted we can use `k out of m` secrets, where `k <= m`.
Are there any real use cases for this? 

## On-chain User Secret 1
The User Secret is stored on-chain using another, friendly account. The User Secret is encrypted with the public key of the user. The User Secret can be decrypted with the private key of the user.
Create a smart contract to store  User Secrets? The same secret can be stored in multiple contracts?

## On-chain User Secret 2
ZK-proof is stored on-chain. The ZK-proof is verified by the smart contract. The proof can be used to recover the User Secret with the owning account's private key.

## List of User Secrets
We can create a token that encapsulates the list of User Secrets. This might include locations and identities, e.g. 'My friend Tom on Facebook' or 'alice@example.com on Google Drive'. 
Can it be public? What are security risks? Can it be used for invalidating User Secrets? 

## Offline page
To crate the backup or recover the private key, the user downloads a signle html page, which guides the user through the process. The page has adapters for all known User Secret storage locations. It also has cryptography functions to create the backup and recover the private key. The page does not store any data or private keys, but can reveal the private key to the user when conditions are met.
How to make sure the page is not tampered with? How to make sure the page is not used for phishing?

## Browser plugin
The browser plugin can be used to create the backup or recover the private key. The plugin has adapters for all known User Secret storage locations. It also has cryptography functions to create the backup and recover the private key. The plugin does not store any data or private keys, but can reveal the private key to the user when conditions are met.
Also consider implementing Snap extension for MetaMask. Vendor lock-in risk?

## Brain User Secret
The User Secret is stored as an anwer to a security question. Security questions suck individually, but if you combine eg. 20 of them you can get quite a lot of entropy.
Creating a User Secret from a security question is very sensitive to typos, case sensitivity, etc. How to make sure the user can recover the User Secret? How to make sure the User Secret is not easily guessable?

## Avoid sychronous channel
In the situation when the recovery depends on an action from a third party, e.g. friend's approval or decryption of on-chain data, we should avoid sychronous channels.
What are other secure channels to deliver User Secrets?

## Verifiable User Secret
Implement "A Simple Publicly Verifiable Secret Sharing Scheme and its Application to Electronic Voting" by Berry Schoenmakers into the User Secret management.

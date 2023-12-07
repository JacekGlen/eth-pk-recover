# eth-pk-recover
Ethereum network private key recovery: methodology and implementations

## Introduction

This repository describes a methodology for recovering Ethereum private keys from various sources. The goal is to provide a comprehensive overview of the different methods that can be used to recover private keys from various sources.

The methodology is based on the following principles:
- **Extensible**: The methodology should be extensible, meaning that it should be possible to add new methods for recovering private keys from different sources.
- **Modular**: The methodology should be modular, meaning that it should be possible to combine different methods for recovering private keys from different sources.

The methodology is supplemented with specific implementations.

## Motivation

Private key give an unlimited access to the Ethereum account. If a private key is lost or stolen, the account can be compromised. This can lead to loss of funds or other assets stored in the account.

A lot of effort has been put into securing private keys. The introduction of hardware wallets has made it easier to store them securely. However, there are still many cases where private keys cannot be stored in hardware wallets. Account abstraction has been proposed as a solution to this problem. However it has not been widely adopted yet. Even then, account abstraction does not meet every scenario. 

So users are faced with a dillema: the more secured the private key is, the less accessible it is. The less secured the private key is, the more accessible it is. This is a tradeoff that users have to make when deciding how to store their private keys. So many users choose to store their private keys in a way that is easily accessible, but not very secure. This makes it easier for attackers to steal private keys and compromise accounts.

Also too tight security can be a problem. If a user loses access to their private key, they will not be able to recover their account.

This leads to another problem: how to make sure that legitimate actor can recover their private keys in case of loss? 

## Methodology

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



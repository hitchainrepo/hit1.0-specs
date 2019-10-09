# Project Information File Specification

## Table of contents
<!-- TOC -->
- [Project Information File Specification](#project-information-file-specification)
  * [Table of contents](#table-of-contents)
  * [Description](#description)
  * [Signature](#signature)
  * [Version](#version)
  * [Entrance Url](#entrance-url)
    + [Ethereum Entrance](#ethereum-entrance)
    + [File Server Entrance](#file-server-entrance)
  * [Owner](#owner)
  * [Repository](#repository)
    + [Basic Information](#basic-information)
    + [Repository Encrypt](#repository-encrypt)
  * [Member](#member)
<!-- /TOC -->

## Description

The Project Information File is the primary description of the basic information for the Hit repository, including signatures, versions, portal addresses, warehouse information, owner and member information.

Sample file structure:

    3d6cb4d3882def540b92c93ec3e4b8b94abb5250ec0c268dadb033a731a11a7e0e647288b2cc8c4517a6f6b0b161f24087a202dbd06a56e8619b9148b7e55f24b66bf80ae58b687608bc0cc27f5a0b778a838288e6ebb44dd3e74687d3ae96feaff7e7b4a2f0701f3bf11326e5456fe170aa3ffc4b4f01ab43b828e5cf03198b
    {
      "version": "1",
      "ethereumUrl": "https://121.40.127.45:1443",
      "fileServerUrl": "121.40.127.45",
      "repoName": "spring-boot-seckill-20190829161143",
      "RepoPriKey": "1edb7644ab4746ab5c988c641fc2a1800f2e46e1a35433ba0f09999c7c80b78ea447831412c93e4a255c6abf3edeec6942a3642a494c052717ad3fb6921ff5b5169e92ad67fb830a42a65c49f7dda3e4d41dd42001f8f078657ca43c8b1b6665507ca372755649b86bb407e3ba96511ded6bb105e3604211ca075962a34ca605",
      "repoPubKey": "044040a31b0552d46a924b7e4db48adc77d2a5e2d2b38505822e698ab8ff7bc1f958613bac303cbce20867be64cddd70b7724c096524b4e4ed53c7681f58860932",
      "repoAddress": "0x48e154cb7040602163236df58a8cc3c0836425e1-6",
      "owner": "0x2bc8307ecc99ed184bae05a0b6b4371d406bf490",
      "OwnerPubKeyRsa": "30819f300d06092a864886f70d010101050003818d0030818902818100b63fe96447d3b2d5c77b01ad284ad94a96f28ae9d524f67b242abac2808d3134ee22811f448af97975100f881174905a48fe10ee5687bb40af86a6d44eb2ca819d70c3d96eec492e95e5c5af53f19150bb82e0b89283c8f24465c2bef3178b1d04365b20dc6827cb4217af1f694c97a95418b4eb9965e29658184dcd98d928330203010001",
      "ownerAddressEcc": "0x2bc8307ecc99ed184bae05a0b6b4371d406bf490",
      "members": [
        {
          "member": "0x9e98b74fc70d02b8fad98eb33315507e6e4e7f9c",
          "MemberPubKeyRsa": "30819f300d06092a864886f70d010101050003818d0030818902818100f2c3777657fc45b2dc309721e6653454c8fe576758e513aeae269797dfcb40567b1e36d8967640de78accf64aff4e39d2f25f2d75d71d803278a1c9733cacb6394210123c26a279c64bba07de9dd18e5103eb9d89920599be4804130b3f279aecaeb7e0094dd1200f489985c3394607c0c6571a0abac2dc787035e8f2266c5310203010001",
          "memberAddressEcc": "0x9e98b74fc70d02b8fad98eb33315507e6e4e7f9c",
          "MemberRepoPriKey": "550603bde73e656ec2ad8e3b26575fafd64c146dab83c1c5dcef7532db775af83422622d926bf8bb9084b987ce55de36c7b6be1a85f558734102f205c767e8a32383f7aaee70011ea45d9833ef55df54a51960f1e7d5be8a54a08fd15652004042ffa5defba30012853b649f9c2f1c458d5441da535adf605561cd4d0ca4d9c3"
        }
      ]
    }

## Signature

The first line of the file content is the signature information, which is the signature of the content below the first line, which is used to verify that the file is not modified by other people (non-owners):
* Signature method: MD5withRSA, sign(content, ownerRsaPrivateKey)
* Verification signature: MD5withRSA, verify(content, signature, ownerRsaPublicKey)

## Version

The version information specifies the version of the current specification.
* version: version information

## Entrance Url
### Ethereum Entrance

Ethereum entrance address.
* ethereumUrl: Ethereum Service Address

**Notice**: This portal address configuration is no longer used and will be removed in a future release.

### File Server Entrance

The file service entry address, currently using IPFS as the file store, is the IPFS file service address entry.
* fileServerUrl: IPFS service address

## Owner

Warehouse owner (creator) information, including:
* owner: owner's account, Ethereum account address
* ownerPubKeyRsa: owner's RSA public key for signature and warehouse encryption
* ownerAddressEcc: owner's Ethereum account address

## Repository
### Basic Information

The warehouse basic information includes:
* repoName: the name of the warehouse
* repoAddress: the warehouse address, the warehouse address format is: contractAddress-id

### Repository Encrypt

Warehouse encryption information includes:
* repoPriKey: The RSA key pair is randomly generated when the repository is encrypted. The private key of the repository is encrypted with the owner's public key (ownerPubKeyRsa), and the private key of the repository is used for decryption of the repository.
* repoPubKey: the public key of the repository is used to encrypt the repository

## Member

The warehouse member information members is an array, and the member information includes:
* member: member's account, Ethereum account address
* memberPubKeyRsa: member's RSA public key for warehouse private key encryption
* memberAddressEcc: member's Ethereum account address
* memberRepoPriKey: Warehouse private key encryption, the encryption process is:
    - 1) Owner uses the private key to decrypt the private key (repoPriKey) encrypted by the warehouse to obtain the original private key;
    - 2) Encrypt the original private key using the member's public key (memberRepoPriKey);
    - 3) The member obtains the original warehouse key and decrypts the file by decrypting its own private key (memberRepoPriKey);
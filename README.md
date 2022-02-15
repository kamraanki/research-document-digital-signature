# Research documents digital signature verification PoC 
## Problem Statement
```sh
XYZ Ltd. is an asset management company that has a research department, that has a blockchain-based platform where they have hosted critical research documents.
Many research-based vendors/organizations are consumers of this platform. These vendors/organizations have their decentralized digital identities and can log in to the
platform using their digital wallets. They contribute to these documents for research purposes, the authored content is referred by other platform partners to form respective
views. Thus to make the platform more trustful and transparent, XYZ Ltd. wants to provide a feature to allow the user to digitally sign the authored content. Please, design
and implement a smart contract that allows a Researcher/vendor/organization to digitally sign their respective authored content and other researchers/organizations that are
partners to this DLT enabled platform to be able to verify the signature to check the authenticity.
```
## Approach
- As research documents can be larges in size Kb's or Mb's too. So, it is not recommended to put this much large data over Blockchain.
- So, to solve this problem we will keep research documents on middleware and hash on the blockahin.

## Implementation
- We have two functionalities i.e. Upload research document and Download research document.
- Implementation of "Upload research document functionality" is as following:-
    > Select a research document file (*.pdf) and it's checksum will be calculated automatically.
    > Next we need to sign the checksum ny clicking "Sihn checksum" button and document will be signed with the help of Metamask.
    > After this we need to submit this document. Document will be uploaded to middleware server and checksum will be verified.
    > After successful verification of checksum from middleware, we will create a transaction and will store checksum on chain. (We will also send digital signature on chain for verification)
    > In smart contract author digital signature will be verified, once verified checksum will be stored in Blockchain.
- Implementation of "Download research document functionality" is as following:-
    > Input a valid document id and click on "Download" button.
    > Document checksum will be fetched from Blockchain and it will be verified with the document's checksum. Once verified, document will be downloaded.

## Deployment details
- Smart contract deployment on Ropsten test network is as following:-
    ```sh
    Contract Address:- 0xb7cd0dBFb31C664EFd78aDf2Ac8b01D649905026 
    ```
    ```sh
    Abi:- [{"inputs":[{"internalType":"string","name":"","type":"string"}],"name":"documents","outputs":[{"internalType":"bytes32","name":"","type":"bytes32"}],"stateMutability":"view","type":"function"},{"inputs":[{"internalType":"string","name":"documentId","type":"string"}],"name":"getDocumentChecksum","outputs":[{"internalType":"bytes32","name":"","type":"bytes32"}],"stateMutability":"view","type":"function"},{"inputs":[{"internalType":"string","name":"documentId","type":"string"},{"internalType":"bytes32","name":"_hashedMessage","type":"bytes32"},{"internalType":"uint8","name":"_v","type":"uint8"},{"internalType":"bytes32","name":"_r","type":"bytes32"},{"internalType":"bytes32","name":"_s","type":"bytes32"}],"name":"registerDocumentChecksum","outputs":[],"stateMutability":"nonpayable","type":"function"}] 
    ```
- Middleware is also deployed. Go through demo from following link:-
    ```sh
    Demo Link:- <http://13.233.223.152:8080/> 
    ```

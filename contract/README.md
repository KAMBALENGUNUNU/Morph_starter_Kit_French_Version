## Foundry

**Foundry est une boîte à outils ultra-rapide, portable et modulaire pour le développement d'applications Ethereum, écrite en Rust.**

Foundry se compose de :

-   **Forge**: Framework de test pour Ethereum (comme Truffle, Hardhat et DappTools).
-   **Cast**: Couteau suisse pour interagir avec les contrats intelligents EVM, envoyer des transactions et récupérer des données de la chaîne.
-   **Anvil**: Nœud Ethereum local, similaire à Ganache, Hardhat Network.
-   **Chisel**: Un REPL Solidity rapide, utilitaire et verbeux.

## Documentation

https://book.getfoundry.sh/

## Utilisation

### Construction

```shell
$ forge build
```
# Compile les contrats intelligents avec Forge

### Test

```shell
$ forge test
```
# Lance les tests pour les contrats intelligents


### Formatage

```shell
$ forge fmt
```
# Formate le code Solidity selon les conventions


### Captures de gaz

```shell
$ forge snapshot
```
# Prend des snapshots des coûts en gaz des transactions



### Anvil

```shell
$ anvil
```
# Lance un nœud Ethereum local pour les tests



### Déploiement

```shell
$ forge script script/Counter.s.sol:CounterScript --rpc-url <your_rpc_url> --private-key <your_private_key>
```
# Déploie un contrat intelligent en utilisant un script Forge



### Cast

```shell
$ cast <subcommand>
```
# Utilise Cast pour interagir avec les contrats et la blockchain



### Aide

```shell
$ forge --help
$ anvil --help
$ cast --help
```
# Affiche l'aide pour chaque outil



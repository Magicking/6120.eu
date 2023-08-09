+++
title = "Note technique du paypal coin"
date = "2023-08-07T21:50:00+01:00"
showCover = false
tags = ["stable", "erc20", "ethereum"]
keywords = ["stable", "erc20", "ethereum"]
description = ""
showFullContent = false
readingTime = true
hideComments = false
color = "" #color from the theme settings
+++

# Introduction

Après être tombé sur la news https://newsroom.paypal-corp.com/2023-08-07-PayPal-Launches-U-S-Dollar-Stablecoin qui annonce la sortie d'un jeton ERC20 par PayPal et Paxos ainsi qu'après une recherche sur Twitter on tombe sur quelques informations techniques intéressantes.

C'est un jeton de type ERC20 qui peut-être mis en pause, dont la destruction (Burn) et la création (Mint) de sa quantité est régi par une entitée centralisée.

# Composition du jeton

Le [proxy](https://ethereum.org/en/developers/docs/smart-contracts/upgrading/) du jeton avec lequel les utilisateurs vont interragir est [0x6c3ea9036406852006290770BEdFcAbA0e23A0e8](https://etherscan.io/token/0x6c3ea9036406852006290770bedfcaba0e23a0e8), en oscultant un peu plus le smart-contract, on s'aperçoit qu'il y'a eu plusieurs implémentation du jeton au cours du passé

![](/img/posts/pyusd/1.png)

et que l'ensemble des smart-contracts existent depuis environ 1 an, probablement une phase test avant l'annonce du 2023-08-07 étant donné un volume important de transaction précédant celle-ci.

TODO SCREENSHOT OF PROXY DEPLOYMENT

L'implémentation actuel du jeton étant [0xe17b8adf8e46b15f3f9ab4bb9e3b6e31db09126e](https://etherscan.io/address/0xe17b8adf8e46b15f3f9ab4bb9e3b6e31db09126e) la différence majeure avec le code source de l'implémentation précédente était le masquage des termes PayPal/PYUSD par Hopper USD/XYZ.

C'est cette dernière que nous allons étudier, le proxy ne servant qu'à stocker l'état du smart-contract en lieu et place de l'implémentation.

# Analyse technique

En préambule, on observe que le contrat utilise une très ancienne version du langage Solidity ``0.4.24`` en spécifiant la nécéssité des fonctions expérimentales de la version ``0.5``.

Le smart-contract est plutôt généreux en commentaire notamment avec une annotation [NatSpec]() orienté développeur et plusieurs lignes au sein de chaque fonction.

## Fonctions

Les fonctionnalités présentes dans le smart-contract peuvent être regroupées en 6 familles différentes détaillé ci-dessous.

### Proxy
#### constructor

Fonction executée lors du déploiement de l'implémentation du smart-contract, ici l'implémentation est initializé puis mis en pause pour éviter toute erreur.

#### initialize

Fonction initialisant l'état du smart-contract tout en prévenant une ré-initialisation lors d'une mise à jour, appelle notamment une autre fonction privée `initializeDomainSeparator` en charge de définir le prefix de délégation (le smart-contract et son nom).

### ERC20

Les fonctions ci-desous ne sont pas utilisables si l'émetteur ou le récepteur des fonds ont été gelé.

#### allowance

Accesseur sur la limite de dépense d'un compte Ethereum pour un autre compte.

#### approve

Définie la limite de dépense d'un compte Ethereum pour un autre compte.

#### decreaseApproval

Décroie la limite de dépense d'un compte Ethereum pour un autre compte.

#### increaseApproval

Accroie la limite de dépense d'un compte Ethereum pour un autre compte.

#### balanceOf

Retourne la quantité de jeton pour un compte Ethereum.

#### totalSupply

Retourne la quantité total de jeton.

#### transfer

Transfère la quantité de jeton d'un compte Ethereum vers un autre compte.

#### transferFrom

Transfère la quantité de jeton d'un compte Ethereum vers un autre compte au travers par le biais d'un tiers compte autorisé.

### Owner Admin

Toutes les fonctions ci-dessous sont accessibles uniquement par le possesseur du smart-contract.

#### proposeOwner

Définie le potentiel nouveau compte possesseur du smart-contract.

#### disregardProposeOwner

Annule le potentiel nouveau compte possesseur du smart-contract

#### claimOwnership

Promeut le potentiel compte possesseur en nouveau possesseur.

#### reclaimPYUSD

Transfère les jetons affectés au contrat au possesseur.

#### pause

Mets en pause 
#### unpause

### Asset protection owner
    setAssetProtectionRole
     - Définie le gestionnaire de protection des biens
    freeze
     - Gèle une addresse
    unfreeze
     - Dégèle une addresse
    wipeFrozenAddress
     - Détruit les fonds d'une addresse gelée
    isFrozen
     - Accesseur des addresses gelées

### Gestion de la quantité
    setSupplyController
     - Définie le gestionnaire de quantité
    increaseSupply
     - Créé et transfère des jetons au gestionnaire de quantité
    decreaseSupply
     - Détruit des jetons du gestionnaire de quantité.

### Gestion de la délégation
    nextSeqOf
     - Accesseur du nonce (nombre )
    betaDelegatedTransfer
     - Transfère des fonds au travers d'un tiers
     - Le tiers n'est pas enforce par le protocole
     - Il est possible de faire des transfères de 0 du moment que l'on paie des fees, cela semble être un
    betaDelegatedTransferBatch
     - Trans
    isWhitelistedBetaDelegate
    setBetaDelegateWhitelister
    whitelistBetaDelegate
    unwhitelistBetaDelegate

## Notes

 - Utilisation d'accesseur qui sont déjà rajouté par défaut
 - Fonction qui retourne toujours les mêmes constantes (vrai)

# Conclusion
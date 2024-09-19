# Forge Standard Library • [![CI status](https://github.com/foundry-rs/forge-std/actions/workflows/ci.yml/badge.svg)](https://github.com/foundry-rs/forge-std/actions/workflows/ci.yml)

Forge Standard Library est une collection de contrats et bibliothèques utiles pour être utilisés avec [Forge and Foundry](https://github.com/foundry-rs/foundry).Elle tire parti des cheatcodes de Forge pour rendre l'écriture des tests plus simple et plus rapide, tout en améliorant l'expérience utilisateur des cheatcodes.

**Apprenez à utiliser Forge-Std avec le  [📖 Livre Foundry (Guide Forge-Std))](https://book.getfoundry.sh/forge/forge-std.html).**

## Installation

```bash
forge install foundry-rs/forge-std
```

## Contrats
### stdError

Ceci est un contrat utilitaire pour les erreurs et les revert. Dans Forge, ce contrat est particulièrement utile pour le cheatcode `expectRevert`, car il fournit toutes les erreurs intégrées au compilateur.

Consultez le contrat lui-même pour obtenir tous les codes d'erreur.

#### Exemple d'utilisation

```solidity

import "forge-std/Test.sol";

contract TestContract is Test {
    ErrorsTest test;

    function setUp() public {
        test = new ErrorsTest();
    }

    function testExpectArithmetic() public {
        vm.expectRevert(stdError.arithmeticError);
        test.arithmeticError(10);
    }
}

contract ErrorsTest {
    function arithmeticError(uint256 a) public {
        uint256 a = a - 100;
    }
}
```

### stdStorage

C'est un contrat assez volumineux en raison de la surcharge nécessaire pour rendre l'expérience utilisateur agréable. Principalement, il s'agit d'un wrapper autour des cheatcodes `record` et `accesses`. Il peut *toujours* trouver et écrire dans les slot(s) de stockage associés à une variable particulière sans connaître la disposition du stockage. La seule _grosse_ mise en garde est que, bien qu'un slot puisse être trouvé pour des variables de stockage packées, nous ne pouvons pas écrire en toute sécurité dans cette variable. Si un utilisateur tente d'écrire dans un slot packé, l'exécution renvoie une erreur, sauf s'il est non initialisé (`bytes32(0)`).

Cela fonctionne en enregistrant tous les `SLOAD` et `SSTORE` pendant un appel de fonction. S'il y a un seul slot lu ou écrit, il renvoie immédiatement le slot. Sinon, en coulisses, nous itérons et vérifions chacun d'eux (à condition que l'utilisateur ait passé un paramètre `depth`). Si la variable est une struct, vous pouvez passer un paramètre `depth` qui correspond essentiellement à la profondeur du champ.

I.e.:
```solidity
struct T {
    // depth 0
    uint256 a;
    // depth 1
    uint256 b;
}
```

#### Exemple d'utilisation:

```solidity
import "forge-std/Test.sol";

contract TestContract is Test {
    using stdStorage for StdStorage;

    Storage test;

    function setUp() public {
        test = new Storage();
    }

    function testFindExists() public {
        // Disons que nous voulons trouver le slot pour la variable publique `exists`. 
        // Il suffit de passer le sélecteur de fonction à la commande `find`.
        uint256 slot = stdstore.target(address(test)).sig("exists()").find();
        assertEq(slot, 0);
    }

    function testWriteExists() public {
        // Disons que nous voulons écrire dans le slot pour la variable publique `exists`.
        // Il suffit de passer le sélecteur de fonction à la commande `checked_write`.
        stdstore.target(address(test)).sig("exists()").checked_write(100);
        assertEq(test.exists(), 100);
    }

    // Il prend en charge des dispositions de stockage arbitraires, comme les emplacements de stockage basés sur assembly
    function testFindHidden() public {
        // `hidden` est un hachage aléatoire de bytes, l'itération à travers les slots ne le trouverait pas. 
        // Notre mécanisme le trouve.
        // Vous pouvez également utiliser le sélecteur au lieu d'une chaîne de caractères.
        uint256 slot = stdstore.target(address(test)).sig(test.hidden.selector).find();
        assertEq(slot, uint256(keccak256("my.random.var")));
    }

    // Si vous ciblez un mapping, vous devez passer les clés nécessaires pour effectuer la recherche
    // i.e.:
    function testFindMapping() public {
        uint256 slot = stdstore
            .target(address(test))
            .sig(test.map_addr.selector)
            .with_key(address(this))
            .find();
        // dans le constructeur de `Storage`, nous avons écrit que la valeur de cette adresse était 1 dans la map
        // donc lorsque nous chargeons le slot, nous nous attendons à ce qu'il soit à 1
        assertEq(uint(vm.load(address(test), bytes32(slot))), 1);
    }

    // Si la cible est une struct, vous pouvez spécifier la profondeur du champ :
    function testFindStruct() public {
        // REMARQUE : voir le paramètre de profondeur - 0 signifie le 0ème champ, 1 signifie le 1er champ, etc.
        uint256 slot_for_a_field = stdstore
            .target(address(test))
            .sig(test.basicStruct.selector)
            .depth(0)
            .find();

        uint256 slot_for_b_field = stdstore
            .target(address(test))
            .sig(test.basicStruct.selector)
            .depth(1)
            .find();

        assertEq(uint(vm.load(address(test), bytes32(slot_for_a_field))), 1);
        assertEq(uint(vm.load(address(test), bytes32(slot_for_b_field))), 2);
    }
}

// Un contrat de stockage complexe
contract Storage {
    struct UnpackedStruct {
        uint256 a;
        uint256 b;
    }

    constructor() {
        map_addr[msg.sender] = 1;
    }

    uint256 public exists = 1;
    mapping(address => uint256) public map_addr;
    // mapping(address => Packed) public map_packed;
    mapping(address => UnpackedStruct) public map_struct;
    mapping(address => mapping(address => uint256)) public deep_map;
    mapping(address => mapping(address => UnpackedStruct)) public deep_map_struct;
    UnpackedStruct public basicStruct = UnpackedStruct({
        a: 1,
        b: 2
    });

    function hidden() public view returns (bytes32 t) {
        // un slot de stockage extrêmement caché
        bytes32 slot = keccak256("my.random.var");
        assembly {
            t := sload(slot)
        }
    }
}

```

### stdCheats

Il s'agit d'un wrapper autour de cheatcodes divers qui nécessitent des wrappers pour être plus conviviaux pour les développeurs. Actuellement, il n'y a que des fonctions liées à  `prank`.En général, les utilisateurs peuvent s'attendre à ce que de l'ETH soit ajouté à une adresse lors de l'utilisation de `prank`,  mais ce n'est pas le cas pour des raisons de sécurité. La fonction `hoax` doit uniquement être utilisée pour une adresse avec un solde attendu, car elle sera écrasée. Si une adresse possède déjà de l'ETH, il suffit d'utiliser `prank`.  Si vous souhaitez modifier explicitement ce solde, utilisez simplement `deal`. Si vous voulez faire les deux, `hoax` est également adapté.


#### Exemple d'utilisation:

```solidity

// SPDX-License-Identifier: MIT
pragma solidity ^0.8.0;

import "forge-std/Test.sol";

// Hérite de stdCheats
contract StdCheatsTest is Test {
    Bar test;
    function setUp() public {
        test = new Bar();
    }

    function testHoax() public {
        // nous appelons `hoax`, qui donne à l'adresse cible de l'eth
        // puis appelle `prank`
        hoax(address(1337));
        test.bar{value: 100}(address(1337));

        // surchargé pour vous permettre de spécifier combien d'eth
        // initialiser sur l'adresse
        hoax(address(1337), 1);
        test.bar{value: 1}(address(1337));
    }

    function testStartHoax() public {
        // nous appelons `startHoax`, qui donne à l'adresse cible de l'eth
        // puis appelle `startPrank`
        //
        // il est également surchargé pour que vous puissiez spécifier un montant d'eth
        startHoax(address(1337));
        test.bar{value: 100}(address(1337));
        test.bar{value: 100}(address(1337));
        vm.stopPrank();
        test.bar(address(this));
    }
}

contract Bar {
    function bar(address expectedSender) public payable {
        require(msg.sender == expectedSender, "!prank");
    }
}
```

### Std Assertions

Contient diverses assertions.

### `console.log`

L'utilisation suit le même format que [Hardhat](https://hardhat.org/hardhat-network/reference/#console-log).
Il est recommandé d'utiliser `console2.sol` comme montré ci-dessous, car cela affichera les logs décodés dans les traces Forge.

```solidity
// l'importer indirectement via Test.sol
import "forge-std/Test.sol";
// ou l'importer directement
import "forge-std/console2.sol";
...
console2.log(someValue);
```

Si vous avez besoin de compatibilité avec Hardhat, vous devez utiliser `console.sol`  standard à la place. En raison d'un bug dans `console.sol`,  les logs qui utilisent les types `uint256` ou `int256` ne seront pas correctement décodés dans les traces Forge.

```solidity
// l'importer indirectement via Test.sol
import "forge-std/Test.sol";
// ou l'importer directement
import "forge-std/console.sol";
...
console.log(someValue);
```

## License

Forge Standard Library est proposé sous licence [MIT](LICENSE-MIT) or [Apache 2.0](LICENSE-APACHE) license.

<!-- TITRE -->
<p align="center"> 
  <img width="200px" src="https://morphl2brand.notion.site/image/https%3A%2F%2Fprod-files-secure.s3.us-west-2.amazonaws.com%2Ffcab2c10-8da9-4414-aa63-4998ddf62e78%2F76b87f21-9863-4533-932c-91c593cc741c%2FLogo_Morph_white.jpg?table=block&id=00854626-61f3-4668-8ab1-cb8f3ec0dcb0&spaceId=fcab2c10-8da9-4414-aa63-4998ddf62e78&width=2000&userId=&cache=v2" align="center" alt="Morph" />
 <h2 align="center">Morph Starter Kit</h2>
</p>

<!-- TABLE DES MATIÈRES -->

<details>
  <summary>Table des Matières</summary>
  <ol>
    <li>
      <a href="#à-propos-du-projet">À Propos Du Projet</a>
      <ul>
        <li><a href="#construit-avec">Construit Avec</a></li>
      </ul>
    </li>
    <li>
      <ul>
        <li><a href="#prérequis">Prérequis</a></li>
        <li><a href="#installation">Installation</a></li>
      </ul>
    </li>
    <li><a href="#utilisation">Utilisation</a></li>
    <li><a href="#feuille-de-route">Feuille de Route</a></li>
    <li><a href="#contribution">Contribution</a></li>
    <li><a href="#licence">Licence</a></li>
    <li><a href="#contact">Contact</a></li>
    <li><a href="#remerciements">Remerciements</a></li>
  </ol>
</details>

<!-- À PROPOS DU PROJET -->


## À Propos Du Projet

Le kit de démarrage Morph aide les développeurs à créer rapidement et efficacement des dApps sur la blockchain Morph. Il s'agit d'un modèle complet pour créer des dApps fullstack. Ce kit est une extension du [kit ReactToWeb3](https://github.com/Protocol-Explorer/ReactToWeb3)

<p align="right">(<a href="#top">retour en haut</a>)</p>


## Construit Avec

Le kit de démarrage Morph est construit avec une variété de frameworks et bibliothèques.

- [Morph](https://www.morphl2.io/)
- [Solidity](https://docs.soliditylang.org/en/v0.8.19/)
- [Next.js](https://nextjs.org/)
- [Foundry](https://book.getfoundry.sh/)
- [walletConnect](https://cloud.walletconnect.com/sign-in)
- [wagmi](https://wagmi.sh/react/getting-started)
- [shadcn](https://ui.shadcn.com/docs/installation/next)

<p align="right">(<a href="#top">retour en haut</a>)</p>

<!-- DÉMARRAGE -->

## Prérequis

- Node
- Git
- Foundry

```bash
cd contract
yarn

```


### Configuration de l'Environnement

#### Contrat

Dans votre terminal, exécutez

```bash
cd contract
yarn
```

#### Frontend

Avant de commencer, vous devez configurer vos variables d'environnement. Créez un fichier `.env.local`dans le répertoire racine en exécutant dans un nouveau terminal :

```bash
cp .env.example .env.local
```

Dans le fichier, mettez à jour la variable `NEXT_PUBLIC_PROJECT_ID` variable avec votre identifiant de projet WalletConnect. Vous pouvez en obtenir un en enregistrant votre projet sur [WalletConnect Cloud](https://cloud.walletconnect.com/).

### Installer les Dépendances
 
```bash
npm install
# or
yarn 
# or
pnpm install
# or
bun install
```

### Lancer le Serveur de Développement

Pour exécuter le serveur de développement, lancez l'une des commandes suivantes dans votre terminal :

```bash
npm run dev
# or
yarn dev
# or
pnpm dev
# or
bun dev
```

Visitez  [http://localhost:3000](http://localhost:3000) pour voir votre application en action. Commencez par modifier `app/page.tsx` pour apporter des modifications et les voir en temps réel.

## 🧞 Fonctionnalités

- **TypeScript**: Utilisez le typage fort de TypeScript pour écrire un code plus robuste et sans erreurs.
- **Tailwind CSS**:  Stylisez votre application efficacement avec CSS orienté utilitaires.
- **WAGMI Hooks**: Gérez les interactions avec les portefeuilles blockchain et les réseaux en toute simplicité.
- **Viem**: Gérez les interactions on-chain directement dans votre application frontend.
- **Morph Sepolia Testnet**: Connectez-vous au testnet Morph pour développer et tester vos dApps.

## ✨ Ressources d'Apprentissage

- **Morph L2**: En savoir plus sur Morph et ses capacités en visitant le [Morph Layer 2 Official Site](https://www.morphl2.io/).
- **Documentation Morph**:Pour des informations détaillées sur le fonctionnement de Morph et comment l'intégrer dans vos applications, consultez les [Morph Docs](https://docs.morphl2.io/docs/how-morph-works/intro/).

## 🚀 Déploiement

Déployez facilement votre application en utilisant des plateformes comme [Vercel](https://vercel.com/),  qui offre un support natif pour les applications Next.js, ou [Juno](https://juno.build), qui vous donne un contrôle total sur le déploiement de votre dApp sur le Web3. Consultez les guides spécifiques à chaque plateforme pour plus de détails sur le déploiement des applications Next.js.

















# Next.js TypeScript Starter Kit Onchain

![Une capture d'écran du kit de démarrage](./screenshot.png)

Ce kit de démarrage est conçu pour fournir un modèle complet pour construire des interfaces frontend pour vos dApps en utilisant Next.js, TypeScript, Shadcn, et Tailwind CSS. Il inclut une configuration pour les hooks WAGMI React et Viem pour des transactions onchain fluides.

Par défaut, ce modèle se connecte au réseau de test Morph Sepolia.

## 🧑‍🚀 Configuration Initiale

### Configuration de l'environnement

Avant de commencer, vous devez configurer vos variables d'environnement. Créez un fichier `.env.local` dans le répertoire racine en exécutant :

```bash
cp .env.example .env.local
```

Dans ce fichier, mettez à jour la variable `NEXT_PUBLIC_PROJECT_ID`avec votre identifiant de projet WalletConnect. Vous pouvez en obtenir un en enregistrant votre projet sur [WalletConnect Cloud](https://cloud.walletconnect.com/).

### Installer les dépendances

```bash
npm install
# or
yarn 
# or
pnpm install
# or
bun install
```

### Lancer le serveur de développement

Pour exécuter le serveur de développement, lancez une des commandes suivantes dans votre terminal :

```bash
npm run dev
# or
yarn dev
# or
pnpm dev
# or
bun dev
```

Visitez  [http://localhost:3000](http://localhost:3000) pour voir votre application en action. Commencez par modifier `app/page.tsx` pour faire des changements et les voir se refléter en temps réel.

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


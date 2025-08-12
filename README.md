<div align='center'>
  <h1>CG Base Plugin</h1>
</div>

This base plugin demonstrates the core capabilities of the [Common Ground Plugin Library](https://github.com/Common-Ground-DAO/CGPluginLib). It provides a practical example of integrating the plugin library, showcasing essential frontend-backend interactions and common use cases.

Use this as a base to creating your very own plugin and to understand how to leverage the full feature set of CG plugins in your own applications.


## Local Setup

- Go to your community settings
- Create a plugin
- As plugin URL, set http://localhost:5173
- Copy the key data shown after plugin creation
- Create a file .env.local in the root folder of this repository
- There, add the private and public key, and a cookie secret. Make sure you use exactly the variable names shown below:

```
VITE_PLUGIN_PUBLIC_KEY="-----BEGIN PUBLIC KEY-----\n---data---\n-----END PUBLIC KEY-----\n"
PLUGIN_PRIVATE_KEY="-----BEGIN PRIVATE KEY-----\n---data---\n-----END PRIVATE KEY-----\n"
COOKIE_SECRET=some_random_value
```

- Be sure your node version is at least >= 24 (you can use [nvm](https://github.com/nvm-sh/nvm) to manage your node versions)
- run `npm install`
- run `npm run prisma:migrate` to create a local sqlite database
- run `npm run dev` to run the plugin
- the plugin should now load when visiting it in your community



## Docker setup

- Change into the project directory
- Copy docker.env.local.example to docker.env.local
- There, update the plugin public and private key, and other changes according to your needs
- Now, run `docker build -t cg-plugin-server .`
- Run `docker run --rm --name cg-plugin-server -p 3000:3000 cg-plugin-server`
- You can now add the plugin for testing with `http://localhost:3000/` (change the port according to your needs)
- If you want to deploy the plugin to your server, we recommend providing the plugin through a reverse proxy server (e.g. with nginx, apache, ...). You should always use https (e.g. with letsencrypt).

## Available npm Scripts

### Development
- `npm run dev` - Start development server with hot reload
- `npm run build` - Build for production
- `npm run start` - Start production server
- `npm run typecheck` - Run TypeScript type checking

### Database
- `npm run prisma:generate` - Generate Prisma client
- `npm run prisma:migrate` - Create and apply new migration
- `npm run prisma:reset` - Reset database and reapply all migrations
- `npm run prisma:deploy` - Apply pending migrations (production)
- `npm run prisma:studio` - Open Prisma Studio GUI at `http://localhost:5555`
- `npm run db:seed` - Run database seeds

## (Optional) Token support

This project also includes basic web3 functionalities, such as being able to connect your wallet, scaffolding for testing with hardhat, and a "contracts" folder with some examples we use on the [cg-airdrop-plugin](https://github.com/Common-Ground-DAO/cg-airdrop-plugin). It has support for **ERC20** and **LUKSO LSP7**.

To use a local hardhat node for testing with smart contracts (optional):
- run `npm run hardhat:node`
- run `npm run hardhat:deploy` to deploy a local erc20 and an lsp7 token for local testing
- add the local HardHat chain to your local wallet plugin (Rabby, Metamask, etc.)
  - You can simply do that by connecting your wallet and selecting HardHat in the chain dropdown

## More 

For details on how the Plugin Library works and more, be sure to check [the repo for the Plugin Library](https://github.com/Common-Ground-DAO/CGPluginLib). For a fully functional implementation, look at our [Airdrop Plugin](https://github.com/Common-Ground-DAO/cg-airdrop-plugin) (cg-base-plugin is a squashed, cleaned up version of it).

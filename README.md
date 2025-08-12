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
- Create a file `.env.local` in the root folder of this repository
- There, add the private and public key, and a cookie secret. Make sure you use exactly the variable names as shown below:

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
- `npm run prisma:studio` - Open Prisma Studio GUI at `http://localhost:5555` - you can manage your local plugin database there
- `npm run db:seed` - Run database seeds

If you want to define your own database models, you can do that in prisma/schema.prisma. To get started with custom database models:
- Define your own models in `prisma/schema.prisma`. A good guide is available here: https://www.prisma.io/docs/guides/react-router-7 (note the link is for react-router 7, which this repository is based on)
- You can delete the `prisma/migrations` folder and run `npm run prisma:reset` to start from a clean state.
- Then, run `npm run prisma:migrate` 

### Hardhat
- `npm run hardhat:compile` - Compile solidity contracts in contracts/contracts
- `npm run hardhat:node` - Run a local hardhat node for solidity development
- `npm run hardhat:deploy` - Run the local hardhat deploy script in contracts/scripts/deploy-mocks.ts

## (Optional) Hardhat support

This project also includes basic web3 functionalities, such as being able to connect your wallet, scaffolding for testing with hardhat, and a "contracts" folder with some examples we use on the [cg-airdrop-plugin](https://github.com/Common-Ground-DAO/cg-airdrop-plugin). It offers simple ERC20 and LSP7 contracts for local deployment and use.

To use a local hardhat node for testing with smart contracts (optional):
- `npm run hardhat:node` will run a local blockchain for development and testing.
- `npm run hardhat:compile` will compile all solidity contracts in contracts/contracts.
- `npm run hardhat:deploy` to run the local deploy script in contracts/scripts/deploy-mocks.ts. It deploy a local ERC20 and LSP7 token for testing. You need to start the hardhat node first.
- You can add the local hardhat chain to your wallet plugin, simply by connecting your wallet and selecting Hardhat in the chain dropdown

## More

For details on the provided `npm run ...` commands, check the package.json file.

For details on how the Plugin Library works and more, be sure to check [CGPluginLib repository](https://github.com/Common-Ground-DAO/CGPluginLib). For a fully functional implementation, look at our [Airdrop Plugin repository](https://github.com/Common-Ground-DAO/cg-airdrop-plugin) (cg-base-plugin is a squashed, cleaned up version of it).

## Even more: Isolation mode, Gaming, Web Assembly

Common Ground supports a special mode for Plugins called "Isolation mode". It reloads the app.cg UI in a special mode that allows the use of some advanced Browser features for plugins (SharedArrayBuffer, high precision timers etc.) that are otherwise unavailable. This means that app.cg offers huge flexibility in what types of software you can embed.

There is a working game plugin integration that uses isolation mode to provide a web assembly compiled c++ game (Luanti) right on app.cg. It provides an experience similar to Minecraft and can even be played serverless (p2p). The code is available [here](https://github.com/Kaesual/minetest-wasm), and there is the [Luanti community on app.cg](https://app.cg/c/luanti/) where the plugin is developed and managed. In case you want to use web assembly compiled software in your community, get in touch there.

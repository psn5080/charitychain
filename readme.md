# CharityChain

CharityChain is a cutting-edge platform designed to empower users to make a positive impact on the world by donating to the charity programs of their choice with the ease and security of cryptocurrency transactions. With CharityChain, you can seamlessly support causes you're passionate about, all while harnessing the potential of digital currencies for philanthropic endeavors.

* [Video demo](https://youtu.be/8Wli2eASUVo)

| Home View | Donations View |
| --- | --- |
| ![Home View](https://user-images.githubusercontent.com/349751/144357448-.png) | ![Donations View](https://user-images.githubusercontent.com/349751/144357458-5ee0262e-78c2-493f-9931-f15616afee18.png) |

---

## Why Blockchain?

A donation platform based on a public blockchain offers several improvements over traditional options:

- **Accessibility**: Anyone with a digital wallet can make donations without relying on traditional banking or credit services, enabling contributions in amounts that may be unfeasible with conventional currency.
- **Trustworthiness**: Public blockchains eliminate the necessity for trust between parties since every transaction and wallet balance can be openly verified and examined.
- **Transparency**: Charitable activities are verifiable in the public domain, allowing donors to trace and authenticate their contributions, promoting transparency and accountability.
- **Speed and Efficiency**: Donations are promptly delivered to the intended charities' wallets without intermediary fees, streamlining the process.

## How CharityChain Works

The platform administrator enrolls charitable organizations, which can then enroll specific programs or campaigns. Donors choose from active programs and contribute a sum in ether, which is transferred to the designated charity's address.

### Roles

- **Owners**: The contract deployer can register new charities and delete existing ones.
- **Charities**: Registered charities can create, end, or complete programs and opt to leave the platform.
- **Donors**: Anyone can donate to ongoing programs and view their previous contributions.

## Project Implementation

CharityChain is a Truffle project with minimal dependencies. The client app is stateless and written in vanilla JavaScript. It uses `ethers.js` and [MetaMask](https://metamask.io/) as providers and the wallet.

### Directory Structure

- `contracts/`: Solidity contracts (main contract: `Fundraisers.sol`)
- `notes/`: Initial exploration
- `src/`: Client app
- `test/`: Unit tests for the contract in JS

### Installation

1. Verify [Node](https://nodejs.org/) version is at least v8.9.4.
2. Verify [Truffle](https://trufflesuite.com/) installation is at least v5.4.15.
3. Clone the repository.
4. Run `npm install` to fetch dependencies.
5. Start a local blockchain with `truffle develop`.
6. Deploy the contract with `migrate --reset`.
7. Create an instance of the contract and get its address.
8. Serve the client UI from `/src` using `npx serve`.

### Development

Commands for interacting with the contract:

- Register a charity: `f.registerCharity(accounts[1], 'SPCA')`
- Register a program: `f.registerProgram('Cat Adoption', {from: accounts[1]})`
- View programs: `f.getPrograms()`
- Donate: `f.donate(1, {from: accounts[9], value:55555555555555})`

### Deployment

Use [`dotenv`](https://www.npmjs.com/package/dotenv) for managing keys when deploying to public networks. Create a `.env` file with:

- `PRIVATE_KEY`: Private key of the deployment account.
- `INFURA_URL`: Infura URL with the project ID.
# CharityChain

CharityChain is a cutting-edge platform designed to empower users to make a positive impact on the world by donating to the charity programs of their choice with the ease and security of cryptocurrency transactions. With CharityChain, you can seamlessly support causes you're passionate about, all while harnessing the potential of digital currencies for philanthropic endeavors.

* [Video demo](https://youtu.be/8Wli2eASUVo)

| Home View | Donations View |
| --- | --- |
| <img width="375" alt="Screen Shot 2021-12-01 at 8 16 50 PM" src="https://user-images.githubusercontent.com/349751/144357448-0fadceab-a207-467e-83b7-d81c7b6e0ef7.png"> | <img width="375" alt="Screen Shot 2021-12-01 at 8 18 52 PM" src="https://user-images.githubusercontent.com/349751/144357458-5ee0262e-78c2-493f-9931-f15616afee18.png"> |

---

## How does a blockchain help?

Why is a donation platform based on a public blockchain considered an improvement over existing options?

- Accessibility: This platform offers unparalleled ease of use, allowing anyone with a digital wallet to make donations without relying on traditional banking or credit services, enabling contributions in amounts that may be unfeasible with conventional currency.

- Trustworthiness: Leveraging public blockchains eliminates the necessity for trust between parties since every transaction and wallet balance can be openly verified and examined, enhancing the overall reliability of the system.

- Transparency: Charitable activities are readily verifiable in the public domain, enabling donors to easily trace and authenticate their contributions to various charitable causes, promoting a higher level of transparency and accountability.

- Speed and Efficiency: Donations are promptly delivered to the intended charities' wallets without any intermediary fees, minimizing the need for substantial infrastructure or technical requirements on the charity's part, ultimately streamlining the process.

## How does CharityChain work?

The platform administrator has the authority to enroll charitable organizations, and these organizations, in turn, can enroll specific programs or campaigns. Prospective donors have the option to choose from the currently active programs and contribute a sum in ether, which is then transferred to the designated charity's address.

### Owners

The contract deployer serves as the owner, holding the following privileges:

- Enabling the registration of new charitable organizations.
- Exercising the authority to delete existing charitable organizations from the platform.

### Charities

The platform's creator needs to register a charity first. Once registered, a charity can:
  - Create a new program.
  - End an ongoing program.
  - Mark a program as completed.
  - Opt to leave the platform (this option may not be visible in the user interface).

### Donors

Anyone is welcome to donate to any ongoing program and can view their own previous contributions.

---

## Project implementation

CharityChain is a standard-configured Truffle project with [few dependencies](https://github.com/buzzpranav/CharityChain/blob/main/package.json#L22). The client app is stateless and written in vanilla JavaScript, with each page loading only the scripts it needs. Other than the contract migrations, the project does not require a build process.

It uses `ethers.js` and MetaMask as providers and the wallet.

To develop the project locally, you will need Truffle v5.4.15 or higher (Truffle's own [requirements](https://www.trufflesuite.com/docs/truffle/getting-started/installation) are Node v8.9.4 or later, and Linux, MacOS, or Windows).

### Directory structure

* `contracts/`: Solidity contracts – the project's only contract is `Fundraisers.sol`.
* `notes/`: Initial exploration.
* `src/`: Client app.
* `test/`: Unit tests for the contract in JS.

### Installation

* Use `node -v` to verify your Node version is at least v8.9.4. If not, follow [Node's instructions](https://nodejs.dev/learn/how-to-install-nodejs) for installation or updating.
* Use `truffle --version` to verify your Truffle installation is at least v5.4.15. If not, follow their [instructions](https://www.trufflesuite.com/docs/truffle/getting-started/installation) to update or install it (try `npm install -g truffle` for the latest version).
* Clone this repository to your local machine with `git clone git@github.com:kwight/blockchain-developer-bootcamp-final-project.git` (assumes you have SSH keys set up – HTTPS will work fine too).
* `cd` into the root of your cloned repo.
* Run `npm install` to fetch the package dependencies.
* Run `truffle develop`. This will start up a local blockchain and give you a console.
* Make note of the URL and port; if you're not using the defaults, or are using another blockchain such as Ganache, [this line](https://github.com/buzzpranav/CharityChain/blob/main/src/scripts/fundraisers.js#L28) will need to be updated, as well as the `development` network in `truffle-config.js`.
* In that console, deploy the contract with `migrate --reset`.
* Create an instance of the contract with `f = await Fundraisers.deployed()`.
* Enter `f.address` to get the contract's local address, and enter it on [this line](https://github.com/buzzpranav/CharityChain/blob/main/src/scripts/fundraisers.js#L5).
* The client UI is served as static files from `/src`. In that directory in a different terminal window (keep the development console running), run `npx serve` and open the given URL in your browser. Any local webserver service run from that directory will also work.
* Back in the console, run `test` to verify the contract unit tests all pass.

You're all set – you've got a console with access to the deployed contract on the local blockchain, and a front-end in your browser that's using the local blockchain as its data source.

### Development

Here are some commands you can use to interact with the contract from the console. These assume you've set the `f` variable from the installation notes above. Remember that on the local blockchain, the contract owner is the `accounts[0]` account (which is the default `from:` value when one isn't specified). If the client UI is open while running commands on the console, it will update automatically.

* Register a charity: `f.registerCharity(accounts[1], 'SPCA')`
* Register a program: `f.registerProgram('Cat Adoption', {from: accounts[1]})`
* Register another program: `f.registerProgram('Dog Rescue', {from: accounts[1]})`
* View the registered programs: `f.getPrograms()`
* Mark the first program as complete: `f.completeProgram(0, {from: accounts[1]})`
* Donate to the dog rescue from that account: `f.donate(1, {from: accounts[9], value:55555555555555})`

### Deployment

The project uses `dotenv` for managing keys when deploying to public networks. Create a local `.env` file (which is gitignored) with the following constants. Ropsten is already configured (other networks would need to be added to `truffle-config.js`).

* `PRIVATE_KEY`: Private key of the account that should be owner on deployment.
* `INFURA_URL`: Infura URL with the project ID.

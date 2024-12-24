# Solana-SPL-Program-Tutorial

A highly requested tutorial! We are covering from start to finish how to write Solana SPL Token Program to launch your own token on the Solana blockchain. 


<img src="https://raw.githubusercontent.com/net2devcrypto/misc/main/anchorlogo.png" width="150" height="45"> <img src="https://raw.githubusercontent.com/net2devcrypto/misc/main/sol-logo.png" width="190" height="40">

> [!NOTE]  
> THE FILES ATTACHED TO THIS REPO ARE FOR EDUCATIONAL PURPOSES ONLY.
> NOT FINANCIAL ADVICE
> USE IT AT YOUR OWN RISK, I'M NOT RESPONSIBLE FOR ANY USE, ISSUES.

<h3>Video 1</h3>

<a href="https://youtu.be/g2YK_YBWA9A" target="_blank"><img src="https://github.com/net2devcrypto/misc/blob/main/ytlogo2.png" width="150" height="40"></a>

<h3>Video 2</h3>

<a href="https://youtu.be/tzaZJXS7AWM" target="_blank"><img src="https://github.com/net2devcrypto/misc/blob/main/ytlogo2.png" width="150" height="40"></a>

<h3>Setup Anchor Development Environment Instructions</h3>

<h4>The steps below are compatible with Ubuntu 22.04</h4>

> [!NOTE]  
> If you have Windows, please download VMware Workstation Player, install then create a virtual machine. Follow the tutorial video for full guidance.
> 
> VMware Workstation Player for Windows: https://www.techspot.com/downloads/downloadnowfile/1969/?evp=4c50cf08866937ea246522b86f4d4286&file=2171
>
> Ubuntu Desktop 22.04 ISO: https://releases.ubuntu.com/jammy/ubuntu-22.04.4-desktop-amd64.iso
> 

<h4>Step 1 Dependencies</h4>

```shell
sudo apt-get update && sudo apt-get upgrade && sudo apt-get install -y curl pkg-config build-essential libudev-dev libssl-dev
```

<h4>Step 2 Install Rust</h4>

```shell
curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh
```
Press Enter When Prompted.

<h4>Step 3 Install Solana CLI</h4>

```shell
sh -c "$(curl -sSfL https://release.solana.com/v1.18.14/install)"
```

<h4>Step 4 Update PATH (UBUNTU ONLY)</h4>

```shell
nano ~/.bashrc
```

Add this line to end of file:

```shell
export PATH="/root/.local/share/solana/install/active_release/bin:$PATH"
```

save by :  CTRL + X , Press Y, ENTER

Reboot PC.

Open back the terminal then confirm that Solana Cli is active by typing "solana" and press ENTER.

<h4>Step 5 Install NodeJS</h4>

```shell
curl -fsSL https://deb.nodesource.com/setup_20.x -o nodesource_setup.sh
```

```shell
sudo -E bash nodesource_setup.sh
```

```shell
sudo apt-get install -y nodejs
```

Verify Installation:

```shell
node -v
```

<h4>Step 6 Install Yarn</h4>

```shell
corepack enable
yarn init -2
```

Ignore Error: Internal Error: Process git failed to spawn

<h4>Step 7 Install Anchor</h4>

```shell
cargo install --git https://github.com/coral-xyz/anchor avm --locked --force
```

```shell
avm install latest
avm use latest
```

Verify Installation:

```shell
anchor --version
```

<h4>Step 8 Generate Dev Solana Wallet </h4>

```shell
solana-keygen new
```

<h3>Video 3</h3>

<a href="https://youtu.be/66o6qma2Jdc" target="_blank"><img src="https://github.com/net2devcrypto/misc/blob/main/ytlogo2.png" width="150" height="40"></a>

<h3>Deploy SPL Token Program</h3>


## Step 1 Build and Deploy SPL Program

<h5> A - Download Repo Folder SplToken</h5>

<h5> B - Create a new Anchor project named "spl"</h5>

```shell
anchor init spl
```

<h5> C - Open the spl project folder in VS Code</h5>

<h5> D - Replace the lib.rs file located in the programs/spl/src folder with the lib.rs file located in the downloaded SplToken folder</h5>

<h5> E - Replace the cargo.toml file located in the project programs/spl folder with the cargo.toml file located in the downloaded SplToken folder</h5>

<h5> F - Go to the Anchor.toml file located at the root of the project folder and change cluster to devnet.</h5>

```shell
[provider]
cluster = "devnet"
```

SAVE FILE!

<h5> G - Open terminal and proceed to build project then deploy.</h5>

```shell
anchor build
```

```shell
anchor deploy
```

<h5> H - Copy the program ID obtained once the deployment has completed.</h5>

<h5> I - Go to target/types/spl.ts and update the address with the program ID obtained after anchor deploy.</h5>

```shell
export type Spl = {
  "address": "ENTERPROGRAMID",
```

SAVE FILE!

<h5> J - Go to target/idl/spl.json and update the address with the program ID obtained as well</h5>

```shell
{
  "address": "ENTERPROGRAMID",
```

SAVE FILE!

<h5> K - Go to programs/src/lib.rs and update declareid with the program ID obtained as well</h5>

```shell
declare_id!("ENTERPROGRAMID");
```

SAVE FILE!


## Step 2 Create and Store Metadata in Arweave

Watch @ https://youtu.be/66o6qma2Jdc?t=3m40s

Copy the metadata.json Arweave path.

## Step 3 Initiate SPL Token and Mint

<h5> A - Replace on spl project, the file tests/spl.ts with the spl.ts test file located in the downloaded SplToken folder</h5>

<h5> B - Edit the spl.ts test file by providing the token metadata with your values and amount to initially mint.</h5>

```shell
const metadata = {
    name: "Net2Dev Rewards SPL",
    symbol: "N2DR",
    uri: "https://arweave.net/Xjqaj_rYYQGrsiTk9JRqpguA813w6NGPikcRyA1vAHM", //replace with Arweave metadata json path
    decimals: 9,
  };
const mintAmount = 10; // Amount of tokens to initially mint.
```

SAVE FILE!

<h5> C - Open terminal and proceed to run test.</h5>

```shell
anchor test
```

## Step 4 Transfer Tokens to new Wallet from Owner Wallet

<h5> A - Copy the file spl-transfer.js from the downloaded SplToken folder and paste into the spl project folder</h5>

<h5> B - Open terminal and install solana/spl-token sdk</h5>

```shell
npm i @solana/spl-token
```

<h5> C - Obtain the private key of the program owner as string, copy the value</h5>

Watch @ https://youtu.be/66o6qma2Jdc?t=55m30s

<h5> D - Edit the spl-transfer.js with the following values</h5>

```shell
const owner = 'REPLACEWITHSTRINGPRIVATEKEY' // private key string previously obtained 
const spltoken = new PublicKey("SPLPROGRAMID"); // Program Id of your SPL Token, obtained during "anchor deploy"

const tokens = 2; // set the amount of tokens to transfer.
```

SAVE FILE!


<h5> E - Create new solana wallet (Phantom Wallet for example) and copy address</h5>

<h5> F - Add the new wallet address obtained previously to the spl-transfer.js as destination wallet </h5>


```shell
const destWallet = new PublicKey("NEWWALLETADDRESS");
```

SAVE FILE!


<h5> G - Run the Test and confirm that the ATA got generated and you got tokens on the new destination wallet!</h5>


```shell
node spl-transfer.js
```

Expected Result:


```shell
create ata txhash: 4uU9xegH7YZ3tTC934PBSzsVQf3pwoA5BWwXnpFpuK7aCTDu9yqK32r2Vjsbqz4vxhMReeL6NkmQ1hZPg3XSAXh8
Tokens transferred Successfully, Receipt: rttSvKXANuiTZkUmx1gj5B1jSH6bNz4NU64YmvqXouLYoWzqejot1NXxGrML7L87FWa2tX8WBDViKw8C5nmEZrC
```

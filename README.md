# CREATE-A-CUSTOM-ERC-20-TOKEN-USING-SOLIDITY-AND-DEPLOY-IT-ON-AN-ETHEREUM-TESTNET.
CREATE A CUSTOM ERC-20 TOKEN USING SOLIDITY AND DEPLOY IT ON AN ETHEREUM TESTNET.

require("@nomicfoundation/hardhat-toolbox");
require('dotenv').config();

/** @type import('hardhat/config').HardhatUserConfig */
module.exports = {
  solidity: "0.8.19",
  networks: {
    sepolia: { // or goerli
      url: process.env.SEPOLIA_RPC_URL || "",
      accounts: [process.env.PRIVATE_KEY || ""],
    },
  },
  etherscan: {
    apiKey: process.env.ETHERSCAN_API_KEY, // Optional: for verification
  },
};
const hre = require("hardhat");

async function main() {
  const initialSupply = 1000000 * 10**18; // 1 million tokens with 18 decimals
  const MyToken = await hre.ethers.getContractFactory("MyToken");
  const myToken = await MyToken.deploy(initialSupply);

  await myToken.deployed();

  console.log("MyToken deployed to:", myToken.address);
}

main().catch((error) => {
  console.error(error);
  process.exitCode = 1;
});

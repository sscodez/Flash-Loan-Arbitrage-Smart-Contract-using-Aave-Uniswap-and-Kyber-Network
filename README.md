# Flash-Loan-Arbitrage-Smart-Contract-using-Aave-Uniswap-and-Kyber-Network
This contract uses Aave flash loans &amp; Uniswap/Kyber exchanges for arbitrage trading. Users borrow DAI &amp; buy ETH on the cheaper exchange for profit, then repay the flash loan + fee &amp; keep the profit. No collateral is required, showcasing the power of flash loans for accessing liquidity.


Importing necessary libraries and interfaces:
The first lines of the contract imports the required libraries and interfaces for using the Aave flash loan functionality, as well as the Uniswap and Kyber network interfaces for the arbitrage trades.

Defining the contract:
The main contract is defined as FlashLoanArbitrage, which is set up to inherit from the FlashLoanReceiverBase contract provided by Aave.

Defining variables:
The contract defines several variables, including addresses for the lending pool, token addresses for DAI, ETH, and other tokens, as well as instances of the Uniswap and Kyber network interfaces.

Defining the executeArbitrage function:
This function is where the arbitrage trades take place. The function first takes out a flash loan for a specified amount of DAI. The DAI is then used to purchase ETH on either the Uniswap or Kyber network, depending on which offers a better price. The purchased ETH is then immediately sold on the other network for a profit. The profits are used to repay the flash loan plus a small fee, and the remaining profits are transferred to the contract owner.

Defining the startArbitrage function:
This function simply calls the executeArbitrage function and passes in the amount of DAI to be borrowed as an argument.

Defining the receiveFlashLoan function:
This function is required by the FlashLoanReceiverBase contract and is called by the Aave protocol when the flash loan is executed. In this function, the arbitrage trade is initiated by calling the executeArbitrage function.

## Prerequisites

Before using the contract, make sure you have the following dependencies:

- Aave Protocol V2: [ILendingPool.sol](https://github.com/aave/protocol-v2/blob/master/contracts/interfaces/ILendingPool.sol), [ILendingPoolAddressesProvider.sol](https://github.com/aave/protocol-v2/blob/master/contracts/interfaces/ILendingPoolAddressesProvider.sol)
- Uniswap V2 Periphery: [IUniswapV2Router02.sol](https://github.com/Uniswap/uniswap-v2-periphery/blob/master/contracts/interfaces/IUniswapV2Router02.sol)
- OpenZeppelin Contracts: [IERC20.sol](https://github.com/OpenZeppelin/openzeppelin-contracts/blob/master/contracts/token/ERC20/IERC20.sol)

## Contract Functions

### Constructor

```solidity
constructor(ILendingPoolAddressesProvider _provider, IUniswapV2Router02 _uniswapRouter, IERC20 _dai, IERC20 _usdc, address _ethAddress)
```

The constructor initializes the contract by setting the Aave Lending Pool Addresses Provider, Uniswap Router, DAI token, USDC token, and ETH address.

### startArbitrage

```solidity
function startArbitrage(uint256 amount) external
```

This function initiates the flash loan arbitrage by executing a flash loan from the Aave lending pool. The specified `amount` is borrowed as a flash loan.

### executeArbitrage

```solidity
function executeArbitrage(uint256 amount, uint256 amountToRepay) external
```

Once the flash loan is received, this function is called to execute the arbitrage strategy. It swaps DAI for USDC on Uniswap, then swaps USDC for ETH on Uniswap. Finally, it repays the flash loan by transferring the specified `amountToRepay` of DAI back to the lending pool.

### withdrawTokens

```solidity
function withdrawTokens(IERC20 token, uint256 amount) external
```

The contract owner can use this function to withdraw any ERC20 tokens that have been deposited into the contract. Specify the `token` address and the `amount` to withdraw.

### withdrawETH

```solidity
function withdrawETH() external
```

The contract owner can use this function to withdraw any ETH balance that has been deposited into the contract.

## Usage

1. Deploy the FlashLoanArbitrage contract, providing the necessary constructor parameters.
2. Fund the contract with DAI tokens to cover the flash loan amount.
3. Call the `startArbitrage` function to initiate the flash loan and execute the arbitrage strategy.
4. Verify the successful execution of the arbitrage by checking the resulting ETH balance.

## Contributing

Contributions are welcome! If you find any issues or would like to enhance the contract, feel free to open a pull request.

## License

This project is licensed under the [MIT License](LICENSE).

## Acknowledgments

- [Aave](https://aave.com/) for providing the Aave lending protocol.
- [Uniswap](https://uniswap.org/) for the decentralized exchange functionality.
- [OpenZeppelin](https://openzeppelin.com/) for the ERC20 token interface.

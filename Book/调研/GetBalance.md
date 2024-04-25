```javascript
const tokenAbi = [{
    constant: true,
    inputs: [
      {
        name: '_owner',
        type: 'address',
      },
    ],
    name: 'balanceOf',
    outputs: [
      {
        name: 'balance',
        type: 'uint256',
      },
    ],
    payable: false,
    stateMutability: 'view',
    type: 'function',
  }]
const web3 = new Web3(); // Initialize Web3 with your provider
const tokenContract = new web3.eth.Contract(tokenAbi, tokenAddress); // Create an instance of the token contract

async function getTokenBalance(tokenContract, address) {
  try {
    const balance = await tokenContract.methods.balanceOf(address).call();
    return balance;
  } catch (error) {
    console.error('Error retrieving token balance:', error);
    // Handle error case
  }
}

// Usage:
const address = '0x1234567890abcdef1234567890abcdef12345678'; // Replace with the address you want to check
getTokenBalance(tokenContract, address).then((balance) => {
  console.log('Token Balance:', balance);
  // Use the balance in your code
});
```
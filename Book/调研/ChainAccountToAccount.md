```javascript
// 获取用户的账户地址
  const senderAddress = ''; // 发送者账户地址

  // USDT 合约地址
  const usdtAddress = ''; // 填入您的 USDT 合约地址

  // USDT 合约 ABI（根据实际合约地址和 ABI 进行替换）
  // const usdtAbi = [...]; // 填入您的 USDT 合约 ABI
  const usdtAbi = [{
    "inputs": [
      {
        "internalType": "address",
        "name": "recipient",
        "type": "address"
      },
      {
        "internalType": "uint256",
        "name": "amount",
        "type": "uint256"
      }
    ],
    "name": "transfer",
    "outputs": [
      {
        "internalType": "bool",
        "name": "",
        "type": "bool"
      }
    ],
    "stateMutability": "nonpayable",
    "type": "function"
  },]

  // 创建 USDT 合约实例
  const usdtContract = new web3.eth.Contract(usdtAbi, usdtAddress);

  // 接收者账户地址
  const receiverAddress = ''; // 填入接收者的账户地址

  // 转账金额（以 USDT 的最小单位为准，如六位小数的 USDT 金额需要乘以 1e6）
  const amount = 3000000; // 示例为 1 USDT

  
  const nonce_2 = await web3.eth.getTransactionCount(account)
  const nonce2 = web3.utils.toHex(nonce_2)
  const _gasPrice = await web3.eth.getGasPrice()

  await usdtContract.methods.transfer(receiverAddress, amount).send({ from: senderAddress, nonce: nonce2, gasPrice: _gasPrice })
  .on('transactionHash', function(hash) {
    console.log('Transfer initiated: ' + hash);
  })
  .on('confirmation', function(confirmationNumber, receipt) {
    console.log('Transfer confirmed in block: ' + receipt.blockNumber);
  })
  .on('receipt', function(receipt) {
    console.log('Transfer receipt received');
  })
  .on('error', function(error, receipt) {
    console.error('Transfer error:', error);
  });
```
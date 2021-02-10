# Multi-Blockchain-Wallet

![POA](https://github.com/docfern/multi-blockchain-wallet/blob/main/wallet/screenshots/newtons_coin_cradle.jpg)
<br>
<br>
## Instruction: step by step
### New startup market race - initial requirement
Main focus of a newly founded company is to build a portfolio management system (PMS) that supports both, traditional assets (like gold, silver, stocks, etc) and currently very hot topic - crypto-assets!!! But, as there are so many coins out there, our task to understand how HD wallets work, and to build out a system that can create them.<br>
<br>
### Race to the market: Let the games begin !!!
Unfortunately, there aren't as many tools available in Python for this sort of thing, yet.<br>

Thankfully, there is a command line tool, hd-wallet-derive that supports not only BIP32, BIP39, and BIP44, but also supports non-standard derivation paths for the most popular wallets out there today!<br>

Indeed, we have to develop and integrate the script wallet.py at backend with our dearest old friend, Python.<br>
<br>
Once we integrate this "universal" wallet, we can use it to manage billions of addresses across 300+ coins, and it will give us serious edge against the competition.<br>
<br>

In this assignment, we will only need to get 2 coins working: Ethereum and Bitcoin Testnet. Ethereum keys are the same format on any network, so the Ethereum keys should work with your custom networks or testnets.

### Dependencies

- PHP must be installed on your operating system (any version, 5 or 7). Don't worry, you will not need to know any PHP (just in case if ./derive is not working in comand line, which in my experience happened on Windows machine, we will use it as a backup in one coding line).
- We have to clone the hd-wallet-derive tool.
- bit Python Bitcoin library.
- web3.py Python Ethereum library.

### Set-up Project

- Create a project directory called wallet and cd into it.
- Clone the hd-wallet-derive tool into this folder and install it using the instructions on its README.md.
- Create a symlink called derive for the hd-wallet-derive/hd-wallet-derive.php script into the top level project directory like so: ln -s hd-wallet-derive/hd-wallet-derive.php derive<br>

This will clean up the command needed to run the script in our code, as we can call ./derive instead of ./hd-wallet-derive/hd-wallet-derive.php.

- Test that you can run the ./derive script properly, use one of the examples on the repo's README.md.

### NOTE: If one get an error running ./derive, as it can happen on windows machine then use: php ./hd-wallet-derive/hd-wallet-derive.php.
- Create a file called wallet.py -- this will be your universal wallet script.
Your directory tree should look something like this:

![POA](https://github.com/docfern/multi-blockchain-wallet/blob/main/wallet/screenshots/tree.jpg)
<br>
<br>
### Setup constants file to manage coins
- In a separate file, constants.py, set the following constants:
  - BTC = 'btc'
  - ETH = 'eth'
  - BTCTEST = 'btc-test'
- In wallet.py, import all constants: from constants import *
- Use these anytime you reference these strings, both in function calls, and in setting object keys.

### Generate a Mnemonic phrase
- Generate a new 12 word mnemonic using hd-wallet-derive or by using this tool.
- Set this mnemonic as an environment variable, and include the one you generated as a fallback using: mnemonic = os.getenv('MNEMONIC', 'insert mnemonic here')

### Deriving a wallet
- Pass as variables Mnemonic (--mnemonic), Coin (--coin) and Numderive (--numderive), then set the --format=json flag, parse the output into a JSON object using json.loads(output).And finally pass all into one function, called 'derive_wallets'.
- When done properly, the final object should look something like this (there are only 3 children each in this image):
- Accounts used in the project are marked for BTC Test and ETH<br> 
<br>
![POA](https://github.com/docfern/multi-blockchain-wallet/blob/main/wallet/screenshots/wallet_object.jpg)

### Executing test transactions by calling the functions from wallet.py
#### BTCTest transaction
```btc_acc = priv_key_to_account(BTCTEST,btc_PrivateKey) ``` ```create_trx(BTCTEST,btc_acc,"miZgMxdGzSxCTpWazfD2KqhewoUvcQ6CC1", 0.1)``` ```send_trx(BTCTEST,btc_acc,'miZgMxdGzSxCTpWazfD2KqhewoUvcQ6CC1',0.1)```
<br>
#### Confirmation of Executed Transaction

![POA](https://github.com/docfern/multi-blockchain-wallet/blob/main/wallet/screenshots/eth_trans_confirm.jpg)

### ETH transaction - using local private blockchain
```eth_acc = priv_key_to_account(ETH,eth_PrivateKey) ```
```create_trx(ETH,eth_acc,"0xba51af165c60A32B3d23Df9B332b4A86cED4A1B9", 1000)``` 
```send_trx(ETH, eth_acc,"0xba51af165c60A32B3d23Df9B332b4A86cED4A1B9", 1000)```
#### Confirmation of Executed Transaction

![POA](https://github.com/docfern/multi-blockchain-wallet/blob/main/wallet/screenshots/eth_trans_config.jpg)

# Custom Subnet

# Customized Subnet Utilizing HyperSDK
This project aims to enable the creation, management, and interaction of tokens within a virtual machine environment.
## Features
* **Token Creation:** Create new tokens effortlessly.
* **Token Management:** Easily manage your tokens, including transferring and checking balances.
* **Interoperability:** Built for smooth integration with other virtual machine environments.

## Installation
1. Clone the repository:
   ```
   git clone https://github.com/Metacrafters/tokenvm.git
   cd tokenvm
   ```
2. Configure the constants in `consts/consts.go`.
![image](https://github.com/user-attachments/assets/ddc43ab6-cc3f-47b1-93e3-b9508961fb42)
3. Insert the code into `registry/registry.go`.
![image](https://github.com/user-attachments/assets/99a5895b-135f-411d-8504-d6cbf83a0264)
4. Launch the subnet with the following command:
   ```
   ./scripts/run.sh;
   ```
   By default, this will allocate all funds on the network.
5. Next, build the project by running the following command:
   ```
   ./scripts/build.sh
   ```
   This command will place the compiled CLI in `./build/token-cli`.

## Mint and Trade
1. **Step 1: Create Your Asset**
   Execute the following command:
   ```
   ./build/token-cli action create-asset
   ```
   The output should resemble this:
   ```
   database: .token-cli
   address: token1rvzhmceq997zntgvravfagsks6w0ryud3rylh4cdvayry0dl97nsjzf3yp
   chainID: Em2pZtHr7rDCzii43an2bBi1M2mTFyLN33QP1Xfjy7BcWtaH9
   metadata (can be modified later): MarioCoin
   continue (y/n): y
   ✅ txID: 27grFs9vE2YP9kwLM5hQJGLDvqEY9ii71zzdoRHNGC4Appavug
   ```
2. **Step 2: Mint Your Asset**
   Once you have created your asset, you can mint some of it by running:
   ```
   ./build/token-cli action mint-asset
   ```
   After completing this, the output should appear similar to this (it's usually easiest to mint to yourself):
   ```
   database: .token-cli
   address: token1rvzhmceq997zntgvravfagsks6w0ryud3rylh4cdvayry0dl97nsjzf3yp
   chainID: Em2pZtHr7rDCzii43an2bBi1M2mTFyLN33QP1Xfjy7BcWtaH9
   assetID: 27grFs9vE2YP9kwLM5hQJGLDvqEY9ii71zzdoRHNGC4Appavug
   metadata: MarioCoin supply: 0
   recipient: token1rvzhmceq997zntgvravfagsks6w0ryud3rylh4cdvayry0dl97nsjzf3yp
   amount: 10000
   continue (y/n): y
   ✅ txID: X1E5CVFgFFgniFyWcj5wweGg66TyzjK2bMWWTzFwJcwFYkF72
   ```
3. **Step 3: Check Your Balance**
   To verify that the minting was successful, check your balance with the following command:
   ```
   ./build/token-cli key balance
   ```
   When done, the output should look like this:
   ```
   database: .token-cli
   address: token1rvzhmceq997zntgvravfagsks6w0ryud3rylh4cdvayry0dl97nsjzf3yp
   chainID: Em2pZtHr7rDCzii43an2bBi1M2mTFyLN33QP1Xfjy7BcWtaH9
   assetID (use TKN for native token): 27grFs9vE2YP9kwLM5hQJGLDvqEY9ii71zzdoRHNGC4Appavug
   metadata: MarioCoin supply: 10000 warp: false
   balance: 10000 27grFs9vE2YP9kwLM5hQJGLDvqEY9ii71zzdoRHNGC4Appavug
   ```
4. **Step 4: Place an Order**
   To put an order on-chain that allows someone to trade the native token (TKN) for yours, run the following command:
   ```
   ./build/token-cli action create-order
   ```
   After running it, the output should resemble this:
   ```
   database: .token-cli
   address: token1rvzhmceq997zntgvravfagsks6w0ryud3rylh4cdvayry0dl97nsjzf3yp
   chainID: Em2pZtHr7rDCzii43an2bBi1M2mTFyLN33QP1Xfjy7BcWtaH9
   in assetID (use TKN for native token): TKN
   ✔ in tick: 1█
   out assetID (use TKN for native token): 27grFs9vE2YP9kwLM5hQJGLDvqEY9ii71zzdoRHNGC4Appavug
   metadata: MarioCoin supply: 10000 warp: false
   balance: 10000 27grFs9vE2YP9kwLM5hQJGLDvqEY9ii71zzdoRHNGC4Appavug
   out tick: 10
   supply (must be a multiple of out tick): 100
   continue (y/n): y
   ✅ txID: 2TdeT2ZsQtJhbWJuhLZ3eexuCY4UP6W7q5ZiAHMYtVfSSp1ids
   ```
5. **Step 5: Partially Fill the Order**
   Now that an order is on-chain, let’s fill it! Execute the following command:
   ```
   ./build/token-cli action fill-order
   ```
   Once completed, the output should look like this:
   ```
   database: .token-cli
   address: token1rvzhmceq997zntgvravfagsks6w0ryud3rylh4cdvayry0dl97nsjzf3yp
   chainID: Em2pZtHr7rDCzii43an2bBi1M2mTFyLN33QP1Xfjy7BcWtaH9
   in assetID (use TKN for native token): TKN
   balance: 997.999993843 TKN
   out assetID (use TKN for native token): 27grFs9vE2YP9kwLM5hQJGLDvqEY9ii71zzdoRHNGC4Appavug
   metadata: MarioCoin supply: 10000 warp: false
   available orders: 1
   0) Rate(in/out): 100000000.0000 InTick: 1.000000000 TKN OutTick: 10 27grFs9vE2YP9kwLM5hQJGLDvqEY9ii71zzdoRHNGC4Appavug Remaining: 100 27grFs9vE2YP9kwLM5hQJGLDvqEY9ii71zzdoRHNGC4Appavug
   select order: 0
   value (must be a multiple of in tick): 2
   in: 2.000000000 TKN out: 20 27grFs9vE2YP9kwLM5hQJGLDvqEY9ii71zzdoRHNGC4Appavug
   continue (y/n): y
   ✅ txID: uw9YrZcs4QQTEBSR3guVnzQTFyKKm5QFGVTvuGyntSTrx3aGm
   ```

6. **Step 6: Cancel Order**
   If you decide to cancel the order, run the following command:
   ```
   ./build/token-cli action close-order
   ```
   The output should appear like this:
   ```
   database: .token-cli
   address: token1rvzhmceq997zntgvravfagsks6w0ryud3rylh4cdvayry0dl97nsjzf3yp
   chainID: Em2pZtHr7rDCzii43an2bBi1M2mTFyLN33QP1Xfjy7BcWtaH9
   orderID: 2TdeT2ZsQtJhbWJuhLZ3eexuCY4UP6W7q5ZiAHMYtVfSSp1ids
   out assetID (use TKN for native token): 27grFs9vE2YP9kwLM5hQJGLDvqEY9ii71zzdoRHNGC4Appavug
   continue (y/n): y
   ✅ txID: poGnxYiLZAruurNjugTPfN1JjwSZzGZdZnBEezp5HB98PhKcn
   ```
## Transfer Assets to Another Subnet
To initiate a transfer between the two subnets you created, execute the following command:
```
./build/token-cli action export
```
Upon completion, the output should look like this:
```
database: .token-cli
address: token1rvzhmceq997zntgvravfagsks6w0ryud3rylh4cdvayry0dl97nsjzf3yp
chainID: Em2pZtHr7rDCzii43an2bBi1M2mTFyLN33QP1Xfjy7BcWtaH9
✔ assetID (use TKN for native token): TKN
balance: 997.999988891 TKN
recipient: token1rvzhmceq997zntgvravfagsks6w0ryud3rylh4cdvayry0dl97nsjzf3yp
amount: 10
reward: 0
available chains: 1 excluded: [Em2pZtHr7rDCzii43an2bBi1M2mTFyLN33QP1Xfjy7BcWtaH9]
0) chainID: cKVefMmNPSKmLoshR15Fzxmx52Y5yUSPqWiJsNFUg1WgNQVMX
destination: 0
swap on import (y/n): n
continue (y/n): y
✅ txID: 24Y2zR2qEQZSmyaG1BCqpZZaWMDVDtimGDYFsEkpCcWYH4dUfJ
perform import on destination (y/n): y
22u9zvTa8cRX7nork3koubETsKDn43ydaVEZZWMGcTDerucq4b to: token1rvzhmceq997zntgvravfagsks6w0ryud3rylh4cdvayry0dl97nsjzf3yp source assetID: TKN output assetID: 2rST7KDPjRvDxypr6Q4SwfAwdApLwKXuukrSc42jA3dQDgo7jx value: 10000000000 reward: 10000000000 return: false
✔ switch default chain to destination (y/n): y
```

--- 

# PROJECT BY
- SHUBHAM

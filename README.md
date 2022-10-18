# Blockchain with Python

## In this Colab notebook, the intention is to develop a simple Blockchain with Python, to understand how a Block is created, how a chain works and the importance of the hash within the Blockchain. I made comments almost in each line of code to be understandable to everybody. 

### We're going to use Colab for the development of the code in Python and Postman to get some request we're going to send from Colab with Flask. 

- For more information about Postman: https://www.postman.com/
- For more information about Flask: https://flask.palletsprojects.com/en/2.2.x/

### The project is divided in 3 steps: 

1. Build the Blockchain.
2. Mine the Blockchain to let the new blocks be added.
3. Run the app to recieve the results. 

### 1. Build the Blockchain.

Each Block is going to have the next attributes: 

 ```def create_block(self, proof, previous_hash):             
      block = {'index': len(self.chain) + 1,
               'timestamp': str(datetime.datetime.now()), 
               'proof': proof,
               'previous_hash': previous_hash} 
 ```

Where:

- **Index**: The number of the block.
- **Time Stamp**: The moment of the creation of the block. 
- **Proof**: We're going to use Proof of Work (PoW) to mine the block.
- **Previous Hash**: The hash of the last block. 

**IMPORTANT**

**What is Proof of Work?** 

Proof of work (PoW) is a decentralized consensus mechanism that requires members of a network to expend effort solving an arbitrary mathematical puzzle to prevent anybody from gaming the system.


**What is the SHA-256 Algorithm**

SHA-2 (Secure Hash Algorithm 2), of which SHA-256 is a part, is one of the most popular hash algorithms around. A cryptographic hash, also often referred to as a “digest”, “fingerprint” or “signature”, is an almost perfectly unique string of characters that is generated from a separate piece of input text. SHA-256 generates a 256-bit (32-byte) signature.

To generate the hash of each block, we're going to use "hashlib"


 ```def proof_of_work(self, previous_proof):
      new_proof = 1                                        
      check_proof = False                                   
      while check_proof is False:
          hash_operation = hashlib.sha256(str(new_proof**2 - previous_proof**2).encode()).hexdigest()
          if hash_operation[:4] == '0000':                 
            check_proof = True
          else:
              new_proof +=1
      return new_proof

 ```
For more information about Haslib for Python: https://docs.python.org/3/library/hashlib.html

### 2. Mine the Blockchain.

In this part, we're going to assume that a miner is mining a Block to be added to the chain, getting the next result to be received to the miner

 ```response = {'message': 'You just have mined succesfully a block!',   #--> Message to the miner after mined a block
                'index': block['index'],
                'timestamp': block['timestamp'],
                'proof': block['proof'],
                'previous_hash': block['previous_hash']}
 
 ```
                
### 3. Run the app to recieve the results.

We created: 
 ```@app.route('/mine_block', methods = ['GET']) ```

To get the response when mining a Block.

 ```@app.route('/get_chain', methods = ['GET']) ```

To get the response of the chain with the Blocks added previusly. 

# Blockchain with Python

## In this Colab notebook, the intention is to develop a simple Blockchain with Python, to understand how a Block is created, how a chain works and the importance of the hash within the Blockchain. I made comments almost in each line of code to be understandable to everybody. 

### We're going to use Colab for the development of the code in Python and Postman to get some request we're going to send from Colab with Flask. 

- For more information about Postman: https://www.postman.com/
- For more information about Flask: https://flask.palletsprojects.com/en/2.2.x/

### The project is divided in 3 steps: 

1. Build the Blockchain.
2. Mine the Blockchain to let the new blocks be added.
3. Run the app to recieve the results. 

### Build the Blockchain.

Each Block is going to have the next attributes: 

 ```def create_block(self, proof, previous_hash):             
      block = {'index': len(self.chain) + 1,
               'timestamp': str(datetime.datetime.now()), 
               'proof': proof,
               'previous_hash': previous_hash}

Where:

- Index: The number of the block.
- Time Stamp: The moment of the creation of the block. 
- Proof: We're going to use Proof of Work (PoW) to mine the block.
- Previous Hash: The hash of the last block. 

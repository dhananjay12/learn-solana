## Run
* tell the Solana CLI that we want to use a local cluster.
```
solana config set --url localhost
```

* Now we can create a new CLI Keypair. We will use this for interacting with our local cluster.
```
solana-keygen new
```
* Next step is to start our local cluster. Note, you may need to do some system config and possibly restart your machine to get the local cluster working. Type the following command into the terminal. If you still have the solana local validator running from the setup instructions, then you don’t need to run this command
```
solana-test-validator
```
* Build the program
```
cargo build-bpf --manifest-path=./Cargo.toml --bpf-out-dir=dist/program
```
* Deploy the program
```
solana program deploy dist/program/token_program.so
```
* Run client
If you aren’t running a local validator and are deploying to the public Devnet, please replace the ‘http://127.0.0.1:8899’ string in the getRpcUrl() function with ‘https://api.devnet.solana.com’ in utils.js
```
npm run start
```
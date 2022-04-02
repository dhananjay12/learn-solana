## Install anchor

https://project-serum.github.io/anchor/getting-started/installation.html#install-anchor

```
 npm i -g @project-serum/anchor-cli

cargo install --git https://github.com/project-serum/anchor --tag v0.23.0 anchor-cli --locked

anchor --version
```

Folder structure was created using (dont have to do it here)
```
anchor init gm-anchor
cd gm-anchor
```

## Run Setup
* tell the Solana CLI that we want to use a local cluster.
```
solana config set --url localhost
```
and then
```
solana-test-validator
```

Now we can create a new CLI Keypair. We will use this for interacting with our local cluster.

```
solana-keygen new -o id.json
```

Now that we have a new keypair, lets use the Solana airdrop program to retrieve some lamports that we can use to pay for transaction fees:

```
solana airdrop 2 $(solana-keygen pubkey ./id.json)
```

## Build and Deploy

```
anchor build
```

Now that the program has been built, we need to extract the generated program ID and insert it back into the ‘declare_id’ line in the Rust program. We can obtain the program ID using the following command:

```
solana address -k ./target/deploy/gm_anchor-keypair.json
```

Copy the program ID and paste it into the lib.rs program, replacing the string in the ‘declare_id’ line near the top of the program. 
For example
```
declare_id!("75PsQyHnFLhmF1jb4m31f2Gt35HFou3vJsaBCVAhYKAo");
```

build again

```
anchor build
```

Now we can deploy the program to the local cluster, using the following commands:

```
anchor deploy
```

## Running client

Anchor requires a couple of environment variables set to interact with deployed programs. Set the following environment variables on your terminal, to tell Anchor to use your previously created wallet account.
```
export ANCHOR_WALLET='../id.json'
export ANCHOR_PROVIDER_URL='http://127.0.0.1:8899'
```

You can run the client with the following command, passing in the program parameter, as well as the create action, then you can choose whatever you want for the post title and contents. This will create a new post for the specified post account that gets created:

```
cd app

node client.js --program $(solana address -k ../target/deploy/solana_social-keypair.json) --action create --title "this is a title" --content "this is the content for the social media post"
```

Now that you’ve created a post, you can now run the client again with the `update` action to update the post. Be sure to put different values this time for the post title and contents. For the `post` parameter, you need to enter the postAccount public key that was outputted to the console in the previous step. This is so that we updated the correct account that was populated previously.

```
node client.js --program $(solana address -k ../target/deploy/solana_social-keypair.json) --action update --title "this is a new title" --content "I have updated the post contents" --post <insert acct from previous tx>
```
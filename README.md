# Setup

Install `node`, `npm`, `rust`, `solana`.

## Install Rust
```
curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh
```
Restart terminal and check version.
```
 rustc --version
```

## Install Solana

```
sh -c "$(curl -sSfL https://release.solana.com/stable/install)"
```

Make sure to restart terminal. Refres bash profile if needed `source ~/.bash_profile` or run the following 
```
export PATH="/Users/dhananjay/.local/share/solana/install/active_release/bin:$PATH"
```
Check version
```
solana --version
```

## Run Solana local validator

```
solana config set --url localhost

solana-test-validator
```

## Test your setup

Enter the following command into the terminal to set your Solana provider URL to the Devnet cluster

```
solana config set --url https://api.devnet.solana.com
```

Generate a new keypair account. When promoted for a password, you can enter one, or leave it blank and press enter.

```
solana-keygen new --force
```

Now that you’ve created an account, you can use the airdrop program to obtain some SOL tokens.

```
solana airdrop 2
```
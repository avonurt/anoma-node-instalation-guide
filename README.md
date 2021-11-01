# anoma-node-instalation-guide DRAFT

Link to the official documentation: https://docs.anoma.network/v0.2.0/index.html

Here are the list of steps that were executed on `Ubuntu 20.04` version to run Anoma node

## Step 1 - install all needed packages

`sudo apt update && sudo apt upgrade -y`

`sudo apt install make clang pkg-config libssl-dev libclang-dev build-essential git curl ntp jq llvm tmux`

## Step 2 - install Rust

`curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh`

`source $HOME/.cargo/env`

## Step 3 - clone anoma repository

`cd $HOME`

`git clone https://github.com/anoma/anoma.git`

## Step 4 - checkout to the needed Anoma version

You should enter `anoma` folder using following command:

`cd $HOME/anoma`

When you are in the `anoma` folder you should execute following command:

`git checkout v0.2.0`

## Step 5 - copy `wasm` folder to the `$HOME` direcory 

`cp -a $HOME/anoma/wasm $HOME/wasm`

## Step 6 - install Anoma from the source

It is better to execute instalation in the seperate session, because it is take time. You could use `tmux` to create seperate session using following command: 

`tmux new -s session1`

When you are in the new session please enter `anoma` folder: 

`cd $HOME/anoma`

And execute the install process: 

`make install`

Wait for the instalation to complete.

## Step 7 - configure your node to join the Feigenbaum public testnet

`cd $HOME`

`anoma client utils join-network --chain-id=anoma-feigenbaum-0.ebb9e9f9013`

## Step 8 - generate new key in the wallet

`anoma wallet key gen --alias my-key`

## Step 9 - start a local Anoma ledger node

It is better to start it in the separate session or using systemd. In this example I will use `tmux`.

`tmux new -s anoma`

`anoma ledger`

Wait for the node to be synced

## Step 10 - Initialize an account

`anoma client init-account --alias my-new-acc --public-key my-key --source my-key`

After successful execution you should see something like this:

`The transaction initialized 1 new account
Added alias my-new-acc for address atest1kjdslahfaksjdhfajdhfkjadshfjkdfakjdhfakjlakdhfjhakdjhadkjfhaksdfh'

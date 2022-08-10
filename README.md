
# Data analytics 101 on Solana

Repo for getting started on fetching data from Solana using solana-py.

## Getting started

1. Install:

- node version 14+
- Rust:
  - Make sure you can run ```rustup --version```

- Solana tool suite [(link)](https://docs.solana.com/cli/install-solana-cli-tools) for running a Solana chain locally 
  - Make sure you can run ```solana --version```

If you are on Windows, it's slightly more tricky as you need to run rust and solana under WSDL. I use Ubuntu 20.04 as distro.

2. Start locally


- Set Solana to work locally: 
```solana config set --url localhost```
- Generate a keypair 
``` solana-keygen pubkey ```

- Start local Solana cluster with one test validator

```
$ solana-test-validator
[...]
JSON RPC URL: http://127.0.0.1:8899
⠈ 16:49:04 | Processed Slot: 76241 | Confirmed Slot: 76241 | Finalized Slot: 76209 | Full Snapshot Slot: 76201 | Incre
```

- (optional) In another terminal, type ```solana logs``` for watching the transaction logs.
- Build/deploy the program

```
# build
npm run build:program-rust
# deploy
solana program deploy dist/program/helloworld.so
```

Excellent. Now we have deployed the program and can interact with it using a client. There are multiple flavors of the RPC client (JS, Python, etc), we use the JS version for convenience.

- Head over to ```src/client/main.ts```. The ```main``` method fetches keys and program location and, most importantly, sends a hello to two accounts we pre-defined. We will later on retrieve the number of hellos sent to each account (Data Analytics!).

- Send a hello to 2 accounts: 
```
$ cd /path/to/repo/root
$ npm start
Let's say hello to a Solana account...
Connection to cluster established: http://localhost:8899 { 'feature-set': 483097211, 'solana-core': '1.10.35' }
Using account 9tSZAwG5nAEmkq2M4WEhceEpWNMmKmh6JsGS4X4hHPTj containing 499999999.3671693 SOL to pay for fees
programId GcUtT2NrSk8TT3zVM4tvGvTwDgo7gnA7esXo4RKUfzWj
Using program GcUtT2NrSk8TT3zVM4tvGvTwDgo7gnA7esXo4RKUfzWj
Saying hello to 2bt1NMJds5g4W1LwAeoVsMcUSa9qPD2PywAapBuLnpZw
Saying hello to 97j9kXnLJsGcz6Nxu96rN5S6AEqhrkmuYqsWH1nmW632
2bt1NMJds5g4W1LwAeoVsMcUSa9qPD2PywAapBuLnpZw has been greeted 1 time(s)
Success
```

Nice, so each account has been properly initialized and is able to store hellos. Moreover, we already sent them 1.
Now we can finally start fetching data.

- Initialize a new python environment (I use [Miniconda](https://docs.conda.io/en/latest/miniconda.html))
  - If you have Miniconda installed, simply create an environment using ```conda env create -f environment.yml```
  - Otherwise you need to create an environment manually and install the dependencies stated in the enviroment file).

- Now head over to the [notebook](local-solana-data-analysis.ipynb) for fetching the data.

## Comments on tooling

Feel free to check out this [notebook](tools-overview.ipynb) for some suggestions on data fetching of oracles.


==================================================================

Thanks to https://kirima.vercel.app/post/gentleintrosolana for an excellent head start.
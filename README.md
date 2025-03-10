<div align="center">

# **Bittensor** <!-- omit in toc -->
[![Discord Chat](https://img.shields.io/discord/308323056592486420.svg)](https://discord.gg/bittensor)
[![PyPI version](https://badge.fury.io/py/bittensor.svg)](https://badge.fury.io/py/bittensor)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT) 

---

### Internet-scale Neural Networks <!-- omit in toc -->

[Discord]([https://discord.gg/bittensor](https://discord.gg/qasY3HA9F9) • [Network](https://taostats.io/) • [Research](https://bittensor.com/whitepaper)

</div>

Bittensor is a mining network, similar to Bitcoin, that includes built-in incentives designed to encourage computers to provide access to machine learning models in an efficient and censorship-resistant manner. These models can be queried by users seeking outputs from the network, for instance; generating text, audio, and images, or for extracting numerical representations of these input types. Under the hood, Bittensor’s *economic market*, is facilitated by a blockchain token mechanism, through which producers (***miners***) and the verification of the work done by those miners (***validators***) are rewarded. Miners host, train or otherwise procure machine learning systems into the network as a means of fulfilling the verification problems defined by the validators, like the ability to generate responses from prompts i.e. “What is the capital of Texas?. 

The token based mechanism under which the miners are incentivized ensures that they are constantly driven to make their knowledge output more useful, in terms of speed, intelligence and diversity. The value generated by the network is distributed directly to the individuals producing that value, without intermediaries. Anyone can participate in this endeavour, extract value from the network, and govern Bittensor. The network is open to all participants, and no individual or group has full control over what is learned, who can profit from it, or who can access it.

To learn more about Bittensor, please read our [paper](https://bittensor.com/whitepaper).

# Install
There are three ways to install Bittensor

1. Through the installer:
```bash
$ /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/opentensor/bittensor/master/scripts/install.sh)"
```
2. With pip:
```bash
$ pip3 install bittensor
```
3. From source:
```bash
$ git clone https://github.com/opentensor/bittensor.git
$ python3 -m pip install -e bittensor/
```
4. Using Conda (recommended for **Apple M1**):
```bash
$ conda env create -f ~/.bittensor/bittensor/scripts/environments/apple_m1_environment.yml
$ conda activate bittensor
```

To test your installation, type:
```bash
$ btcli --help
```
or using python
```python
import bittensor
```

#### CUDA
If you anticipate using PoW registration for subnets or the faucet (only available on staging), please install `cubit` as well for your version of python. You can find the Opentensor cubit implementation and instructions [here](https://github.com/opentensor/cubit).

For example with python 3.10:
```bash
pip install https://github.com/opentensor/cubit/releases/download/v1.1.2/cubit-1.1.2-cp310-cp310-linux_x86_64.whl
```

# Wallets 

Wallets are the core ownership and identity technology around which all functions on Bittensor are carried out. Bittensor wallets consists of a coldkey and hotkey where the coldkey may contain many hotkeys, while each hotkey can only belong to a single coldkey. Coldkeys store funds securely, and operate functions such as transfers and staking, while hotkeys are used for all online operations such as signing queries, running miners and validating. 

Wallets can be created in two ways.
1. Using the python-api
```python
import bittensor
wallet = bittensor.wallet()
wallet.create_new_coldkey()
wallet.create_new_hotkey()
print (wallet)
"Wallet (default, default, ~/.bittensor/wallets/)"
```
2. Or using btcli
> Use the subcommand `wallet` or it's alias `w`:
```bash
$ btcli wallet new_coldkey
    Enter wallet name (default):      

    IMPORTANT: Store this mnemonic in a secure (preferably offline place), as anyone who has possession of this mnemonic can use it to regenerate the key and access your tokens. 
    The mnemonic to the new coldkey is:
    **** *** **** **** ***** **** *** **** **** **** ***** *****
    You can use the mnemonic to recreate the key in case it gets lost. The command to use to regenerate the key using this mnemonic is:
    btcli w regen_coldkey --mnemonic post maid erode shy captain verify scan shoulder brisk mountain pelican elbow

$ btcli wallet new_hotkey
    Enter wallet name (default): d1
    Enter hotkey name (default): 

    IMPORTANT: Store this mnemonic in a secure (preferably offline place), as anyone who has possession of this mnemonic can use it to regenerate the key and access your tokens. 
    The mnemonic to the new hotkey is:
    **** *** **** **** ***** **** *** **** **** **** ***** *****
    You can use the mnemonic to recreate the key in case it gets lost. The command to use to regenerate the key using this mnemonic is:
    btcli w regen_hotkey --mnemonic total steak hour bird hedgehog trim timber can friend dry worry text
```
In both cases you should be able to view your keys by navigating to ~/.bittensor/wallets or viewed by running ```btcli wallet list```
```bash
$ tree ~/.bittensor/
    .bittensor/                 # Bittensor, root directory.
        wallets/                # The folder containing all bittensor wallets.
            default/            # The name of your wallet, "default"
                coldkey         # You encrypted coldkey.
                coldkeypub.txt  # Your coldkey public address
                hotkeys/        # The folder containing all of your hotkeys.
                    default     # You unencrypted hotkey information.
```
Your default wallet ```Wallet (default, default, ~/.bittensor/wallets/)``` is always used unless you specify otherwise. Be sure to store your mnemonics safely. If you lose your password to your wallet, or the access to the machine where the wallet is stored, you can always regenerate the coldkey using the mnemonic you saved from above. 
```bash
$ btcli wallet regen_coldkey --mnemonic **** *** **** **** ***** **** *** **** **** **** ***** *****
```

## Using the cli
The Bittensor command line interface (`btcli`) is the primary command line tool for interacting with the Bittensor network. It can be used to deploy nodes, manage wallets, stake/unstake, nominate, transfer tokens, and more.

### Basic Usage

To get the list of all the available commands and their descriptions, you can use:

```bash
btcli --help

usage: btcli <command> <command args>

bittensor cli v{bittensor.__version__}

commands:
  subnets (s, subnet) - Commands for managing and viewing subnetworks.
  root (r, roots) - Commands for managing and viewing the root network.
  wallet (w, wallets) - Commands for managing and viewing wallets.
  stake (st, stakes) - Commands for staking and removing stake from hotkey accounts.
  sudo (su, sudos) - Commands for subnet management.
  legacy (l) - Miscellaneous commands.
```

### Example Commands

#### Viewing Senate Proposals
```bash
btcli root proposals
```

#### Viewing Senate Members
```bash
btcli root list_delegates
```

#### Viewing Proposal Votes
```bash
btcli root senate_vote --proposal=[PROPOSAL_HASH]
```

#### Registering for Senate
```bash
btcli root register
```

#### Leaving Senate
```bash
btcli root undelegate
```

#### Voting in Senate
```bash
btcli root senate_vote --proposal=[PROPOSAL_HASH]
```

#### Miscellaneous Commands
```bash
btcli legacy update
btcli legacy faucet
```

#### Managing Subnets
```bash
btcli subnets list
btcli subnets create
```

#### Managing Wallets
```bash
btcli wallet list
btcli wallet transfer
```

### Note

Please replace the subcommands and arguments as necessary to suit your needs, and always refer to `btcli --help` or `btcli <command> --help` for the most up-to-date and accurate information.

For example:
```bash
btcli subnets --help

usage: btcli <command> <command args> subnets [-h] {list,metagraph,lock_cost,create,register,pow_register,hyperparameters} ...

positional arguments:
  {list,metagraph,lock_cost,create,register,pow_register,hyperparameters}
                        Commands for managing and viewing subnetworks.
    list                List all subnets on the network.
    metagraph           View a subnet metagraph information.
    lock_cost           Return the lock cost to register a subnet.
    create              Create a new bittensor subnetwork on this chain.
    register            Register a wallet to a network.
    pow_register        Register a wallet to a network using PoW.
    hyperparameters     View subnet hyperparameters.

options:
  -h, --help            show this help message and exit
```

### Post-Installation Steps

To enable autocompletion for Bittensor CLI, run the following commands:

```bash
btcli --print-completion bash >> ~/.bashrc  # For Bash
btcli --print-completion zsh >> ~/.zshrc    # For Zsh
source ~/.bashrc  # Reload Bash configuration to take effect
```

# The Bittensor Package
The bittensor package contains data structures for interacting with the bittensor ecosystem, writing miners, validators and querying the network. Additionally, it provides many utilities for efficient serialization of Tensors over the wire, performing data analysis of the network, and other useful utilities.

Wallet: Interface over locally stored bittensor hot + coldkey styled wallets. 
```python
import bittensor
# Bittensor's wallet maintenance class.
wallet = bittensor.wallet() 
# Access the hotkey
wallet.hotkey 
# Access the coldkey
wallet.coldkey ( requires decryption )
# Sign data with the keypair.
wallet.coldkey.sign( data )

```

Subtensor: Interfaces with bittensor's blockchain and can perform operations like extracting state information or sending transactions.
```python
import bittensor
# Bittensor's chain interface.
subtensor = bittensor.subtensor() 
# Get the chain block
subtensor.get_current_block()
# Transfer Tao to a destination address.
subtensor.transfer( wallet = wallet, dest = "xxxxxxx..xxxxx", amount = 10.0)
# Register a wallet onto a subnetwork
subtensor.register( wallet = wallet, netuid = 1 )
```

Metagraph: Encapsulates the chain state of a particular subnetwork at a specific block.
```python
import bittensor
# Bittensor's chain state object.
metagraph = bittensor.metagraph( netuid = 1 ) 
# Resync the graph with the most recent chain state
metagraph.sync()
# Get the list of stake values
print ( metagraph.S )
# Get endpoint information for the entire subnetwork
print ( metagraph.axons )
# Get the hotkey information for the miner in the 10th slot
print ( metagraph.hotkeys[ 10 ] )
# Sync the metagraph at another block
metagraph.sync( block = 100000 )
# Save the metagraph
metagraph.save()
# Load the same
metagraph.load()
```

Synapse: Responsible for defining the protocol definition between axon servers and dendrite clients
```python
class Topk( bittensor.Synapse ):
    topk: int = 2  # Number of "top" elements to select
    input: bittensor.Tensor = pydantic.Field(..., allow_mutation=False)  # Ensure that input cannot be set on the server side. 
    v: bittensor.Tensor = None
    i: bittensor.Tensor = None

def topk( synapse: Topk ) -> Topk:
    v, i = torch.topk( synapse.input.deserialize(), k = synapse.topk ) 
    synapse.v = bittensor.Tensor.serialize( v )
    synapse.i = bittensor.Tensor.serialize( i )
    return synapse

# Attach the forward function to the axon and start.
axon = bittensor.axon().attach( topk ).start()
```

Axon: Serves Synapse protocols with custom blacklist, priority and verify functions.

```python
import bittensor

class MySynapse( bittensor.Synapse ):
    input: int = 1
    output: int = None

# Define a custom request forwarding function
def forward( synapse: MySynapse ) -> MySynapse:
    # Apply custom logic to synapse and return it
    synapse.output = 2
    return synapse

# Define a custom request verification function
def verify_my_synapse( synapse: MySynapse ):
    # Apply custom verification logic to synapse
    # Optionally raise Exception

# Define a custom request blacklist function
def blacklist_my_synapse( synapse: MySynapse ) -> bool:
    # Apply custom blacklist 
    # return False ( if non blacklisted ) or True ( if blacklisted )

# Define a custom request priority function
def prioritize_my_synape( synapse: MySynapse ) -> float:
    # Apply custom priority
    return 1.0 

# Initialize Axon object with a custom configuration
my_axon = bittensor.axon(config=my_config, wallet=my_wallet, port=9090, ip="192.0.2.0", external_ip="203.0.113.0", external_port=7070)

# Attach the endpoint with the specified verification and forwarding functions  
my_axon.attach(
    forward_fn = forward_my_synapse, 
    verify_fn=verify_my_synapse,
    blacklist_fn = blacklist_my_synapse,
    priority_fn = prioritize_my_synape
).start()
```     

Dendrite: Inheriting from PyTorch's Module class, represents the abstracted implementation of a network client module designed 
to send requests to those endpoints to receive inputs.

Example:
```python
dendrite_obj = dendrite( wallet = bittensor.wallet() )
# pings the axon endpoint
await d( <axon> )
# ping multiple axon endpoints
await d( [<axons>] ) 
# Send custom synapse request to axon.
await d( bittensor.axon(), bittensor.Synapse() ) 
# Query all metagraph objects.
await d( meta.axons, bittensor.Synapse() ) 
```

## Setting weights on root network
Use the `root` subcommand to access setting weights on the network across subnets.

```bash
btcli root weights --wallet.name <coldname> --wallet.hotkey <hotname>
Enter netuids (e.g. 0, 1, 2 ...):
# Here enter your selected netuids to set weights on
1, 2

>Enter weights (e.g. 0.09, 0.09, 0.09 ...): 
# These do not need to sum to 1, we do normalization on the backend.
# Values must be > 0
0.5, 10

Normalized weights: 
        tensor([ 0.5000, 10.0000]) -> tensor([0.0476, 0.9524])

Do you want to set the following root weights?:
  weights: tensor([0.0476, 0.9524])
  uids: tensor([1, 2])? [y/n]: 
y

⠏ 📡 Setting root weights on test ...
```

## Release
The release manager should follow the instructions of the [RELEASE_GUIDELINES.md](./RELEASE_GUIDELINES.md) document.

## Contributions
Please review the [contributing guide](./contrib/CONTRIBUTING.md) for more information before making a pull request.

## License
The MIT License (MIT)
Copyright © 2021 Yuma Rao

Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the “Software”), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED “AS IS”, WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.


## Acknowledgments
**learning-at-home/hivemind**

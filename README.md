# Model DAS
Model DAS is a repository, forked from [DAS Prototype](https://github.com/ChainSafe/das-prototype), that aims to model and benchmark a possible solution to the [Data Availability Sampling Networking Problem](https://github.com/ethereum/requests-for-proposals/blob/master/open-rfps/das.md) through [Discovery v5 overlay subnetworks](https://notes.ethereum.org/@pipermerriam/B1SS-nhad).

I'm currently working on implementing the networking stack needed to create a Secure K-DHT discv5 overlay to support Data Availability Sampling.  Concepts from [DAS Playground](https://github.com/EchoAlice/das-playground) are going to be implemnted here.

Check out Model DAS's [Project Proposal](https://hackmd.io/@nWQbi7_nQnWPS0Xt_GbOVQ/HyHiEpD8j).



# Original Readme:
-------------------------------------------------------------------------
This repo contains various prototypes of the core DAS components - dissemination and random sampling.

## Usage

`cargo run -- -n <num-servers> -p <start-listen-port> -t <topology> [simulation-case] [ARGS]`

This will spin up `num-servers` of discv5 servers starting at port `start-listen-port` all the way to `start-listen-port` + `num-servers`, and then start `simulation-case`.

### Disseminate

```bash
cargo run -- -n 500 --topology uniform disseminate -n 256 --batching-strategy 'bucket-wise' --forward-mode 'FA' --replicate-mode 'RS' --redundancy 1
```

### Sample

```bash
cargo run -- -n 500 -t uniform --timeout 6 sample --validators-number 2 --samples-per-validator 75 --parallelism 30
```

### Use snapshots
Snapshots allow saving network configurations along with various RNG seeds to have more consistent measurements and for debugging. Use `--snapshot` flag with values `new`, `last`, and specific timecode eg. `2022-11-08-11:46:09`. Snapshots are saved in `--cache-dir` folder default value = `./data`.

```bash
cargo run -- -n 500 --topology uniform --snapshot last disseminate -n 256
```

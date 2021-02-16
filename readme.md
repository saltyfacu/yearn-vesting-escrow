# Yearn Vesting Escrow

A modified version of [Curve Vesting Escrow](https://github.com/curvefi/curve-dao-contracts) contracts with added functionality:
- An escrow can have a `start_date` in the past.
- The first unlock can be delayed using `cliff_length`.
- An ability to `claim` partial amounts or use a different beneficiary account.
- An ability to terminate an escrow and clawback all the unvested tokens using `rug_pull`. The recipient is still entitled to the vested portion.
- Factory admin controls removed, anyone can deploy escrows, funds are pulled instead of pushed.
- Factory emits an event which allows finding all the escrows deployed from it.

## Contracts

- [`VestingEscrowFactory`](contracts/VestingEscrowFactory.vy): Factory to deploy many simplified vesting contracts
- [`VestingEscrowSimple`](contracts/VestingEscrowSimple.vy): Simplified vesting contract that holds tokens for a single beneficiary

## Usage

```python
$ brownie console --network mainnet
funder = accounts.load(name)
factory = VestingEscrowFactory.at('0xF124534bfa6Ac7b89483B401B4115Ec0d27cad6A', owner=funder)
factory.deploy_vesting_contract(token, recipient, amount, vesting_duration, vesting_start, cliff_length)
```

## Ethereum mainnet deployment

- `VestingEscrowFactory`: [0xF124534bfa6Ac7b89483B401B4115Ec0d27cad6A](https://etherscan.io/address/0xF124534bfa6Ac7b89483B401B4115Ec0d27cad6A#code)
- `VestingEscrowSimple`: [0x9c351CabC5d9e1393678d221F84E6EE3D05c016F](https://etherscan.io/address/0x9c351cabc5d9e1393678d221f84e6ee3d05c016f#code)

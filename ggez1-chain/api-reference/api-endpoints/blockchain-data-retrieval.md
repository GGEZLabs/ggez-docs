# Blockchain Data Retrieval

## **Supply**

[https://rest.ggez.one/cosmos/bank/v1beta1/supply](https://rest.ggez.one/cosmos/bank/v1beta1/supply)

## **Circulating supply**

[https://node.ggez.one/ggezchain/supply?metric=circulating\_supply](https://node.ggez.one/ggezchain/supply?metric=circulating_supply)

## **Bonded supply**

[https://node.ggez.one/ggezchain/supply?metric=bonded\_supply](https://node.ggez.one/ggezchain/supply?metric=bonded_supply)

## **Obtain Block Information by Block Height**

[https://rest.ggez.one/cosmos/base/tendermint/v1beta1/blocks/{height}](https://rest.ggez.one/cosmos/base/tendermint/v1beta1/blocks/%7Bheight%7D)

**Example:**\
[https://rest.ggez.one/cosmos/base/tendermint/v1beta1/blocks/200000](https://rest.ggez.one/cosmos/base/tendermint/v1beta1/blocks/200000)

## **Obtain Transaction Details by TXID**

[https://rest.ggez.one/cosmos/tx/v1beta1/txs/{hash}](https://rest.ggez.one/cosmos/tx/v1beta1/txs/A5A36246D74C08C214CF182FF4F7AD3E6CB24CE07CE597EAD52BE716B93FEB34)

**Example:**\
[https://rest.ggez.one/cosmos/tx/v1beta1/txs/A5A36246D74C08C214CF182FF4F7AD3E6CB24CE07CE597EAD52BE716B93FEB34](https://rest.ggez.one/cosmos/tx/v1beta1/txs/A5A36246D74C08C214CF182FF4F7AD3E6CB24CE07CE597EAD52BE716B93FEB34)

## **Obtain Address Balance:**

### Get balance:

[https://rest.ggez.one/cosmos/bank/v1beta1/balances/{address}](https://rest.ggez.one/cosmos/bank/v1beta1/balances/%7Baddress%7D)

**Example:**\
[https://rest.ggez.one/cosmos/bank/v1beta1/balances/ggez1u7374gx6efl39vsd6mhwn0pw7nhwzqtfjumkfh](https://rest.ggez.one/cosmos/bank/v1beta1/balances/ggez1u7374gx6efl39vsd6mhwn0pw7nhwzqtfjumkfh)

### Get balance by denom:

[https://rest.ggez.one/cosmos/bank/v1beta1/balances/{address}/by\_denom?denom=uggez1](https://rest.ggez.one/cosmos/bank/v1beta1/balances/%7Baddress%7D/by_denom?denom=uggez1)

**Example:**\
[https://rest.ggez.one/cosmos/bank/v1beta1/balances/ggez1u7374gx6efl39vsd6mhwn0pw7nhwzqtfjumkfh/by\_denom?denom=uggez1](https://rest.ggez.one/cosmos/bank/v1beta1/balances/ggez1u7374gx6efl39vsd6mhwn0pw7nhwzqtfjumkfh/by_denom?denom=uggez1)

### Get spendable balance:

[https://rest.ggez.one/cosmos/bank/v1beta1/spendable\_balances/{address}](https://rest.ggez.one/cosmos/bank/v1beta1/spendable_balances/%7Baddress%7D)

**Example:** [https://rest.ggez.one/cosmos/bank/v1beta1/spendable\_balances/ggez1u7374gx6efl39vsd6mhwn0pw7nhwzqtfjumkfh](https://rest.ggez.one/cosmos/bank/v1beta1/spendable_balances/ggez1u7374gx6efl39vsd6mhwn0pw7nhwzqtfjumkfh)

### Get spendable balance by denom:

[https://rest.ggez.one/cosmos/bank/v1beta1/spendable\_balances/{address}/by\_denom?denom=uggez1](https://rest.ggez.one/cosmos/bank/v1beta1/spendable_balances/%7Baddress%7D/by_denom?denom=uggez1)

**Example :** [https://rest.ggez.one/cosmos/bank/v1beta1/spendable\_balances/ggez1u7374gx6efl39vsd6mhwn0pw7nhwzqtfjumkfh/by\_denom?denom=uggez1](https://rest.ggez.one/cosmos/bank/v1beta1/spendable_balances/ggez1u7374gx6efl39vsd6mhwn0pw7nhwzqtfjumkfh/by_denom?denom=uggez1)

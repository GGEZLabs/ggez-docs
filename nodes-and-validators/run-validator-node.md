# Run Validator Node

Before setting up a validator node, make sure to have completed the [Node Setup](node-setup.md) guide.

## Create Account

We will create an account to control the validator

```
ggezchaind keys add account_name
```

If you have already have an account add `--recover` flag to previous command

{% hint style="info" %}
Activate the account by sending tokens to it.
{% endhint %}

## Create Validator

create a `validator.json` file:

```
{
  "pubkey": {
    "@type": "/cosmos.crypto.ed25519.PubKey",
    "key": "Pc1g/vSn3nT1BA/R6FdfAjlze1WBkU6IaAaNzB92ckw="
  },
  "amount": "<amount>uggez1",
  "moniker": "myvalidator",
  "website": "https://validator_website",
  "commission-rate": "0.1",
  "commission-max-rate": "0.2",
  "commission-max-change-rate": "0.01",
  "min-self-delegation": "1"
}
```

Now to create the validator.

```
ggezchaind tx staking create-validator path/to/validator.json --from account_name --gas auto --gas-prices 0.4uggez1 --gas-adjustment 1.5
```

Now if transaction processed successfully you can check your validator if it accepted.

```
ggezchaind q staking validators
```

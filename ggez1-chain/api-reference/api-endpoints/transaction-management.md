# Transaction Management

**Broadcast / Transaction Transmission API:** [https://bc.ggez.one:8443/broadcast\_tx\_asyn](https://bc.ggez.one:8443/broadcast_tx_asyn)

**Transaction Fee Calculation:** tx\_fee= gas\_limit\* gas\_price

**Conversion Rate of Transaction Units with the Main Unit:**\
1 GGEZ1 = 1,000 MGGEZ = 1,000,000 UGGEZ1

**Transaction Success Validation Criteria:**\
Based on Response Code, if code is 0 then transaction is successful.

**Memo/Tag Support:** Yes

## Send Token Example

Send token using Keplr wallet.

**@cosmjs/stargate** and **@keplr-wallet/types** packages required to complete transaction.\
Also chain info file:\
[https://github.com/chainapsis/keplr-chain-registry/blob/main/cosmos/ggezchain.json](https://github.com/chainapsis/keplr-chain-registry/blob/main/cosmos/ggezchain.json)

{% code overflow="wrap" lineNumbers="true" fullWidth="false" %}
````typescript
```typescript
import { ChainInfo } from "./chainInfo";
import { Coin, SigningStargateClient, StdFee } from "@cosmjs/stargate";
import { Window as KeplrWindow } from "@keplr-wallet/types";

declare global {
  interface Window extends KeplrWindow {}
}

export async function sendTokenExample() {
  const { keplr } = window;

  if (!keplr) {
    return { error: "You need to install Keplr" };
  }

  try {
    await keplr.experimentalSuggestChain(ChainInfo);
    await keplr.enable(ChainInfo.chainId);

    const offlineSigner = keplr.getOfflineSigner!(ChainInfo.chainId);
    if (!offlineSigner) {
      return { error: "Error while getting offlineSigner" };
    }

    const signerAddress = (await offlineSigner.getAccounts())[0].address;

    const client = await SigningStargateClient.connectWithSigner(
      '"wss://bc.ggez.one:26657"',
      offlineSigner
    );
    const toAddress = "ggez1u7374gx6efl39vsd6mhwn0pw7nhwzqtfjumkfh";
    const amount: Coin[] = [
      {
        amount: "1000000", // 1000000 uggez1 = 1 GGEZ
        denom: "uggez1",
      },
    ];
    const fee: StdFee = {
      amount: [
        {
          amount: "100000", // Fee = gas * gas_price = 200000 * 0.5
          denom: "uggez1",
        },
      ],
      gas: "200000",
    };
    const memo = "Add memo here"; // It is optional
    const response = await client.sendTokens(
      signerAddress,
      toAddress,
      amount,
      fee,
      memo
    );
    // If code equal 0 transaction should be successful
    if (response.code === 0) {
      console.log("Successful Transaction");
    } else {
      console.log(`Error: ${response.rawLog}`);
    }
  } catch (error) {
    console.error(error);
  }
}

```
````
{% endcode %}

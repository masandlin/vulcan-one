# Vulcan ONE API

Vulcan ONE API is a Go project that provides dynamic handling of API endpoints for Ethereum-related functionalities, such as ERC-20, ERC-721, and ERC-1155 token operations. The API allows users to create webhooks on EVM compatible chain on standardized contracts by specifying the desired contract standard, amount, and address in the API call.

[![codecov](https://codecov.io/gh/FN00EU/vulcan-one/graph/badge.svg?token=5R7OPZNYHH)](https://codecov.io/gh/FN00EU/vulcan-one)
[![Go Report Card](https://goreportcard.com/badge/github.com/FN00EU/vulcan-one)](https://goreportcard.com/report/github.com/FN00EU/vulcan-one)

## Getting Started - Deploying without technical skills

- Fork this repository
- Edit configuration.json to add chain and RPC URLs you want to use, sort by priority first in list is being called as main, others are backup.
- Create account using GitHub on Container-as-a-Service provider, for example <https://www.back4app.com/>.
- Create Container-as-a-Service
![Screenshot of a selecting the container as a service on back4app](assets/back4app_caas.jpg)
- Give permissions and select the forked repository (note that the whale image is Docker logo, not a whale role on back4app)
![Screenshot of a selecting the container as a service on back4app](assets/back4app_selectrepository.jpg)
- Wait until the application builds, on the main dashboard on the left you will have Available and your URL, which you need to use for webhook calls. Or in Settings - Domain, you can add your domain or subdomain for free.
![Screenshot of a selecting the container as a service on back4app](assets/back4app_domain.jpg)

## Example use

### ERC721

For ERC721 compatible call with integer units are keywords "erc721" or "nft".

Specific example of having at least 2 Pudgy Penguins both examples are correct:

```
https://www.yourserverurl.com/api/eth/erc721/2/0xbd3531da5cf5857e7cfaa92426877b022e612cf8

https://www.yourserverurl.com/api/eth/nft/2/0xbd3531da5cf5857e7cfaa92426877b022e612cf8

```

### ERC20

Standards for ERC20 compatible call with integer units are keywords "erc20"
and "token", for better eading compatibility.

If you want to check amount of erc20 use only whole number.

```
yourserverurl/api/evmchainfromconfiguration/erc20/amount/contractaddress
```

Example for verification of 100 ROOT tokens on eth, decimals are not supported:

```
https://www.yourserverurl.com/api/eth/erc20/100/0xa3d4BEe77B05d4a0C943877558Ce21A763C4fa29
```

### ERC1155

For ERC1155 compatible call with integer units are keywords "erc1155" and "sft".

If you want to verify range of ERC1155 - at least 1 is needed for a role:

```
yourserverurl/api/evmchainfromconfiguration/erc1155/idstart-idend/contractaddress
```

If you want to verify exact amount of ERC1155 token id:

```
yourserverurl/api/evmchainfromconfiguration/erc1155/id_balance/contractaddress
```

If you want to verify multiple amounts of multiple ERC1155 token id:

```
yourserverurl/api/evmchainfromconfiguration/erc1155/id1_balance1&id2_balance2/contractaddress
```

### How to configure Vulcan webhook

- Choose Custom Webhook on your server, you need already prepared role in Discord server, as you can't create role from Vulcan UI

![Screenshot of a Vulcan UI filled in for a custom webhook](assets/vulcan_customwebhook.jpg)

- Add new role and paste the url to custom webhook in Vulcan admin based on examples provided
![Screenshot of a Vulcan UI filled in for a custom webhook](assets/adding_webhook.jpg)

## Cross Chain Collections

This feature is optional and it is counting balances accross multiple chains.
The configuration example for all of the multichain Lil Pudgies is:

```
"crossChainCollections":{
      "lilpudgy": {
        "arb":"0x611747CC4576aAb44f602a65dF3557150C214493",
        "bsc":"0x611747CC4576aAb44f602a65dF3557150C214493",
        "polygon":"0x611747CC4576aAb44f602a65dF3557150C214493",
        "eth":"0x524cab2ec69124574082676e6f654a18df49a048"
      }
    },
```

and the api call can be made with any of the matching "network":"contract" call:

**Both** examples will check balance of Lil Pudgy on all configured chains:

```
https://www.yourserverurl.com/api/arb/erc721/4/0x611747CC4576aAb44f602a65dF3557150C214493/x

https://www.yourserverurl.com/api/eth/erc721/4/0x524cab2ec69124574082676e6f654a18df49a048/x

```

### The Root Network FuturePass

Keep in mind, to use CrossChain addition the api call **must have trn selected**.

**Correct** example using trn in the api call for EOA and FuturePass address:

```
https://www.yourserverurl.com/api/trn/erc721/4/0xAaaAAAaa00000464000000000000000000000000/x
```

Incorrect example using other network than trn in the api call:

```
https://www.yourserverurl.com/api/eth/erc721/4/0x6bCa6de2dbDc4E0d41f7273011785ea16Ba47182/x
```

## Plan

- Increase test coverage
- Native support for - Substrate, ICP, Cosmos
- Improved logs and monitoring - Grafana

## Supporters

- New Blast City - <https://x.com/newblastcity>

## Support

If you use or like this tool, you can support it by:

- contributing as a developer
- donation on Ethereum or any EVM compatible chain: 0x3574060c34A9dA3bE20f4342Af6dB4F21Bc9c95E
- donation on The Root Network: 0xFFFfFfFF0000000000000000000000000000114e
- donating and requesting your specific chain to be added (contact me on X (@fn00eu)
for feasibility assessment of the chain being added)

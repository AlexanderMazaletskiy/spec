## Version upgrade changes

1. Implement the function of ERC721
   - Issuance of ERC721 property
   - Issuance of ERC721 Token
   - Transfer of ERC721 Token
   - Destruction of ERC721 Token
2. Add integration testing for ERC721
3. Add RPC interfaces for ERC721
4. Modify part of the RPC interface
5. Support all features of Bitcoin-ABC (v0.18.2)

## Warning

Due to changes of consensus rules in the `Bitcoin-ABC 0.18.2`, and Wormhole added support for the ERC721 protocol; all nodes must be forced to upgrade to the version `(0.2.0)`. At the same time, nodes below version 0.2.0 will no longer be supported, these nodes will not be able to provide accurate transaction and block information due to changes in consensus rules.

## Bitcoin-Abc compatible

The `Wormhole 0.2.0` node is compatible with the `Bitcoin-Abc 0.18.2` version. The Wormhole node can also be used as a Bitcoin-Abc node to support all functions of the Bitcoin-Abc node.

## Get the Wormhole node version

```
wormholed-cli whc_getinfo
{  
  "wormholeversion_int": 20000000,
  "wormholeversion": "0.2.0",
  "bitcoincoreversion": "0.18.2",
  "block": 1266612,
  "blocktime": 1541556523,
  "blocktransactions": 0,
  "totaltransactions": 5155,
  "alerts": [
  ]
}
```

Wormhole node version : `"wormholeversion": "0.2.0"`

Bitcoin-Abc version : `"bitcoincoreversion": "0.18.2"`

The Wormhole version released in this document is 0.2.0 and Bitcoin-ABC 0.18.2 is supported.

## How to upgrade

1. Download the code for version 0.2.0：https://github.com/copernet/wormhole/releases/tag/v0.2.0
2. Install, compile
   - Unix platform：https://github.com/copernet/wormhole/blob/master/doc/build-unix.md
   - OSX platform：https://github.com/copernet/wormhole/blob/master/doc/build-osx.md
   - Windows platform：https://github.com/copernet/wormhole/blob/master/doc/build-windows.md
3. Run the version 0.2.0 using the following command for the first time：`wormholed -startclean=1 -daemon`
4. Use the following command when the software is restarted the next time after the data synchronization is completed for version 0.2.0：`wormholed -daemon`

### Implement the function of ERC721

1. Newly added wormhole transaction type: `WHC_TYPE_ERC721 (9)`, identifies the ERC721 transaction.

2. Newly added enumeration type: `ERC721Action` , identifies the operations involved in the ERC721 transaction.

   - ```
     enum ERC721Action{
         ISSUE_ERC721_PROPERTY = 1,
         ISSUE_ERC721_TOKEN,
         TRANSFER_REC721_TOKEN,
         DESTROY_ERC721_TOKEN
     };
     ```

### ERC721 function enable height

Mainnet：555655

Testnet：1267112

Regtest：110

### Add integration testing for ERC721

Test execution steps：

```
1. precondition：The Wormhole project was successfully compiled
2. Enter the test directory：cd wormhole/test/functional
3. Run the test：./test_runner.py whc_erc721.py
```

### Add RPC interfaces for ERC721

See RPC's detailed explanation：https://github.com/copernet/spec/blob/master/wormhole-RPC.md

#### whc_issuanceERC721property

Description: Issuance of ERC721 property

#### whc_issuanceERC721Token

Description: Issuance of ERC721 Token

#### whc_transferERC721Token

Description: Transfer of ERC721 Token

#### whc_destroyERC721Token

Description: Destruction of ERC721 Token

#### whc_createpayload_issueERC721property

Description: Generate the payload data for create the ERC721 property

#### whc_createpayload_issueERC721token

Description: Generate the payload data for create the ERC721 token

#### whc_createpayload_transferERC721token

Description: Generate the payload data for transfer of ERC721 Token

#### whc_createpayload_destroyERC721token

Description: Generate the payload data for destruction of ERC721 Token

#### whc_getERC721PropertyNews

Description: Get the information of ERC721 property

#### whc_getERC721TokenNews

Description: Get the information of ERC721 Token

#### whc_getERC721AddressTokens

Description: Get Token in the specified address under the specified ERC asset

#### whc_getERC721PropertyDestroyTokens

Description: Get the destroyed ERC721 Tokens under the specified ERC721property

### Modify part of the RPC interface

#### whc_gettransaction

Description: Get information about wormhole transactions

Changes:

- The field is added to the return value for Identifying the ERC721 property id: `erc721propertyid` 
- The field is added to the return value for Identifying the ERC721 token id: `erc721tokenid` 

## Wormhole Spec documents

1. White Paper     https://github.com/copernet/spec/blob/master/whcwhitepaper-en.pdf
2. Yellow Paper     https://github.com/copernet/spec/blob/master/wormhole-yellowpaper-en.md
3. Spec       https://github.com/copernet/spec/blob/master/wormhole-spec-en.md
4. RPC manual    https://github.com/copernet/spec/blob/master/wormhole-rpc-en.md
5. Test manual   https://github.com/copernet/spec/blob/master/wormhole-testmanual-0.2.0-en.md


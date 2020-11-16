<!-- BEGIN HTML HEADER -->

<p align="center">
 <img src="https://rawcdn.githack.com/sambacha/baseline-truffle-box/ad527b263a58f53e2ede4e8f026fcdb51ed40c6d/docs/box-img-lg.png" align="right" width="350">
	<h1 align="left">Baseline Protocol Truffle Box</h1>
 <h3 align="center">  </h3>
 <p align="center">
<align="center">
  
<!-- END HTML HEADER -->  

## Developer Tools 🛠️ 

- [Truffle](https://trufflesuite.com/)
- [Baseline](https://github.com/ethereum-oasis/baseline)
- [Openzeppelin Contracts](https://openzeppelin.com/contracts/)

## Workflows 🧰

- [BPMN](#)
- [Splunk](#)
- [Provide](#)
- [Add yours here](https://github.com/sambacha/baseline-truffle-box/issues/new)

## Organization Registry 💼

Each organization registered within the OrgRegistry first generates a secp256k1 keypair and uses the Ethereum public address representation as "primary key" for future resolution. This key SHOULD NOT sign transactions. A best practice is to use an HD wallet to rotate keys, preventing any account from signing more than a single transaction.

Note that an organization may not update its address.

```solidity
struct Org {
    address orgAddress;
    bytes32 name;
    bytes messagingEndpoint;
    bytes whisperKey;
    bytes zkpPublicKey;
    bytes metadata;
}

struct OrgInterfaces {
    bytes32 groupName;
    address tokenAddress;
    address shieldAddress;
    address verifierAddress;
}

mapping (address => Org) orgMap;
mapping (uint => OrgInterfaces) orgInterfaceMap;
uint orgInterfaceCount;

Org[] public orgs;
mapping(address => address) managerMap;

event RegisterOrg(
    bytes32 _name,
    address _address,
    bytes _messagingEndpoint,
    bytes _whisperKey,
    bytes _zkpPublicKey,
    bytes _metadata
);

event UpdateOrg(
    bytes32 _name,
    address _address,
    bytes _messagingEndpoint,
    bytes _whisperKey,
    bytes _zkpPublicKey,
    bytes _metadata
);
```
## Shield 🛡

Unlike the Radish34 Reference Implementation, the contracts package does not include a "shield" contract. Rather, it is up to each workgroup to determine a suitable shielding mechanism to ensure privacy. For example, the IBaselineRPC implementation within the Nethermind client used in the BRI-1 Reference Implementation ships with shield contract binaries (i.e., including the MerkleTreeSHA contract).

## Registry Contracts Overview 🏢

#### Files Description Table

| File Name                           | SHA-1 Hash                               |
| ----------------------------------- | ---------------------------------------- |
| contracts/registry/IOrgRegistry.sol | 0514e15aa16c4c92f61c3cdc3f17d93e3ee56377 |
| contracts/registry/OrgRegistry.sol  | e0bb2ddd83c0d3373d6b58d50ec756a833ac88d0 |
| contracts/registry/Registrar.sol    | 6507a72d2283a5e2cc04bc99ea90ef1f878fe9b7 |

#### Contracts Description Table

|     Contract     |              Type               |                       Bases                        |                |                            |
| :--------------: | :-----------------------------: | :------------------------------------------------: | :------------: | :------------------------: |
|        └         |        **Function Name**        |                   **Visibility**                   | **Mutability** |       **Modifiers**        |
|                  |                                 |                                                    |                |                            |
| **IOrgRegistry** |            Interface            |                                                    |                |                            |
|        └         |           registerOrg           |                    External ❗️                    |       🛑       |           NO❗️            |
|        └         |            updateOrg            |                    External ❗️                    |       🛑       |           NO❗️            |
|        └         |           getOrgCount           |                    External ❗️                    |                |           NO❗️            |
|        └         |             getOrg              |                    External ❗️                    |                |           NO❗️            |
|                  |                                 |                                                    |                |                            |
| **OrgRegistry**  |         Implementation          | Ownable, ERC165Compatible, Registrar, IOrgRegistry |                |                            |
|        └         |          <Constructor>          |                     Public ❗️                     |       🛑       | ERC165Compatible Registrar |
|        └         |          setInterfaces          |                     Public ❗️                     |       🛑       |         onlyOwner          |
|        └         |          getInterfaces          |                    External ❗️                    |                |           NO❗️            |
|        └         | canImplementInterfaceForAddress |                    External ❗️                    |                |           NO❗️            |
|        └         |          assignManager          |                    External ❗️                    |       🛑       |         onlyOwner          |
|        └         |           registerOrg           |                    External ❗️                    |       🛑       |         onlyOwner          |
|        └         |            updateOrg            |                    External ❗️                    |       🛑       |           NO❗️            |
|        └         |       registerInterfaces        |                    External ❗️                    |       🛑       |         onlyOwner          |
|        └         |           getOrgCount           |                    External ❗️                    |                |           NO❗️            |
|        └         |             getOrg              |                    External ❗️                    |                |           NO❗️            |
|        └         |      getInterfaceAddresses      |                    External ❗️                    |                |           NO❗️            |
|                  |                                 |                                                    |                |                            |
|  **Registrar**   |         Implementation          |                                                    |                |                            |
|        └         |          <Constructor>          |                     Public ❗️                     |       🛑       |           NO❗️            |
|        └         |   setInterfaceImplementation    |                    Internal 🔒                     |       🛑       |                            |
|        └         |          interfaceAddr          |                    External ❗️                    |                |           NO❗️            |
|        └         |        assignManagement         |                    Internal 🔒                     |       🛑       |                            |
|        └         |           getManager            |                     Public ❗️                     |                |           NO❗️            |

#### Legend

| Symbol | Meaning                   |
| :----: | ------------------------- |
|   🛑   | Function can modify state |
|   💵   | Function is payable       |

## Privacy Contracts Description Report 🔮

#### Files Description Table

| File Name                       | SHA-1 Hash                               |
| ------------------------------- | ---------------------------------------- |
| contracts/privacy/IShield.sol   | c4b6e694bbdd4317e6fdc1e595e467cb10e5e1dd |
| contracts/privacy/IVerifier.sol | ba4926ea2f01fde5d11362808fc1e573e69e31e3 |
| contracts/privacy/Shield.sol    | 14415a0a47a10c0865993bdc3c8a350c683dc69f |

#### Contracts Description Table

|   Contract    |       Type        |           Bases           |                |                  |
| :-----------: | :---------------: | :-----------------------: | :------------: | :--------------: |
|       └       | **Function Name** |      **Visibility**       | **Mutability** |  **Modifiers**   |
|               |                   |                           |                |                  |
|  **IShield**  |     Interface     |                           |                |                  |
|       └       |    getVerifier    |       External ❗️        |                |      NO❗️       |
|       └       |   verifyAndPush   |       External ❗️        |       🛑       |      NO❗️       |
|               |                   |                           |                |                  |
| **IVerifier** |     Interface     |                           |                |                  |
|       └       |      verify       |       External ❗️        |       🛑       |      NO❗️       |
|               |                   |                           |                |                  |
|  **Shield**   |  Implementation   | IShield, MerkleTreeSHA256 |                |                  |
|       └       |   <Constructor>   |        Public ❗️         |       🛑       | MerkleTreeSHA256 |
|       └       |    getVerifier    |       External ❗️        |                |      NO❗️       |
|       └       |   verifyAndPush   |       External ❗️        |       🛑       |      NO❗️       |

#### Legend

| Symbol | Meaning                   |
| :----: | ------------------------- |
|   🛑   | Function can modify state |
|   💵   | Function is payable       |


## License 

CC-0

## `OrgRegistry`



Contract for maintaining organization registry
Contract inherits from Ownable and ERC165Compatible
Ownable contains ownership criteria of the organization registry
ERC165Compatible contains interface compatibility checks


### `constructor(address _erc1820)` (public)



constructor function that takes the address of a pre-deployed ERC1820
registry. Ideally, this contract is a publicly known address:
0x1820a4B7618BdE71Dce8cdc73aAB6C95905faD24. Inherently, the constructor
sets the interfaces and registers the current contract with the global registry

### `setInterfaces() → bool` (public)

This is an implementation of setting interfaces for the organization
registry contract


the character '^' corresponds to bit wise xor of individual interface id's
which are the parsed 4 bytes of the function signature of each of the functions
in the org registry contract

### `getInterfaces() → bytes4` (external)

This function is a helper function to be able to get the
set interface id by the setInterfaces()



### `canImplementInterfaceForAddress(bytes32 interfaceHash, address addr) → bytes32` (external)

Indicates whether the contract implements the interface 'interfaceHash' for the address 'addr' or not.


Below implementation is necessary to be able to have the ability to register with ERC1820


### `assignManager(address _newManager)` (external)



Since this is an inherited method from Registrar, it allows for a new manager to be set
for this contract instance

### `registerOrg(address _address, bytes32 _name, bytes _messagingEndpoint, bytes _whisperKey, bytes _zkpPublicKey, bytes _metadata) → bool` (external)

Function to register an organization


Function to register an organization


### `updateOrg(address _address, bytes32 _name, bytes _messagingEndpoint, bytes _whisperKey, bytes _zkpPublicKey, bytes _metadata) → bool` (external)

Function to update an organization


Function to update an organization


### `registerInterfaces(bytes32 _groupName, address _tokenAddress, address _shieldAddress, address _verifierAddress) → bool` (external)

Function to register the names of the interfaces associated with the OrgRegistry


Function to register an organization's interfaces for easy lookup


### `getOrgCount() → uint256` (external)



Function to get the count of number of organizations to help with extraction


### `getOrg(address _address) → address, bytes32, bytes, bytes, bytes, bytes` (external)

Function to get a single organization's details



### `getInterfaceAddresses() → bytes32[], address[], address[], address[]` (external)

Function to get organization's interface details




### `RegisterOrg(bytes32 _name, address _address, bytes _messagingEndpoint, bytes _whisperKey, bytes _zkpPublicKey, bytes _metadata)`





### `UpdateOrg(bytes32 _name, address _address, bytes _messagingEndpoint, bytes _whisperKey, bytes _zkpPublicKey, bytes _metadata)`






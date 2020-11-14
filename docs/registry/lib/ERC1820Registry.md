## `ERC1820Registry`

This contract is the official implementation of the ERC1820 Registry.
For more details, see https://eips.ethereum.org/EIPS/eip-1820




### `getInterfaceImplementer(address _addr, bytes32 _interfaceHash) → address` (external)

Query if an address implements an interface and through which contract.




### `setInterfaceImplementer(address _addr, bytes32 _interfaceHash, address _implementer)` (external)

Sets the contract which implements a specific interface for an address.
Only the manager defined for that address can set it.
(Each address is the manager for itself until it sets a new manager.)




### `setManager(address _addr, address _newManager)` (external)

Sets '_newManager' as manager for '_addr'.
The new manager will be able to call 'setInterfaceImplementer' for '_addr'.




### `getManager(address _addr) → address` (public)

Get the manager of an address.




### `interfaceHash(string _interfaceName) → bytes32` (external)

Compute the keccak256 hash of an interface given its name.




### `updateERC165Cache(address _contract, bytes4 _interfaceId)` (external)

Updates the cache with whether the contract implements an ERC165 interface or not.




### `implementsERC165Interface(address _contract, bytes4 _interfaceId) → bool` (public)





### `implementsERC165InterfaceNoCache(address _contract, bytes4 _interfaceId) → bool` (public)

Checks whether a contract implements an ERC165 interface or not without using nor updating the cache.




### `isERC165Interface(bytes32 _interfaceHash) → bool` (internal)

Checks whether the hash is a ERC165 interface (ending with 28 zeroes) or not.




### `noThrowCall(address _contract, bytes4 _interfaceId) → uint256 success, uint256 result` (internal)



Make a call on a contract without throwing if the function does not exist.


### `InterfaceImplementerSet(address addr, bytes32 interfaceHash, address implementer)`

Indicates a contract is the 'implementer' of 'interfaceHash' for 'addr'.



### `ManagerChanged(address addr, address newManager)`

Indicates 'newManager' is the address of the new manager for 'addr'.




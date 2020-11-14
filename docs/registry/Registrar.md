## `Registrar`



Contract that acts as a client for interacting with the ERC1820Registry

### `onlyManager()`



Throws if called by any account other than the owner.


### `constructor(address ERC1820RegistryAddress)` (public)

Constructor that takes an argument of the ERC1820RegistryAddress


Upon actual deployment of a static registry contract, this argument can be removed


### `setInterfaceImplementation(string _interfaceLabel, address _implementation)` (internal)

Since this is an internal method any contract inheriting this contract would be
leveraged as the sender for the interface registry


This enables setting the interface implementation


### `interfaceAddr(address addr, string _interfaceLabel) → address` (external)



This enables getting the address of the implementer


### `assignManagement(address _newManager)` (internal)

Since this is an internal method any contract inheriting this contract would be
leveraged to call this function directly


This enables assigning or changing manager


### `getManager() → address` (public)



This allows you to get this contract manager address



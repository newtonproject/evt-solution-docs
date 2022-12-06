# EVT Specs

Moive EVT supports the following interfaces

### Variable Interfaces

```
interface EVTVariable {
    /// @dev This emits when token dynamic property added.
    event DynamicPropertyAdded(bytes32 _propertyId);

    /// @dev This emits when token dynamic property updated.
    event DynamicPropertyUpdated(uint256 _tokenId, bytes32 _propertyId, bytes _propertyValue);

    /// @notice Add the dynamic property
    /// @param _propertyId property ID
    function addDynamicProperty(bytes32 _propertyId) external payable;

    /// @notice Set the dynamic property
    /// @param _tokenId token ID
    /// @param _propertyId property ID
    /// @param _propertyValue property value
    function setDynamicProperty(uint256 _tokenId, bytes32 _propertyId, bytes _propertyValue) external payable;

    /// @notice Set multiple dynamic properties once
    /// @param _tokenId token ID
    /// @param _message message
    function setDynamicProperties(uint256 _tokenId, bytes _message) external payable;

    /// @notice Retrieve the vale of dynamic property
    /// @param _tokenId token ID
    /// @param _propertyId property ID
    /// @return property value
    function getDynamicProperty(uint256 _tokenId, bytes32 _propertyId) external view returns (bytes);

    /// @notice Retrieve the all properties including dynamic and static
    /// @param _tokenId token ID
    /// @return ids, properties
    function getDynamicProperties(uint256 _tokenId) external view returns (bytes32[], bytes[]);

    /// @notice Check whether support the given property
    /// @param _propertyId property ID
    /// @return support or unsupport
    function supportsProperty(bytes32 _propertyId) external view returns (bool);
}
```

### Encryption Interfaces

```
interface EVTEncryption {
​    /// @notice This emits when registered a encrypted key.
​    /// @param _tokenId token ID
​    /// @param _encryptedKeyId encrypted key ID
​    event EncryptedKeyRegistered(uint256 indexed _tokenId, bytes32 _encryptedKeyId);

    /// @notice This emits when add a permission.
​    /// @param _tokenId token ID
​    /// @param _encryptedKeyId encrypted key ID
​    /// @param _licensee licensee
​    event PermissionAdded(uint256 indexed _tokenId, bytes32 _encryptedKeyId, address indexed _licensee);

    /// @notice This emits when remove a permission.
​    /// @param _tokenId token ID
​    /// @param _encryptedKeyId encrypted key ID
​    /// @param _licensee licensee
​    event PermissionRemoved(uint256 indexed _tokenId, bytes32 _encryptedKeyId, address indexed _licensee);

    /// @notice Register encrypted key
    /// @param _tokenId token ID
    /// @param _encryptedKeyId encrypted key ID
    function registerEncryptedKey(uint256 _tokenId, bytes32 _encryptedKeyId) external payable;

    /// @notice Add the permission rule of the encrypted key for given address
    /// @param _tokenId token ID
    /// @param _encryptedKeyId encrypted key ID
    /// @param _licensee licensee
    function addPermission(uint256 _tokenId, bytes32 _encryptedKeyId, address _licensee) external payable;

    /// @notice Remove the permission rule of the encrypted key for given address
    /// @param _tokenId token ID
    /// @param _encryptedKeyId encrypted key ID
    /// @param _licensee licensee
    function removePermission(uint256 _tokenId, bytes32 _encryptedKeyId, address _licensee) external;

    /// @notice Check permission rule of the encrypted key for given address
    /// @param _tokenId token ID
    /// @param _encryptedKeyId encrypted key ID
    /// @param _licensee licensee
    /// @return true or false
    function hasPermission(uint256 _tokenId, bytes32 _encryptedKeyId, address _licensee) external view returns (bool);
}
```

### ERC721 Interfaces

- [erc721#IERC721](https://docs.openzeppelin.com/contracts/4.x/api/token/erc721#IERC721)

### ERC721URIStorage Interfaces

- [erc721#ERC721URIStorage](https://docs.openzeppelin.com/contracts/4.x/api/token/erc721#ERC721URIStorage)

### ERC721Enumerable Interfaces

- [erc721#ERC721Enumerable](https://docs.openzeppelin.com/contracts/4.x/api/token/erc721#ERC721Enumerable)

### Ownable Interfaces

- [access#Ownable](https://docs.openzeppelin.com/contracts/4.x/api/access#Ownable)

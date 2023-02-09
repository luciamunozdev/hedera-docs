# ContractUpdate

## ContractUpdateTransactionBody

Modify a smart contract instance to have the given parameter values. Any null field is ignored (left unchanged). If only the `contractInstanceExpirationTime` is being modified, then no signature is needed on this transaction other than for the account paying for the transaction itself. But if any of the other fields are being modified, then it must be signed by the `adminKey`. The use of `adminKey` is not currently supported in this API, but in the future will be implemented to allow these fields to be modified, and also to make modifications to the state of the instance. If the contract is created with no admin key, then none of the fields can be changed that need an admin signature, and therefore no admin key can ever be added. The `adminKey` can be used to add flexibility to the management of smart contract behavior, but this is optional. If the smart contract is created without an `adminKey`, then such a key can never be added, and none of the fields can be changed that need an admin signature.

| Field             | Type                                       | Description                                                                                                                                                                                                                                                                                                                                                                                                                   |
| ----------------- | ------------------------------------------ | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `contractID`      | [ContractID](../basic-types/contractid.md) | The Contract ID instance to update (this can't be changed)                                                                                                                                                                                                                                                                                                                                                                    |
| `expirationTime`  | [Timestamp](../miscellaneous/timestamp.md) | Extend the expiration of the instance and its account to this time (no effect if it already is this time or later)                                                                                                                                                                                                                                                                                                            |
| `adminKey`        | [Key](../basic-types/key.md)               | The state of the instance can be modified arbitrarily if this key signs a transaction to modify it. If this is null, then such modifications are not possible, and there is no administrator that can override the normal operation of this smart contract instance.                                                                                                                                                          |
| `proxyAccountID`  | [AccountID](../basic-types/accountid.md)   | ID of the account to which this account is proxy staked. If proxyAccountID is null, or is an invalid account, or is an account that isn't a node, then this account is automatically proxy staked to a node chosen by the network, but without earning payments. If the proxyAccountID account refuses to accept proxy staking , or if it is not currently running a node, then it will behave as if proxyAccountID was null. |
| `autoRenewPeriod` | [Duration](../miscellaneous/duration.md)   | The instance will charge its account every this many seconds to renew for this long                                                                                                                                                                                                                                                                                                                                           |
| `fileID`          | [FileID](../basic-types/fileid.md)         | The file ID of file containing the smart contract byte code. A copy will be made and held by the contract instance, and have the same expiration time as the instance. **\[deprecated 0.20.0]**                                                                                                                                                                                                                               |
| `memo`            | string                                     | The memo associated with the contract (max 100 bytes)                                                                                                                                                                                                                                                                                                                                                                         |
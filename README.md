# QuestChain Masternode Setup Guide

## Initial Setup:
### Generate New Addresses
Use the `getnewaddress` command in your QuestChain wallet console to generate new addresses for various purposes:
- **CollateralAddress**: Send exactly 1,000,000 QCH to this address. This will be locked as collateral.
- **OwnerKeyAddress**: Must be new and unused. Can also be used as the VotingKeyAddress.
- **VotingKeyAddress**: Can be the same as the OwnerKeyAddress, but must not be the CollateralAddress.
- **PayoutAddress**: Where masternode rewards are sent. It can also be the same as CollateralAddress.
- **FeeSourceAddress**: Should have sufficient funds to cover transaction fees for the protx transactions. It is advisable not to use the CollateralAddress for this purpose.

### Register Your Masternode
Use the `protx register_prepare` command followed by the necessary parameters:
- **collateralHash**: The TXID of the 1,000,000 QCH collateral funding transaction.
- **collateralIndex**: The output index of the funding transaction (either 0 or 1).
- **ipAndPort**: Your masternode's IP address and port. Format for IPv4: `x.x.x.x:40000`, for IPv6: `[x:x:x:x:x:x:x:x]:40000`.
- **ownerKeyAddr**: The new QCH address generated above for the owner/voting address.
- **operatorPubKey**: The BLS public key generated earlier.
- **votingKeyAddr**: The new QCH address generated above or the address of a delegate, used for proposal voting.
- **operatorReward**: Usually set to "0" as you might want 100% of the reward going to the owner.
- **payoutAddress**: A new or existing QCH address to receive the owner’s masternode rewards.
- **feeSourceAddress**: An address used to fund the ProTx fee.

### Sign the Transaction
Use the `signmessage` command with your CollateralAddress to sign the transaction.

### Submit the Transaction
Use the `protx register_submit` command to finalize the registration by submitting the signed transaction.

## Maintenance and Monitoring
Regularly check your masternode status in the QuestChain wallet under the Masternodes tab.
Address any issues indicated by an increasing PoSe Score (Proof of Service Score) to avoid disruptions in service.

## Updates
If moving the node to a different VPS or changing IP addresses, use `protx update_service` to update the node details on the blockchain.

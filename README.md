## Setting Up Masternode for QuestChain (QCH)

1. Open your QuestChain wallet and navigate to the console via `Tools -> Debug console`.
2. Generate two new addresses:
   - Enter `getnewaddress "label"` (example: `getnewaddress MN1`)
   - Enter `getnewaddress "label"` (example: `getnewaddress MN1-owner`)
3. Send exactly 1000000 QCH to the first address and wait until the transaction has 15 confirmations.
4. Run `masternode outputs` in the console and note the respective TX-ID and TX-Index for the steps below.

Next, you need to prepare the masternode to be registered on-chain using the template below (replace the red variables with your data):


protx register_prepare collateralHash collateralIndex ipAndPort ownerKeyAddr operatorPubKey votingKeyAddr operatorReward payoutAddress feeSourceAddress


- `collateralHash`: TX-ID of the transaction containing the 1000000 QCH.
- `collateralIndex`: TX-Index of the transaction containing the 1000000 QCH.
- `ipAndPort`: IP and p2p port (IPv4: 5.189.159.94:40000 | IPv6: [2a02:c207:3005:3682::19]:40000).
- `ownerKeyAddr`: The second new address generated.
- `operatorPubKey`: Public Key from BLS keypair.
- `votingKeyAddr`: The second new address generated.
- `operatorReward`: 0.
- `payoutAddress`: Your masternode address or a new one you want to receive the rewards.
- `feeSourceAddress`: An address in your wallet with a few QCH for TX fees.

If the command was executed successfully, the wallet will respond with 3 strings containing "tx", "collateralAddress", "signMessage".

Next, run `signmessage collateralAddress signMessage`, replacing both variables with the data above (without quotes).

If the command was executed successfully, the wallet will respond with 1 string containing the signature.

Finally, run `protx register_submit tx signature` to submit the masternode to the chain.

You do not need to keep a record of that console output. After a few blocks, you should see your new masternode appear in the masternode tab of your controller.

Note: There is no more masternode.conf file or similar. Everything is done "on-chain" using the commands above. You can verify your masternode is running successfully on VPS with the `masternode status` command. If the state "READY" is displayed, your masternode is running, and you will get your reward on the Next Payment block.

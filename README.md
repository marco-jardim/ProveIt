# ProveIt
 
At long last, we have the technology. You can finally _prove_ to your friends that you liked that band before they were cool! :ok_hand:
 
ProveIt implements proof of historical data possession on the Ethereum blockchain. What this means in practice is that any Ethereum address can submit a text string or a 32-byte cryptographic hash of data to ProveIt's ledger and gain the ability to prove that the owner(s) of this address wrote/possessed the text/data at a particular time. The ledger also allows addresses to stake arbitrary amounts of Ether alongside their entries, lending credibility.
 
Potential uses cases:
* Individual __I__ is a rabid Elon Musk fan, and wants to make a prediction about Musk's glorious future endeavors. Using their Ethereum address __A__, __I__ could submit ```By 2030, a company founded or owned in part by Elon Musk will have delivered a human to the surface of Mars``` to the ProveIt ledger at time __T__. At any point from now until 2030, __I__ can submit evidence of their ownership of __A__ in standard ways (i.e. by signing a credible message via something like the [Etherscan verifySig tool](https://etherscan.io/verifySig)) thereby proving that they made this statement at time __T__. This makes __I__ seem prescient, and more importantly, affirms their Musk fanhood. One could imagine, however, that a rival Musk supporter __R__ might submit many such messages, varying the year, and revealing only the one that makes them appear most credible. To combat this issue, __I__ can lock up an arbitrary amount, __x__, of ether alongside their statement. This amount cannot be recovered without destroying the associated ledger entry. If we assume that __R__ must submit 20 different entries to have a high probability of ending up with at least one very close prediction, they’re forced to lock up 20*__x__ ether, dissuading them from attacking.
* Imagine that Individual __I__ is also an amateur paparazzo/a, and manages to snap an incredibly ~~compromising~~ valuable photograph of Elon. They’re desperately worried that this photo will be stolen and published by __R__, depriving __I__ of all glory and potential proceeds. If __I__ wishes to prove possession of this photograph at time __T__ they can simply make a (cryptographically secure) 32-byte hash of this photograph, and store the hash in ProveIt. The data that produced this hash will of course be unknown at time __T__, but at any point in the future __I__ could release the data (photograph) and allow anyone to verify that it does indeed hash to the entry that __I__ made in ProveIt at time __T__.
 
Technical notes:
* While building ProveIt, I realized that having set functionality would be helpful, so I implemented it in contracts/Sets.sol. It's quite efficient, with O(1) insertion, removal, and existence checks.
* Sets.sol is deployed at: ```0x4e61847E3b0C5786e81C8cd477c4af76b5F7098f``` and is [verified on Etherscan](https://etherscan.io/address/0x4e61847e3b0c5786e81c8cd477c4af76b5f7098f).
* Prover.sol is deployed at: ```0x4125c610b63dd63bE5c48D5CC3C68784F92D3B43``` and is [verified on Etherscan](https://etherscan.io/address/0x4125c610b63dd63bE5c48D5CC3C68784F92D3B43).
* While using popular services like MyEtherWallet to read/write text string entries to ProveIt works, I'm having trouble submitting hashes via these services, I think because the 64-character hex strings are not being treated as 32-byte data. I'm working on a custom front-end for ProveIt that will hopefully fix some of these issues.
* I've yet to implement tests, but they're coming...of course you're free to audit the code yourself.

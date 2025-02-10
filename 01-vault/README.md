# Vault - Tier 1
You are looking through an old version of the OpenZeppelin implementation of ERC-4626 and notice a vulnerability that requires frontrunning an innocent user. You have been granted a large amount of ETH (say e.g. 1k ETH, but you are free to choose the amount :) ) and want to set up a whitehat bot to execute this exploit and return the funds to the user.


- a) Describe the vulnerability and the payoffs for an attacker.
The vulnerability in the old OpenZeppelin ERC-4626 implementation likely involves share price manipulation through frontrunning. The vault does not update share prices atomically when large deposits occur, allowing an attacker to:
1) Observe an incoming large deposit.
2) Frontrun with a small deposit before the large one executes, obtaining shares at an artificially low price.
3) Let the large deposit increase the share price since the new user’s deposit increases total assets without immediately affecting total shares.
4) Redeem their shares at the new, inflated price, extracting value from the vault.

Payoff for an Attacker
A malicious attacker can execute this repeatedly, making risk-free profits at the expense of innocent users. The vault will distribute fewer shares to large depositors than they should receive, causing them to overpay for shares.

- b)  Produce code that can check if this vulnerability has occurred in the past and determine how much value was lost, if any.
- c)  Write code for the bot that can carry out the exploit (don’t worry about returning user funds).

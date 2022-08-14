# Audit-Report

### Background
Sturdy is a protocol for interest-free borrowing and high yield lending.

Lenders deposit stablecoins that they want to earn yield on while borrowers provide collateral and take out loans at no interest (interest rates will kick in above certain utilization rates, but this functionality is out of scope). Sturdy accomplishes this by staking collateral provided by borrowers in third party protocols like Yearn, Lido, and Convex. The yield from collateral staking is periodically harvested, swapped to stablecoins, and distributed to stablecoin lenders.

Sturdy forked Aave V2 contracts for its underlying accounting and lending pool mechanics. In order to convert non-interest bearing tokens ('external assets', e.g. ETH) to their interest bearing equivalent ('internal assets', e.g. stETH), Sturdy uses modules called 'vaults.' When users deposit external assets to a vault, the vault immediately stakes it, converting it to an internal asset, and deposits it to the lending pool. When users want to withdraw their collateral, the vault withdraws the internal asset from the lending pool, unstakes it, and returns it to the user. The user can also deposit or withdraw internal assets directly from the lending pool by interacting directly with the smart contracts.

PoolAdmin can harvest the yield by calling a function that distributes excess staked collateral to lenders after swapping it to stablecoins. This can take on a different form based on the specific collateral asset and staking strategy as described for each vault contract below.

The full repository (with tests) can be found here.


### Findings

# clone-lin-saddle-getd

Experimental i64-scale LIN clone of [saddle-finance/saddle-contract](https://github.com/saddle-finance/saddle-contract) commit `2cfdd05580efb626d79d597034b2cf5ae89b5626` `SwapUtils.getD` / `getY` (`contracts/SwapUtils.sol`, MIT).

- **LIN clone:** [`src/lin_saddle_getd.lin`](src/lin_saddle_getd.lin)
- **Proofs (results only) live in lin-open:** https://github.com/kbelludoo/lin-open/tree/master/examples/saddle_getd
- **Event receipt:** `docs/events/EVENT_SADDLE_GETD_CLONE_LIN.rulel` in lin-open

This repository is the standalone LIN copy. It is **not** a Saddle pool, **not** Curve.vy, and does **not** claim Solidity uint256 / N>2 parity.

Curve.Fi `curve-contract` was not copied: its LICENSE grants no reproduction right. Saddle is the MIT Solidity Newton D.

Canonical goldens (uint64-scale, N=2, precise A = display A * 100):

- `getD(1000,1000,10000)` = **2000** (balanced D equals sum)
- `getD(1000,2000,10000)` = **2998** (imbalanced D < sum)
- `getD(1000000,1000000,20000)` = **2000000**
- `getD(1000000,1100000,20000)` = **2099988**
- `getY(1000,1000,10000,1000)` = **1000** (identity)
- `getY(1000,1000,10000,1010)` = **990**
- fee-less Saddle `dy` = `x1 - y - 1`: `dy(1000,1000,10000,10)` = **9**
- `dy(1000000,1000000,20000,10000)` = **9999** vs Uniswap-style `cp_dy` = **9871**
- zero / negative / A=0 fail-close to **0** (Saddle reverts)

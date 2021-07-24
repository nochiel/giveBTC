
# [WIP] Comparison of btc donation tools.

| Name                  | Requires Full Node    | Tor   | User imports xpub | App generates new hot-wallet      | Has plugin architecture       | BTC (L1) | Lightning (L2)     | Ease of installation                                |
|-----------------------|-----------------------|-------|-------------------|-----------------------------------|-------------------------------|----------|--------------------|-----------------------------------------------------|
| CypherPunkPay         | N                     | Y     |   Y                 |  N                               | -                            |  Y       | Y                  | Hard (Command-line)                                 |
| LNBits                | N                     | N     |   N                 |  Y                               | Y                            |  N       | Y                  | Easy (1 hosted service can have multiple users.)    |
| BTCPay                | Y                     | Y     |   N                 |  Y                               | Not really (hard to use)     |  Y       | Y                  | Easy (LunaNode launcher)                            |


# CypherPunkPay

- We need to make this easy to install: 
    - add CypherPunkPay as a BitcoinStandup-Script module.
    - create a CypherPunkPay one-click [LunaNode](https://www.lunanode.com/) launcher
    - create a CypherPunkPay one-click [Voltage](https://voltage.cloud/) launcher.

- Maintenance is cheap: A USD5 p.m VPS should be sufficient. (TODO Verify claim by testing.)
    - A Bitcoin full-node is not needed. CypherPunkPay uses randomly selected Blockchain explorers to download blocks.
    - A Lightning full-node can be run in a lightweight way using the [TrustedCoin](https://github.com/fiatjaf/trustedcoin) LND plugin that also uses Blockchain explorers to download blocks.



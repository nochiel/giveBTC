
# [WIP] Comparison of btc donation tools.

| Name                  | Requires Full Node    | Tor   | User imports xpub | App generates new hot-wallet      | Has plugin architecture       | BTC (L1) | Lightning (L2)     | Ease of installation                                |
|-----------------------|-----------------------|-------|-------------------|-----------------------------------|-------------------------------|----------|--------------------|-----------------------------------------------------|
| CypherpunkPay         | N                     | Y     |   Y                 |  N                               | Y (Easily extensible.)       |  Y       | Y but requires configuration. | Easy (Using [BitcoinStandup-Scripts for Linode]())                                 |
| LNBits                | N                     | N     |   N                 |  Y                               | Y                            |  N       | Y                  | Easy (1 hosted service can have multiple users.)    |
| BTCPay                | Y                     | Y     |   N                 |  Y                               | Not really (hard to use)     |  Y       | Y                  | Easy (LunaNode launcher)                            |



# CypherpunkPay

- We need to make this easy to install: 
    - [x] add CypherpunkPay as a BitcoinStandup-Script module.
    - ~Create a CypherpunkPay one-click [LunaNode](https://www.lunanode.com/) launcher~
        - Not really necessary because it's now easy to use a BlockchainCommons Linode Stackscript to install.
    - ~Create a CypherpunkPay one-click [Voltage](https://voltage.cloud/) launcher.~

- Maintenance of CypherpunkPay is cheap: A USD5 p.m VPS should be sufficient. 
    - A Bitcoin full-node is not needed. CypherpunkPay can use randomly selected Blockchain explorers to download blocks.
    - A Lightning node for CypherpunkPay can be run in a lightweight way using:
        - [LND](https://github.com/lightningnetwork/lnd/blob/master/docs/INSTALL.md#using-neutrino) configured with the [Neutrino backend](https://github.com/lightningnetwork/lnd/blob/master/docs/INSTALL.md#using-neutrino) which makes use of a Bitcoin node with BIP157 and BIP158 enabled.
        - C-lightning configured to use the [TrustedCoin](https://github.com/fiatjaf/trustedcoin)  plugin which allows the node to run without requiring a Bitcoin full-node by retreiving blocks from a set of public block explorers. 
    - LND for Lightning is currently available in the development and testing configurations. However, because it requires the user to know how to configure it, it's not enabled by default in BitcoinStandup-Scripts.

---

Below is a guide on how to get started receiving bitcoin donations with a self-sovereign setup:

# How to receive Bitcoin donations using CypherpunkPay and [BlueWallet](https://bluewallet.io/)

0. Create a [Linode](linode.com) account. This will allow you to have your own virtual private server (VPS).

1. Use the ["Learning Bitcoin from the Commandline", 2.1: Setting Up a Bitcoin-Core VPS with Bitcoin Standup](https://github.com/BlockchainCommons/Learning-Bitcoin-from-the-Command-Line/blob/master/02_1_Setting_Up_a_Bitcoin-Core_VPS_with_StackScript.md) guide to make use of the BlockchainCommons Linode StackScript.
- Refer to [How to Deploy a New Linode Using a Stackscript](https://www.linode.com/docs/guides/how-to-deploy-a-new-linode-using-a-stackscript/) if you would like to know more about how to use Stackscripts.

2. If you would like to get started as quickly as possible choose `Pruned Mainnet` as your `Installation Type`.

3. Configure the options for installing CypherpunkPay. 

4.To enable CypherpunkPay to generate bitcoin addresses for you, you will need to import an Extended Public Key (xpub) from *a brand new wallet. While you can use any wallet software to do this, it is very easy to use BlueWallet, for this as it allows you to maintain several distinct wallets within the app.
- Create a new wallet labeled "CypherpunkPay". Select the wallet.
- Open wallet options (3 dots at the top-right of the app) and choose "Show XPUB". You will be presented with a QR code and string beginning with xpub or ypub or zpub. Copy this string into the "xpub" text box of the CypherpunkPay configuration. 
    - You can learn about Heirarchically Deterministic Wallets and xpubs by reading [All you need to know about HD wallets, xpub, ypub and zpub](https://medium.com/cryptoapis/all-you-need-to-know-about-hd-wallets-xpub-ypub-and-zpub-f6601f1bce35)

5. Deploy your Linode as described in the linked guide in Step 1.

6. Your CypherpunkPay donation page will be accessible only through Tor. It can only be accessed using a [Tor Browser](https://www.torproject.org/download/). (Download and install it on your smartphone or laptop.)
- Using Tor ensures that the precise location of your server can't be determined by a visitor nor will you or anyone with access to your server be able to determine the location of a donor who uses your CypherpunkPay page. 
- You can learn about Tor by reading ["Learning Bitcoin from the Commandline", Chapter 14: Using Tor](https://github.com/BlockchainCommons/Learning-Bitcoin-from-the-Command-Line/blob/master/14_0_Using_Tor.md) 
- To find the address for your CypherpunkPay Hidden Service, log in to your server as described in the linked guide in Step 6 and type `sudo cat /var/lib/tor/cypherpunkpayhostname`. You will see an onion url that looks like `mgcym6je63k44b3i5uachhsndayzx7xi4ldmwrm7in7yvc766rykz6yd.onion`. Copy the address you see and save it or share it e.g. by putting it in your twitter profile.

7. Navigate to the CypherpunkPay hidden service using the Tor Browser you installed on your phone in Step 6. Donate a small amount of satoshis to yourself! You should immediately see the amount appear in your CypherpunkPay wallet in BlueWallet. Now anyone who uses your hidden service can donate to you!



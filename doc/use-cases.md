## Tradeoffs

A typical donation app involves many moving parts for someone who uses it:
- Bitcoin node
- Lightning node
- Web hosting
- Bitcoin wallet
- Lightning channels
- Private Keys
- Wallet backups
- Lightning channels backups
- Backups of private keys
- Onboarding costs and time
- Operational and maintenance costs

Ideally, one should be fully sovereign. This would require that person to **run** their own Bitcoin and Lightning nodes, **manage** their channels, securely **create and store** backups, **connect** their nodes through Tor, **host** their own website with something like Yunohost, **backup** their private keys or seed phrase on metal, and **backup** their Lightning channels states.

However, this situation usually requires deep **technical expertise** and **time** commitment and incurs high **costs**. Naturally, therefore, compromises must be made. But some aspects shouldn't be compromised on, perhaps more importantly it should be ensured that the user remains in control of their own private keys and only the user knows what the private keys are, i.e.  _`app` remains self-custodial._ Otherwise, `app` would have a deep security tradeoff most likely not worth taking.

Another compromise the app should not make relates to privacy. Addresses should not be reused by default. Optionally, but for activists most likely necessarily, the app should be behind a torgap.

Some tradeoffs that _can_ be made relate to `node`, `hosting`, and `backups`.

`nodes`: although in a perfect world the user should run their own Bitcoin and Lightning nodes, sometimes that is not possible. Nowadays there are many easy solutions for this, but still, often times either _time_ or _money_ can become a bottleneck.
- `time`: running a node usually involves spending (or investing really) lots of time. Activities inherent to running a node that demand time: debugging, researching, configuring, purchasing, maintaining, etc. `time` can be saved if the user chooses not to run the nodes themselves, resorting to a third party instead. However, this introduces some risks:
    - That third party is could snoop on the user's transactions and learn about their addresses, spending habits, and maybe even total funds. It could lead to a point of changing addresses not be necessary. This is maybe more concerning for activists, because that third party could be subpoenaed or demanded by some other means by a nation-state, for instance, to reveal the knowledge it has on the user.
        - If the app connects to the third party node through Tor, some of this risks can be diminished. Wasabi, for instance, takes it a step further and rotates Tor identities frequently, further mitigating some of the above concerns.
        - And if the user maintains control of their keys and has the ability to export and setup with another solution/third party, it might be a tradeoff worth making.
        - What are the best solutions for this? Maybe [Voltage nodes](https://blog.voltage.cloud/how-voltage-works/)?

---

> A key criteria of trade offs that I see is with Bitcoin only, private keys are only required to spend, and can be kept offline. Lightning requires private keys to online (or at least some) which means more complications to manage the higher risk. (@ChristopherA)

## [WIP] Use Cases

### Sebastian - the human rights activist

Sebastian is a human rights activist in Romania. He has limited access to the traditional banking system and resorts to Bitcoin for receiving donations, paying contractors, and covering daily expenses. He also has a very busy schedule, so he enjoys how convenient `app` is.

Sebastian opens

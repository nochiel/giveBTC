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

However, this situation usually requires deep **technical expertise** and **time** commitment and incurs high **costs**. Naturally, therefore, compromises must be made. But some aspects shouldn't be compromised on, perhaps more importantly it should be ensured that the user remains in control of their own private keys and only the user knows what the private keys are, i.e.  _`giveBTC` remains self-custodial._ Otherwise, `giveBTC` would have a deep security tradeoff most likely not worth taking.

Another compromise the app should not make relates to privacy. Addresses should not be reused by default. Optionally, but for activists most likely necessarily, the app should be behind a torgap.

Some tradeoffs that _can_ be made relate to `node`, `hosting`, and `backups`.

### Node

Although in a perfect world the user should run their own Bitcoin and Lightning nodes, sometimes that is not possible. Nowadays there are many easy solutions for this, but still, often times either _time_ or _money_ can become a bottleneck.

- `time`: running a node usually involves spending (or investing really) lots of time. Activities inherent to running a node that demand time: debugging, researching, configuring, purchasing, maintaining, etc. `time` can be saved if the user chooses not to run the nodes themselves, resorting to a third party instead. However, this introduces some risks:
    - That third party could snoop on the user's transactions and learn about their addresses, spending habits, and maybe even total funds. It could lead to a point of changing addresses not be necessary. This is maybe more concerning for activists, because that third party could be subpoenaed or demanded by some other means by a nation-state, for instance, to reveal the knowledge it has on the user.
        - If the app connects to the third party node through Tor, some of this risks can be diminished. Wasabi, for instance, takes it a step further and rotates Tor identities frequently, further mitigating some of the above concerns.
        - And if the user maintains control of their keys and has the ability to export and setup with another solution/third party, it might be a tradeoff worth making.
        - What are the best solutions for this? Maybe [Voltage nodes](https://blog.voltage.cloud/how-voltage-works/)? [Blockstream Greenlight](https://blockstream.com/lightning/greenlight/)?
          - Solutions like Voltage and Greenlight are also good on the _money_ aspect. Since they're on demand virtual nodes on the cloud, they can run on low costs. Voltage and Greenlight differ, however, as in the former packs it up into a third-party cloud solution whereas Greenlight runs on Blockstream's infrastructure.
    - Running a remote node is probably still better than running no node at all. In the latter case, the user would be using block explorers or remote servers (such as Electrum servers which is what BlueWallet uses by default) for gathering data (knowing a transaction for your address has been broadcast and confirmed) and sending data (broadcasting a transaction you send yourself).
    - In the specific case of `giveBTC`, however, receiving data will likely be what is more widely used. Doing that over `tor` can greatly improve privacy, but running a node is still better. It is specifically advised  for the user to have their own node, even if with one of the services above, because
- `sovereignty`: Perhaps the biggest upside of running a node has to do with individual sovereignty. That is because a node is the ultimate truth seeker and ruler; it determines whether you really have the amount of money you expect to have. If you trust a third-party node, chances are they could be dishonest –– for instance, they could tell you one thing when a different thing is happening in the background. However, well-established solutions tend to be at least somewhat trustworthy. It ultimately comes down to individual requirements and preferences.
    - One thing regarding sovereignty that a third-party node shouldn't compromise on is private keys. It is one thing to outsource your node, i.e. run it on a third party cloud solution; it is another completely different one to outsource your private keys, i.e. use a custodial solution. A Bitcoin or Lightning node that you don't control yourself should _at least_ not have control or knowledge over your private keys. One could go all the way down the rabbit hole to generate their own private keys with dice rolls and trust literally no one, but often times compromises must be made.
    - Both `Voltage` and `Greenlight` claim that their service has no knowledge of the user's private keys whatsoever. Blockstream's solution is still being implemented and rolled out, but Voltage's is open sourced and can be verified. The latter did modify some implementations of Lightning which haven't been widely adopted nor merged yet, so there's that.
- `money`: The node should not incur huge operating costs for the user, otherwise they might give it up entirely.

In summary, the `node` solution related to `giveBTC` should, if possible, be easy to set up and configure, empower the user for private keys sovereignty and have zero knowledge on them, and run cheaply.

### Hosting

`money`: Hosting is important because the user will most likely not commit to paying big monthly hosting fees. So the donation page should run cheaply on a hosting solution such as a VPS or even a managed one, depending on requirements.

`time`: Ideally, deploying the donation page to the cloud should be made simple for the end user. If the user has to open up the command line interface and type sudo commands, they might possibly look somewhere else. The more complex it is for the user to set up the app, the less likely it is they will do it in the first place and the more likely to be many headaches for maintaining it long term (e.g. BTCPayServer, although there _is_ a one-click install for LunaNode)

`sovereignty`: Here it is difficult to have sovereignty because the user will only be full sovereign over their hosting if they do it themselves locally, for example with Yunohost in a raspberry pi local server, or with EmbassyOS. But one choice that can be made relates to the service provider. For example, it is better for the user to purchase their domain at something like NameCheap, which has a record of standing up for their customers (Cobra case against Craig Wright) and accepts BTC, than to purchase it with KYC-hungry providers such as GoDaddy for example.

Having a one-click install on a VPS for `giveBTC` is likely the best case scenario, since the user will not likely set up everything locally due to `time`, `money` and `technical` issues –– something that even a personal VPS will incur often times, especially the technical issues side.

### Backups

Ideally, backups should be encrypted with zero-knowledge on the cloud. With encrypted backups on the cloud, the user can rest assured that if their laptop, microSD, USB drive, or house burn to the ground, backups will be available. How to best implement it? Maybe the hosting solution might be able to provide regular, automatic backups. But they will hardly be encrypted. The node solution might handle part of it too, for Lightning channels for example, like BlueWallet's mobile Lightning implementation.

If the app cannot handle everything related to backups, the user should be directed towards good resources that demonstrate good backup practices, especially for Bitcoin-related things (e.g. private keys or seed phrases).

---

> A key criteria of trade offs that I see is with Bitcoin only, private keys are only required to spend, and can be kept offline. Lightning requires private keys to online (or at least some) which means more complications to manage the higher risk. (@ChristopherA)

## [WIP] Use Cases

### Sebastian - the human rights activist

Sebastian is a human rights activist in Romania. He has limited access to the traditional banking system and resorts to Bitcoin for receiving donations, paying contractors, and covering daily expenses. He also has a very busy schedule, so he enjoys how convenient `app` is. Sebastian didn't need to learn a lot of things to be up and running with giveBTC.

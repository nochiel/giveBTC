## Tradeoffs

A typical donation app involves many moving parts for someone who uses it. In order of priority for self-sovereignty, these parts are:

- Private Keys
    - Keys are essentially one's coins. If one does not control their private keys, they merely have an IOU (from whomever holds their keys, e.g. an exchange) or they have nothing (see, for instance, all the users of AfriCrypt who were left with nothing when the founders of that exchange fled in 2021).
- Bitcoin node
    - A node is the source of truth about the state of the Bitcoin network. Without a node, one has to trust 3rd parties to tell their wallet the state of the Bitcoin network and their won unspent transaction outputs (UTXOs).
- Lightning node
- Bitcoin wallet
    - A wallet is essentially a collection of public keys that were generated in some way from one or more private keys.
- Lightning channels
- Wallet backups
- Lightning channels backups
- Backups of private keys
- Onboarding costs and time
- Operational and maintenance costs
- Web hosting for whatever public/private services one might want to run e.g. a donations page or online store.

Ideally, one should be fully sovereign. This would require that person to **run** their own Bitcoin and Lightning nodes, **manage** their channels, securely **create and store** backups, **connect** their nodes through Tor, **host** their own website with something like Yunohost, **backup** their private keys or seed phrase on metal, and **backup** their Lightning channels states.

However, this situation usually requires deep **technical expertise** and **time** commitment and incurs high **costs**. Additionally, there are risks: if something goes wrong and one loses their funds there is no CEO or customer service department of Bitcoin whom one can call. Sovereignty's other side is personal responsibility. 

Naturally, therefore, compromises must be made. But some aspects shouldn't be compromised on, perhaps more importantly it should be ensured that the user remains in control of their own private keys and only the user knows what the private keys are, i.e.  _`giveBTC` tries to be a repositor of what services and tools allow the user to custody their own keys and make decisions about tradeoffs while receiving bitcoin donations.

Another compromise the app should not make relates to privacy. Consider reading [A beginner's guide to Bitcoin privacy](https://bitcoiner.guide/privacy/) for a list of the main things users of Bitcoin should keep in mind.

The fundamental question of tradeoffs in Bitcoin is with respect to trusted third parties. Bitcoin users should answer for themselves the question: "Who am I trusting for the various aspects of my Bitcoin usage?" Having some idea of the answers to these questions is important because history shows that *trusted intermediaries are security holes*'

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

> A key criteria of tradeoffs that I see is with Bitcoin only, private keys are only required to spend, and can be kept offline. Lightning requires private keys to online (or at least some) which means more complications to manage the higher risk. (@ChristopherA)

## What are the pain points in Bitcoin usage that a donation app/service should address?

    - Difficulty of installation for a non-technical activist?
        - Avoiding loss of funds by the activist.
            - Donors should have a reasonable funnel and not give up because of user interface difficulties. If a donor logs off without completing their donation, the activist has lost funds.
            - The activist should not have to keep a hot-wallet online. If a hot-wallet is accessed by a third party, the keys it records can be stolen.
    - Avoiding loss of funds by donors.
        - Donors should have high confidence that when they complete a donation it goes to the intended activist.
    - Ease of accounting.
        - The activist should be able to collate and record their receipts. Different activists will be in different jurisdictions and have varying reporting and accounting requirements. A donation app should allow them to satisfy these requirements.
        - A donor should see a simple invoice that they can keep for their own records. At a minimum, they should see the transaction hash and the `nym the donor has chosen to use.

## <a name='features'>What features are wanted?</a>

- Ability to pay to an on-chain address without address reuse.
    - E.g. <http://hexawallet.io>'s donation account functionality?
- Ability to pay to a Lighting ⚡ invoice using e.g. LNURL-pay in addition to Lightning Invoices (BOLT-11).
- Privacy by default. In particular:
  - No address reuse.
  - Tor-gapped so that hosting can't be targeted.
  - Only the user, should be able to control the addresses generated by the app.
-  Low cost of maintenance.

---

## Use Cases

### Sebastian - the human rights activist

Sebastian is a human rights activist in Romania. He has limited access to the traditional banking system and resorts to Bitcoin for receiving donations, paying contractors, and covering daily expenses. He also has a very busy schedule, so he enjoys how convenient `app` is. Sebastian didn't need to learn a lot of things to be up and running with giveBTC.

## Alice using `app`

- Alice is a women's rights activist who wants to receive Bitcoin ₿ donations non-custodially.
- Alice does not have a server. She is not a technical person or power user. She does not have capacity for complicated accounting.
- On `app`, she can create an account with her public key and a signature of her public key as input.
    - Alternatively, she can run a simple script on a hosting provider like Linode and quickly stand up her donations age.
- She is directed to a donation widget that she can customise.
- She can then share a link to this widget or embed it in a blog.
- The widget gives Alice a real-time listed of her addresses and donations to those addresses.
- The widget allows her to export all her keys whenever she wants.

## Charlie using giveBTC.app to donate to Alice.

- Charlie uses a link from Alice to go to her donation page.
- He can choose a currency and amount he'd like to donate.
- He is presented with a unique URL (qr code) that contains both the address and the amount in sats to donate. 
- He scans the qr with his wallet (or taps the URL which opens his wallet) and makes a donation.
- The widget tells him that his donation has been successfully received.


Bitcoin Simple Property RFC
===========================

Motivation
----------
Bitcoin is usually described as a new kind of currency. It is in fact a public ledger that can be used to create a digital property and control its ownership inside the blockchain. To date number of concepts emerged in this field, [Colored coins](http://wiki.bitcoinx.org/) and [Mastercoin](http://www.mastercoin.org/) being the most popular. Both of these innovative approaches face their own set of issues. I propose a new simple digital property protocol addressing those issues, while keeping many of the nice features of both concepts.

Advantages
----------
Colored coins match the digital property ownership with individual outputs of bitcoin transactions so one can't spend these coins without losing the digital property ownership. Proposed Simple property matches the ownership with a bitcoin address and it even allows the balance of the address to be zero and still retain the property ownership. Colored coins require dedicated client application to carefully handle the outputs while Simple property can be used with existing clients.

Mastercoin is a protocol too complex for a simple digital property control and also requires a special client application. Its [Exodus address](http://blockchain.info/fb/1exodu) is picked and controlled by its creators (and so is the Mastercoin itself), introducing a possible point of failure. Bitcoin simple property is much simpler and allows anyone to create and control their own Exodus address (called the Origin Address).

Definitions
-----------
###1. Origin Address###
Any bitcoin address can act as an origin address. Origin address is used to issue the digital property and record its transactions.

###2. Funding###
Funding is later used to create the digital property during the issuance process. A bitcoin transaction is a valid funding transaction if:
* it is the first or one of the subsequent payments to the origin address until the first issuance transaction is made and
* at least one of its outputs belongs to the origin address.

###3. Issuance###
All issuance transaction outputs that don't belong to the origin address represent the digital property. Each satoshi represents one unit of the digital property. A bitcoin transaction is a valid issuance transaction if:
* it is the first or one of the subsequent payments from the origin address until the first trade transaction is made and
* all of its inputs belong to the origin address and
* at least one of its outputs doesn't belong to the origin address.

###4. Trade###
A trade transaction moves the digital property ownership from one bitcoin address to another. A bitcoin transaction is a valid trade transaction if:
* none of its inputs belongs to the origin address and
* at least one of its outputs belongs to the origin address (this is called the marker payment) and
* at least one of its outputs doesn't belong to the origin address and
* sum of the digital property-carrying inputs equals the sum of the outputs that don't belong to the origin address.

Marker payments don't transfer the property ownership, they just mark a bitcoin transaction as a Simple property trade transaction.


All other bitcoin transactions are ignored.


Infrastructure
--------------

###Client Integration###
Bitcoin simple property doesn't require client integration. If the client allows disabling change addresses, not even the [Coin control](https://bitcointalk.org/index.php?topic=144331.0) is needed. Issuance and trade transactions can be created manually in existing clients. To make this process easier in the future, [payment requests](https://en.bitcoin.it/wiki/BIP_0070) for issuance and trade transactions can be generated via a web interface and then verified and processed by existing clients.

###Trading & Exchange###
This proposal does not include any advanced exchange mechanism. Blockchain is not suitable for a high-speed, large scale trading due to its slowness and transaction cost. This is also the reason why the [trade contracts](https://en.bitcoin.it/wiki/Smart_Property) are not included in this proposal.


Comments
--------
Please discuss the proposal in this thread: https://bitcointalk.org/index.php?topic=332600.0.







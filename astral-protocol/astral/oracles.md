# Oracles

A vital part of the Astral protocol is the integration of an **Oracle** system that can **trustlessly** fetch spatial data from multiple sources into an immutable registry. Spatial data incoming to the Astral Protocol has many different categories:

* Satellite data
* Ground sensors data
* GPS data
* And many  more

Each one of these sources is prone to failure and subject to cheating. Due to the potential spatial economies that can be built with our protocol, it is paramount to have multiple data sources for each of these categories of data. Taking the example of the GPS data, it is widely known how spoofable the system is. The usage of a protocol such as [FOAM ](https://foam.space/)in combination with GPS data can provide a more reliable and trustless measure of the position of an object or a person in the real world. Combined with other methods of validating one's position, such as biometrics, it is possible to reduce to a great extent the possibility to cheat the system.

In addition to the different data sources, the usage of multiple Oracle networks, such as [Chainlink ](https://chain.link/)or [API3](https://api3.org/), as the gateway to the **Astral Protocol** will further reduce the possibility of mutability of the data and the potential of failure of any of the aforementioned networks.


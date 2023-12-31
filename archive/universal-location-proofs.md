# Universal Location Proofs

Technically it is extremely difficult (if not impossible) to create a definitive proof that some information was created at a specific physical location.

There are technical ways to improve trust in the position - signing position captured by the sensor triangulating with the GPS or FOAM network in a secure enclave, for example. It would require a special app or - eventually - a plugin for mobile crypto wallets that allows users to generate the “universal location check-ins” (credit @jabyl from Distributed Town for his help thinking this through).

Additional layers of trust could be built on a location by incorporating other sensor readings (like from a camera or microphone), as could requiring users to scan a cycling QR code only available at the location, form social check-ins in which they verify that the others were present, etc.

We’ve been doing some early thinking about zero-knowledge location proofs as well, which prove that a point is inside a polygon without revealing the user’s position. This could then be verified on chain, enabling location-based smart contracts that preserve the user's privacy. Applications include local currencies, intelligent mobility systems, dynamic game preserves, detecting illegal and unregulated fishing in Maritime Protected Areas, location-anchored games and a lot more.

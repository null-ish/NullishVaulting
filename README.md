# NullishVaulting
The Nullish Vaulting Method is a technique that allows users to store uninscribed satoshis below ordinals in a novel and secure manner.

[Example 1](https://gamma.io/inscription/34c82078494a7f4f27e8780d75282764a6e84fb52635af756ac19e542325b2bci0) | [Example 2](https://gamma.io/inscription/fc096fefcc8ca64ee1b6a783848b02e65dca2ede5198c0efcf99190425b0ad71i0) 


# Templates
* [Uncommon SVG Template (1.5kb)](uncommon.svg)

# Vaulting Tutorial
## Step 1: Wallet Creationg & Importing
1. Create your inscriber wallet with ord:<br>`ord --wallet walletName wallet create`<br><br>
2. Get your receiver address with ord:<br>`ord --wallet walletName wallet receive`<br><br>
3. Import the key into Sparrow with Taproot derivation settings.

## Step 2: Send UTXOs into the wallet
Make sure your wallet has 3 UTXOs:
[<b>Never have more than 1 uncommon in your wallet when inscribing, as the other uncommons might get used by ord to pay the inscription fees</b>]
1. Small amount of sats (1,000+ sats ideally, more will work too)
2. Uncommon sat with padding after it.
3. Large amount of sats (this is for fees, so we will use 1,000,000 sats as an example)

## Step 3: Sandwiching the Uncommon Sat
1. With Sparrow, select all 3 outputs.
2. Make sure the outputs are in this order as inputs:
```
1. Small amount of sats (1,000+ sats ideally, more will work too)
2. Uncommon sat with padding after it.
3. Large amount of sats (this is for fees, so we will use 1,000,000 sats as an example)
```
![Sparrow transaction example](https://i.imgur.com/lgm9DJh.png)


## Step 4: Inscribe the Vault
1. Once the sandwich transaction is confirmed, you can find the satpoint of the uncommon with `https://ordinals.com/sat/XXXXXXXXX` and view the location.
2. The location of the uncommon will look like this: `SANDWICH_TX:0:NNNNNN` - Note that the ord explorer only displays locations for uncommon sats.
3. You will need to use the satpoint right before NNNNN (NNNNN - 1) to inscribe the sat BEFORE the uncommon. This will leave the uncommon at the index 2 of the inscription.

Use a command like this (without the <>):
```
ord --wallet walletName wallet inscribe --destination bc1pxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx C:\...\uncommon.svg  --satpoint SANDWICH_TX:0:<NNNNNN-1> --fee-rate 50
```

I personally use Greg's ord version: https://github.com/gmart7t2/ord

It allows for a command like this:
```
ord --wallet walletName wallet inscribe --destination bc1pxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx C:\...\uncommon.svg --satpoint SANDWICH_TX:0:<NNNNNN-1> --postage "20000 sats" --fee-rate 60 --dump
```
(Postage allows for larger padding for your inscription, and --dump makes sure it saves the private keys of the commit transaction to ensure your sat doesn't get lost if the commit transaction gets stuck)

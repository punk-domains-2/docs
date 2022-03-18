---
order: 30
icon: flame
image: ./static/old-new-domain-image.png
---

# Punk Domains v2 coming soon!

We're adding new exciting features to Punk Domains and making it more gas efficient. 🤘

Let's take a look at what's coming.

### 1. New default domain image

The most **visible** change is a new default domain image. We're replacing the old one with black background, with the new one that has our brand colors (as gradient) as a background.

![](/static/old-new-domain-image.png)

We feel this will make punk domains stand out more in NFT marketplaces! 🔥

### 2. Replacing `transfer()` with `call()`

Ok, this one is a bit more technical. 🤓

In v1, payment transfers were done with the `transfer()` method. We're replacing this method with the `.call{value}` method, which provides more flexibility to TLD owners (the ones that are contracts) through the fallback mechanism. 

Additionally, we've added a ReentrancyGuard mechanism, which is often necessary for `.call{value}` methods.

### 3. Gas optimizations ⛽

In order to reduce gas costs and make our contracts more lean, we've removed the `url` and PFP fields as separate fields in domains. 

<iframe src="https://giphy.com/embed/1uXj5hl0EMj0Tfe8Ub" width="480" height="360" frameBorder="0" class="giphy-embed" allowFullScreen></iframe><p><a href="https://giphy.com/gifs/dad-dude-basic-1uXj5hl0EMj0Tfe8Ub">via GIPHY</a></p>

Instead, both URL and  profile picture data can be defined in the **custom data** field, which is a very flexible data structure within the Domain struct.

### 4. Referrals

Away from the very technical subjects and onto something we think you'll all love! Now **you can get paid for referring** Punk Domains to others!

Each TLD will now have a referral system, which means that a certain percentage of a domain mint payment could go to a referrer (if TLD owner sets the referral fee above 0%). 

The **default** referral fee is 10%, but the owner can set it to any number between 0% and 50%. The TLDs owned by Punk Domains will have the referral fee at 10% at the start.

### V2 Deployment

Note that changes are not yet live. We will be deploying new v2 contracts **gradually** across the supported chains.

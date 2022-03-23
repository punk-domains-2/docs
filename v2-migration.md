---
order: 90
icon: flame
image: ./static/old-new-domain-image.png
---

# Punk Domains Version 2 (migration completed)

> Punk Domains has migrated to version 2. If you've minted domains in V1, you'll automatically get new ones. Old ones will be marked as deprecated, so just ignore them. All newly created domains are now v2 domains.

We have added new exciting features to Punk Domains and making it more gas efficient. 🤘

Let's take a look at what's new!

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

Each TLD now has a referral system, which means that a certain percentage of a domain mint payment could go to a referrer (if TLD owner sets the referral fee above 0%). 

The **default** referral fee is 10%, but the owner can set it to any number between 0% and 50%. The TLDs owned by Punk Domains will have the referral fee at 10% at the start.

> How do referrals work on Punk Domains website? 
> 
> Simple! Just add `?ref=0xYourAddress` or `?ref=your.domain` to the URL and the website will remember you as a referrer. So next time you mint a domain (on v2), you should be able to see in block explorer that you have received a referral fee (on testnets it's 10%).

![](/static/referrals.png)

### V2 Deployment

Punk Domains has (as of 23 March 2022) migrated to version 2. If you've minted domains in V1, you'll automatically receive new ones. Old domain NFTs will be marked as deprecated, so just ignore them. 

All newly created domains are now v2 domains.

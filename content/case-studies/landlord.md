---
title: Keeping a finite world playable
subtitle: Landlord Real Estate Tycoon - supply scarcity and the first session
---


---

## TL;DR

- Landlord is a multiplayer, location based, tycoon game that used real world data to create engagement for players around the world.
- 25M+ downloads, real time worldwide transactions.
- Issue was the scarcity of properties (and its shares) for new players.
- We've added systems that monitor and adjust properties around new players.
- D1 retention +2-3pp, massive amount of positive feedback.

---

## The product

- Game based on real life properties - Google Maps / OpenStreetMap APIs; NASA light pollution API as a factor of property value + check in data from Google/Foursquare.
- 25M+ downloads, studio flagship title.
- Players buy, trade, bid on real properties around the world. Properties are divided into 1000 shares that accumulate to 100%.
- **My role:** Product Manager/Product Owner, led a team of up to 15 people fully liveopsing the title for 6 years.

---

## The loop, and why it choked

**Loop worked.** More players → more fierce competition for the same properties → rarity increases the value → owning true Apple HQ becomes a status good → engagement and spend grows. Product was more interesting and bid wars were more engaging the more players were playing.

**And that's why it choked**. Real properties = finite supply. We can't build more real properties and we can't afford to wait for real life developers ;). 
The better the loop worked, the emptier the shelf for new players. Especially in big, popular cities. So eventually we've reached a state where there was a high probability that starting in a Capital City was making the start of the game unplayable. 
For example **Berlin (85% of ALL shares in properties bought)**.


![[mermaid-diagram.png]]

---

## How we saw it coming


- We had a system that was calculating the amount of shares available in properties throughout the city, it was a live system recalculating 2-3 times per day.
- We had a possibility to check any given area/city on demand and we did that **before every big UA spend** in targeted countries.
- I saw a lot of negative reviews from players - ***"I can't progress because I don't have cheap properties around me"***, ***"Can't start playing, all properties around me are bought up"***. 
- Technically it was possible to play using marketplace (real time bidding against other players) but it was extremely hard and inefficient at lower levels.


---

## What we changed

### Geo-scoped surfacing

We've been showing the cheapest properties for new players that recently joined the game.

*Why: First session is extremely important and it can't depend on the marketplace feature where players might not even be able to compete.*


### Expanding search radius

Radius was automatically expanded if the game was not able to meet the criteria for new players (at least X properties that have free shares and are in a given price range).

*Why: We had to compromise between the "known" properties that player immediately recognizes as something close to their location and player has a thing to buy. I usually focused on the former because of the way our players engaged with the game, but in this case I've made an exception.*

### Reclamation from inactive players 

The most lucrative properties were sold to the market through our Marketplace or immediately to the bank if a player was inactive for more than 30 days.

*Why: Supply was frozen in the portfolio of inactive players so we had to make sure that it wouldn't rot there for eternity. This was not a perfect feature and it was done as a last measure.*


### Charles Landlord 

We've created a landlord persona - **Charles**. He was teaching new players how to play and allowing them to purchase his own artificial property as a FTUE mechanic that was later repurchased by him and the player earned a profit.

*Why: I wanted to add more narrative depth into the game and this idea of a cheeky, old, bald landlord was working quite well in our promos and marketing materials. Idea was to have a proper and 100% bulletproof mechanic for our new players so that even if the scarcity of properties was extreme in a specific location that player would still be able to start playing and earn some progress thanks to Charles.*

---

## What moved

- Negative reviews such as "I don't have anything to buy" **practically disappeared** - closest proof for what we tried to fix.
- **Retention D1 rose 2-3pp**.
- Additionally (which wasn't planned): reclaiming properties from inactive-player mechanic - which was set up to launch first day of each month increased the revenue by 2-3x above the average on those days, without any promotion available.

---

## How I'd measure this today

- **What we didn't do:** we measured before/after on cohorts, we didn't do a controlled AB test.
- **Why:** We didn't have tools setup, issue was increasing in time so we had to act quickly. I went with my gut that those mechanics would work. The time pressure on the delivery was extremely high.
- What it does not prove: seasonality, a freshness effect, changes in the traffic mix.
- How I would approach it today: OEC, guardrails, decision criteria set up front, holdout.

---

## What I'd do differently

- The share monitoring system should be an integral feature from the very beginning of the game and not added later (we definitely lost a huge amount of players because of this). All of those 4 systems that we introduced were not added at the same time so it was a long and costly production pipeline.
- The reclaiming shares system was a blunt tool that lacked any finesse. We had a multitude of situations where players were coming back after 3-6 months and they were lost immediately because we sold out their portfolio.
- The easiest solution would be to introduce more shares for properties with a specific printing mechanic that would allow us not to sell out properties from inactive players. I did that in Landlord's successor -> **Landlord GO!** however it didn't work quite as planned, which stopped us from doing something similar in Landlord. Properties had a sentimental value to players, and owning 100% of them was a great achievement for players.
---
title: Finding the leak
subtitle: Sequence - diagnosing and fixing the first-time user experience
---

## TL;DR

- Sequence World - a mobile f2p adaptation of a Goliath board game.
- 63% of all players dropped after `first_open`.
- Found issue with incorrectly tracked `first_open` event.
- Technical issues connected to our internal asset server and session timeout.
- D1 retention from **22% to 30%**, FTUE completion rate from **22% to 50%**.

---

## The product

- **Sequence World** - a mobile adaptation of a highly popular, old school, board game. Very popular in the US - selling millions of copies worldwide. 
- My role: **Product Owner** - responsible for economy, features/systems, monetization, analytics,  and led a team of 12.
- Context: **Players arrive from both mobile world and board game world**, some of them know the rules already and still have to go through digital onboarding.  

---

## Where the funnel leaked

The chart below showcase two points of friction:
- The first was extreme loss of players right after the First Open event.
- The second was during first match. 

![[onboarding-before-light.png]]


---

## Two possibilities, both true 

We immediately went with technical issue which was a correct direction but unfortunately it wasn't really reproducible with our current capabilities. It wasn't tracked down by our devs.

Since we already had tunnel vision on technical issues, there were two hypotheses I thought could be possible.
- our internal asset server was somehow not working correctly - game downloads a few assets at the beginning of the game, typical of most games now.
- SDK init was failing but we didn't see any data on it yet.

**We started with SDK init because asset server was working flawlessly in other projects - which turned out to not be true because it was indeed wrongly implemented.**

We had to add more granulation to our event funnel with additional parameters to ensure that we had all the knowledge. I've designed a structure and we implemented it as below. 

![[loading-init-light.png]]

We can see here that our session timeout feature was not working correctly. We should not lose players on this step (at least not as many).

![[asset-server-before-light.png]]

We can see here that we were losing players on our internal asset server step.

---

## What we changed

- We've fixed implementation of the asset server, and changed the way we downloaded assets, so now at the start we only downloaded mandatory files, so it was much quicker. The rest of the files were downloaded throughout the tutorial.
- Timeout was wrongly implemented and was creating a scenario where players were stuck and couldn't do anything (wrong timing 5s changed to 20s, and wrong behaviour).

---

## What moved — and what didn't

- We've managed to decrease the number of players lost from **63% to 12%**.
- FTUE complete rate moved from **22% to 50%**.
- D1 retention went from **22% to 30%**.
- We didn't address the issue of players dropping mid-game, but that was the decision to focus on the beginning of the game.

The chart below showcase the improved FTUE.

![[onboarding-after-light.png]]

---

## Measurement, honestly

- We measured data before/after.
- Different UA traffic could affect the outcome, but we were focused on T1 US market so it wasn't really a big issue.

---

## What I'd do differently

- I would make sure that we only download assets that are necessary for tutorial.
- Adding more granulation from the start would be my best bet for the future in terms of FTUE.
- We had an issue with the `first_open` event - it was duplicated and our funnel was basically lying to us (our internal `first_open` was logged **AFTER** loading events). So we saw percentages and thought all was good, but once I dug deeper into numbers I found out that it was incorrect. In the future I would make sure that `first_open` is always default from the analytics provider.


---
layout: default
title: Administrator's Guide
nav_order: 4
description: A more detailed guide for admins/staff of servers using GriefPrevention
---

# Administrator's Guide
{: .no_toc }

You probably don't need to read this entire document just to get started with GP on your server. GP does almost all the work for you, so just try it out and come back here when you can't figure something out. :)

## Table of Contents
{: .no_toc .text-delta}

- TOC
{:toc}

---

## Administrative Claims

Required Permission: `griefprevention.adminclaims`

"Administrative" claims are reserved areas which are owned by "the administration" rather than a specific player. They don't cost any specific player blocks to create, and any player who has permission to create administrative claims also has permission to modify all administrative claims. If you want to grant all players permissions in these claims, remember you have `/accesstrust public`, `/containertrust public`, and `/trust public` available. If you want to prevent players from making claims in an area without impacting their ability to build there, place an administrative claim and then use `/trust public` while standing inside it.

Creating, deleting, and building within public claims requires the `griefprevention.adminclaims` permission. Use `/adminclaims` to switch to administrative claims mode, and `/basicclaims` to switch back to basic mode. The shovel works for admin claims just as it does for private claims. Use the permission to regulate building in and creation of these.

## Changing Player Claims

### Overriding

Required Permission: `griefprevention.ignoreclaims`

Any player with this permission may gain access to any non-administrative claim using the `/IgnoreClaims` command, allowing them to build, break, and change permissions (trust, untrust, etc). Admin claims still require the `adminclaims` permission. Use `/IgnoreClaims` again to go back into "respecting claims" mode, to prevent accidental changes to others' builds. Individual actions taken in ignore claims mode aren't logged, so don't give this permission to anyone you don't trust 100%.

### Deleting and Resizing

Required Permission: `griefprevention.deleteclaims`

Use `/deleteclaim` to delete the claim you're standing in, even if it's not yours (deleting public claims additionally requires the `adminclaims` permission). Use `/deleteallclaims <player>` to delete all of a specific player's claims, for example to remove claims for a player who's been banned.

GriefPrevention doesn't automatically remove claims for banned players because many servers have a ban appeal process. If you want an easy combo command, use your commands.yml (see documentation on the Bukkit wiki) to alias your /ban command so that it BOTH bans the player AND deletes all his claims (you can even through in a `/deathblow` if you like).

Anyone who has the `griefprevention.deleteclaims` permission may also resize another player's claim using the golden shovel as if it were his own claim. The owner's claim blocks will be added or subtracted as appropriate. There's not a separate permission for resizing because resizing essentially makes un-claiming any block possible (same as delete).

All deletions and resizes (except by the claim owner himself) are logged.

## Creating Claims for Players

Anyone with both the `griefprevention.adminclaims` permission and the `griefprevention.transferclaim` permission may create a claim for another player by first creating an administrative claim with `/adminclaims`, then using `/transferclaim`. This is the only way to create a private claim which is less than the minimum claim size. The `/adminclaims` command is discussed in more detail above.


## Adjusting a Player's Claim Limit

Required Permission: `griefprevention.adjustclaimblocks`

You may use `/adjustbonusclaimblocks <player> <amount>` to add or reduce the claim blocks available to a player. You might use this as a reward for winning a competition or creating a really impressive build, or as a monetization strategy to help offset your server expenses (charging real money for bonus claim blocks). Unlike accrued claim blocks which are limited by a config variable, there's no limit on bonus claim blocks.

You may also grant bonus claim blocks based on permissions. For example, `/acb [myservergroups.builders] 5000` (make sure to include the square brackets) to grant everyone with the `myservergroups.builders` permission 5,000 claim blocks. This is not a one-time operation - players who get the permission in the future will also get the bonus, and will lose the bonus if they lose the permission.

You may also set accrued blocks with `/adjustaccruedclaimblocks`.


## Investigating a Player's Claims

Required Permission: `griefprevention.claimslistother`

The `/claimslist <player name>` command will list all of a player's claims along with their sizes and locations, and summarize the claim block math for you.

## Investigating a specific claim

Equip the investigation tool (stick by default), and right click the claimed area.

## Fighting Wilderness Grief (World Repair)

Required Permission: `griefprevention.restorenature`

"Public grief" is the kind of grief a player inflicts on the world rather than on a specific individual. It includes forest fires (not possible with GriefPrevention installed), tree topping (also not possible with GP installed), terrain damage, and intentionally ugly builds. The `/restorenature` command addresses the last two by empowering an administrator to very quickly revert player-generated changes with a simple right-click. To enter restoration mode, equip your claim tool (golden shovel by default), use `/restorenature`, then point at the problematic area and right click. Put your shovel away to exit that mode. Don't worry, you can't restore nature inside someone's claim, so it's safe to use anywhere. It won't fill a big crater - for that, you need `/RestoreNatureFill` (see below).

Required Permission: `griefprevention.restorenatureaggressive`

Usually, griefers spent a lot of time digging on the surface to collect the blocks they use for their wilderness griefing, leaving a big hole. This is extremely easy to fill-in with the `/RestoreNatureFill [radius]` command, which turns your shovel into a filler tool. Just right-click at the level you want to fill to! Hours of griefer effort can be remedied in seconds.

For the rare griefing cases where griefers use natural-looking blocks to grief (like enormous smooth stone or leaf penises), you'll need the `/RestoreNatureAggressive` mode. It will remove even some natural blocks, so it must be used carefully. It only removes blocks at and above the level you click at. So point at the bottom of the grief, and not any lower. Since it will remove various natural blocks with air below them, you can quickly remove a large stone, leaf, ore, or log construction by knocking out the bottom layer, and then using `/rna`. You'll also need `/rna` for floating grass blocks. Rule of thumb: Always try `/RestoreNature` first, and go to `/RestoreNatureAggressive` for only the cases where that doesn't work. Just like standard `/rn`, `/rna` will always respect claims. So you needn't worry about using it close to claimed player builds.

Strictly speaking, none of this is "rollback", because GP doesn't spend CPU cycles or hard drive space to maintain history of block changes. What GP really does is remove block types which were definitely placed by players, then scans the remaining blocks to repair ugliness like unnatural terrain and surface stone. Please be careful with other tools that promise to roll back or regenerate for several reasons:

* Regenerating a chunk is a BAD idea if world generation code has changed since the chunk was originally generated. This can happen with Mojang patches, world seed changes, and world generation plugin installations / updates / removals. In this case, you may get an entirely NEW chunk which doesn't match the surrounding chunks, like a snowy square in the middle of a desert. 
* WorldEdit promises to only regenerate within your selection. Really, it regenerates entire chunks, then does its best to "undo" the changes made outside of your selection area. This code is tough to keep correct as Mojang updates the game, so you may end up accidentally changing areas outside of your selection area due to a bug. `/RestoreNature` never changes land claim blocks in the first place, so there are no concerns around trying to put them back the way they were after an unintended change. 
* Regenerating will blocks back that maybe you prefer stay gone, like already-looted dungeons and veins of ore. 

Always start with safe `/RestoreNature` and only use other tools if you're comfortable with the risks.

## Fighting Chat Trolls

Required Permission: `griefprevention.softmute`

Banning a chat griefer ("troll") who's trying to start arguments often prompts that player to escalate - he may return on one or many other accounts to grief more subtly, recruit other badly-behaved players to join the server, or even launch a DDOS attack to make your server temporarily unavailable. The `/SoftMute` command will mute the player but still allow him and other `/softmute` targets to see his messages, so that he doesn't know you've blocked his "attack". Because he thinks he's effectively trolling, he doesn't escalate, and eventually leaves quietly on his own, none the wiser. For bonus points, you've wasted his time and frustrated him because no one seems to be taking his bait (it's the least he deserves).


## Killing Drama

Required Permission: `griefprevention.separate`

If two players just can't get along, you can fix it with `/separate`, which forces those players to ignore each other. They won't know they're ignoring each other, either. It's a simple, effective, and instantaneous fix for emotional battles that annoy the disinterested and often suck in more of your player population over time. You may undo `/separate` with `/unseparate`.


## Reviewing Chat Logs Efficiently

You'll find abridged logs under `plugins\GriefPreventionData\Logs`. They're formatted for easy reading and only include social interactions between players. They're automatically deleted after 7 days so you don't have to throw away the old stuff manually. GriefPrevention's config file includes options around this feature, including changing the expiration period and putting more information into the logs if you want it.

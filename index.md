---
layout: default
title: Home
nav_order: 1
permalink: /
---

# Home

## GriefPrevention Docs

**Currently under construction; in the meantime, documentation currently lives [here.](https://github.com/TechFortress/GriefPrevention/wiki)**

Official documentation for the GriefPrevention Bukkit plugin. Get started with the page directory on the left, or find what you're looking for with the search bar at the top.

---

GriefPrevention is a Minecraft server plugin which stops grief before it starts automatically without any effort from administrators, and with very little (self service) effort from players. Solve all your grief problems with a single download, no database, and no configuration step (the default configuration is sane and will likely be all you need, but of course everything is configurable and fine-tuneable to your liking).

## Feature List

* No database or world backups required.
* Extremely efficient CPU / RAM usage.
* Land claims are easy to manage.
    * Players create and manage their own land claims, so you don't have to do it for them.
    * New players get automatic claims around their first chests so they're protected even if they don't know how to create land claims yet.
    * Players who ask for help in chat get an instant link to a demonstration video.
    * Resizing claims and creating new claims is done with ONLY the mouse, no slash commands (slash commands are also available).
    * When a player appears to be building something nice outside his claim, he's warned and shown his claim boundaries.
    * Claim boundaries are easy to see, and don't require any client-side mod installation.
    * Extremely easy-to-remember, single-parameter slash commands for giving other players permissions.
    * Claim subdivision and granular permissions are available to organize towns and cities. <a href="http://www.youtube.com/watch?v=I3FLCFam5LI">Watch this video.</a>
* It's IMPOSSIBLE to grief a land claim. Watch <a href="http://www.youtube.com/watch?v=RWekSeMi1OE">this video.</a>
    * No building or breaking.
    * No stealing from ANY containers.
    * No sleeping in beds.
    * No button/lever usage.
    * No adjusting redstone repeaters or other configurable blocks.
    * No pushing blocks in with pistons.
    * No pulling blocks out with pistons.
    * No TNT damage (including cannons).
    * No creeper damage.
    * No explosive damage from other plugins, like Extra Hard Mode or Magic Spells.
    * No enderman/silverfish block changes.
    * All doors may be automatically locked (optional, see config file).
    * No killing or luring animals away.
    * No stealing water (e.g. buckets).
    * No trampling crops by players, animals, or monsters.
    * No building overtop, all claims reach to the max build height.
    * No placing or breaking paintings / item frames / armor stands, etc.
    * Fluids will not flow into a claim from outside.
    * No placing blocks via TNT/Sand/Gravel cannon.
* Pets and death loot are protected.
    * Players can't pick up what another player dropped on death without permission (configurable, of course)
    * All types of pets can be protected everywhere, even outside of land claims (can be configured per-world).
* Excellent anti-spam protection
    * Warns, then mutes, then may kick or ban spammers (configurable - you choose).
    * Most spammers get only one message out before they're muted.
    * Blocks server advertising (IP addresses).
    * Blocks repeat message spam.
    * Blocks ASCII art (ex. Nyan Cats) spam.
    * Blocks similar message spam.
    * Blocks unreadable (gibberish) message spam.
    * Blocks CAPS.
    * Blocks macro spam (very different messages in quick succession).
    * Blocks login/logout spam, even when the spammer has multiple accounts.
    * Blocks death spam.
    * Blocks bot team spam.
    * Blocks slash command spam, including /tell, /emote, and any more you add.

* Wilderness Protection and Rollback
    * Fire doesn't spread or destroy blocks.
    * Creepers and other explosions don't destroy blocks above sea level.
    * TNT doesn't destroy blocks above sea level.
    * No planting trees on platforms in the sky ("tree grief").
    * Instant, point and click nature restoration for not-claimed areas. Watch this video.
        * Insanely easy and fast fixes for penises, swastikas, and anything else unsightly.
        * Point at what you don't like and click, and it's fixed. Even from far away.
        * Never accidentally changes blocks inside land claims.
        * No need to investigate who built it, who broke it, or when they did it.
        * Doesn't matter if the griefer built with "natural" blocks, it will still be fixed.
        * No database.
        * No backups.
        * No chunk regeneration (it's dangerous for technical reasons).
        * Fixes bad chunk generations, like floating islands. It will be better than new.
        * Fills holes, even next to water to correct big spills.
        * Smooths noisy terrain.
        * No griefer construction is safe. If it's unnatural enough to be noticeable by players, it will be removed or filled-in.

* Land claims can't be used as a griefing tool.
    * It's impossible to get a player "stuck" inside a land claim.
    * Land claims beyond the first require a golden shovel.
    * Minimum claim size prevents sprinkling small claims to annoy other players.
    * Max claim allowance grows with time played on the server, and can't be cheated by idling.
    * A simple administrative slash command will instantly remove all of a griefer's claims, no matter where they are.

* Catches clever griefers.
    * Enhances the /ban command to ban ALL a griefer's accounts (not just his IP address).
    * Logs sign placements.
    * /SoftMute command to shut down chat trolls without them knowing they're beaten.
    * Abridged chat logs make reviewing what happened while you were away super-quick and easy.
    * Automatically mutes new-to-server players who use racial or homophobic slurs.

* PvP Protections.
    * When PvP is off, no setting fire or dumping lava near other players.
    * Absolutely bullet-proof anti-spawn-camping protection including bed respawns, which requires no configuration.
    * No logging out, stashing items, or using plugin teleportation to escape combat.
    * Optional siege mode, to answer players who hide in their claimed houses to avoid combat.

* Supports your server growth.
    * Permit players to exchange server currency for claim blocks (requires configuration and other plugins).
    * Grant claim blocks automatically for votes, donations, etc (console command provided, other plugins required).


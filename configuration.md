---
layout: default
title: Setup+Configuration
nav_order: 3
description: How to configure GriefPrevention to your particular requirements (although the defaults will suit most!)
---

# Setup+Configuration
{: .no_toc }

## Table of Contents
{: .no_toc .text-delta}

- TOC
{:toc}

---

<!-- may want to add link to YAML parser -->
Unless you have BOTH creative/survival or PvP/non-PvP worlds on your server, then you do NOT have to configure GriefPrevention to get maximum protection without issue - the defaults should be suitable.

However, this page attempts to detail the available configuration settings you may wish to tweak, if you need to tailor GP's behaviour to your requirements.

If you have such a complex server configuration, or if you're interested in reducing protection or tweaking some settings, keep reading. Otherwise, just copy/paste the JAR into your plugins folder and /reload; a default config will be created for you.

If you update a config file, you can use /gpreload to reload the config. This does NOT completely reload the plugin, so if you download an updated JAR file, you still have to /reload or reboot your server to get all the changes.

---

# Limiting Which Worlds GriefPrevention Runs On

Use the `claims.mode` configuration variable to list which worlds players may create claims in. Options are `Survival`, `Creative`, `SurvivalRequiringClaims`, and `Disabled`.

When you disable land claims in a world, most of GriefPrevention's features turn off for that world as well. There are very few exceptions, for example anti-spam.

Beware - if you set a world to `Disabled` which already includes some land claims, those land claims will stop protecting the blocks inside. You can use this setting, for example, to turn off GP land claims in a Factions or Towny world.

Warning about `SurvivalRequiringClaims`: This is designed for survival servers which have a designated resource-gathering world. Because claiming land without building first requires a golden shovel, you may want to either set an easier-to-get claim creation tool (see config), or add other plugins to make the golden shovel more accessible to your players. Also remember that you can modify `messages.yml` to customize GriefPrevention's help messages so that they're more helpful to the players on your not-so-standard server. Finally, remember that a player could potentially claim land, build/break stuff, then move his land claim. You can discourage this using GriefPrevention's config file option to have players lose some or all claim blocks used in a land claim when abandoning the claim. Please do what you can to make this mode work for you - because very few server owners use it, I don't want to overcomplicate it.

---

# Optional Database Configuration

Once you go database, you can't go back to file system without losing any NEW data you created while in database mode. Do NOT assume that you need to use a database for performance reasons. Try with the filesystem first, and I think you will be surprised at the efficiency.  Many fairly large servers are using the flat file storage option with no issues at all.  If you don't know databases or know someone who does, stay away from database mode. It will just make your life more complicated for you. Any data you create while in file system mode can be very easily moved to a database later, if you decide the file system isn't working for you.

If you configure GP for database and there's a problem connecting to the database, many GP features won't work, and others will give you error messages in your log files. When you're enabling database support for the first time, pay close attention to your boot logs.

A database URL looks like this: `jdbc:mysql://localhost:3306/gpdata` . The last bit is your database name, which YOU create manually with a MySQL command like `create database mydatabase;`. If you don't know your username, it's probably "root". Please do not ask me for help with your database URL. This is standard Java-to-database connectivity, and you can find plenty of help for this area on the Internet. I'm also not your go-to guy for permissions problems or anything else related to database maintenance (backups, migrations, data edits, data searches, etc).

If you have data on the file system already, they will be migrated to the database. Please be patient during the migration process, which can take a while. On my test server, it took 7 minutes to migrate 1400 claims and 5000 players from file system to database. Just in case there's any problem, your file system data is NOT deleted, only moved. If you have a problem, you can quickly recover by copying that backup back into its original place and removing the database configuration fields from your `config.yml`. This will put you back on file system mode with all of your data in place.

---

# Complimentary Plugins

## Do I need a block logger/rollback plugin?

In my opinion, no. GriefPrevention will prevent griefers from doing any damage to claimed areas and can very quickly clean up wilderness grief without any database to back it up, so you would only need a rollback tool as a backup plan in case one of your players builds something and doesn't claim it. On my servers, I tell my players that if they don't claim it, that's their problem, and I refuse to babysit them. You may have a different attitude. :) Even if you keep a rollback tool on your server, GriefPrevention will be immensely helpful because it will drastically reduce the number of incidents you have to respond to. And fewer responses means fewer admins, which reduces your risk of accidentally giving a clever griefer admin privileges.

## What about anti-cheating?

I don't consider cheating to be griefing, unless the server is very competitive (as are many PvP servers). If you're concerned about cheating, I recommend the AntiXRay plugin to stop xrayers from taking all the diamonds, and NoCheatPlus to stop wall climbing, fast running, fast break, kill aura, etc. You should disable NoCheat's anti spam, because GP's anti spam is much more effective (and NoCheatPlus may prevent GP from doing its anti-spam job).

If you're allowing theft or have entirely disabled claims on your server, you may want to replace AntiXRay with orebfuscator to not only protect ores, but also keep player builds hidden.

---

# Plugin Compatibility

WorldGuard, ChestShop, Residence, etc

You may be using one of these for some very specific areas, and they provide their own protections in those areas. For example, you might use WorldGuard to create a PvP zone in your non-PvP world. To make sure no one can create a GriefPrevention claim in an area, do the following. First, use `/adminclaims` (detailed below) to create a claim overlapping the area already protected by your other plugin. Then, stand in the area and use `/trust public`. This essentially disables GriefPrevention's protections in that area, while preventing other players from creating any claims there because it's already claimed.

Note that by default, GriefPrevention will not allow a player to create a land claim which overlaps a WorldGuard region he doesn't have permission to build in. You can disable this feature in the config file.

## Player Logout Messages

To prevent spam from bots and determined children, GriefPrevention silences rapid logout/login messages from a player. If the player isn't gone a full 10 seconds, neither his log out nor log back in message will be broadcast. If you're using a plugin which silences or changes logout messages and that plugin appears to stop working when GriefPrevention is installed, ask that plugin's developer to reduce their logout event handling priority to "high" or lower so that GriefPrevention will see that plugin's changes to logout messages and respect them. If you don't want to do that or don't want to wait for the other developer to respond, you can disable this feature in your config file by changing the time span from 10 seconds to 0 seconds.


## Tool Conflicts

Some other plugins might be using the golden shovel or stick. For example, I've heard a Magic Spells plugin uses the stick as a wand. You may use the configuration variables below to customize which tools GriefPrevention uses, but be warned that some players may be confused when the demonstration videos tell them to use a tool that doesn't work as described on your server. Also, be sure to search messages.yml for any help text which might mention the default tools.

`Creation Tool: GOLD_SPADE`

This is the tool players will use to create and resize claims. Administrators will use it for rollback. You'll find details on both below.

`Investigation Tool: STICK`

This is the tool used to visualize a claim by pointing at a build or the ground with the item in your hand and right-clicking.

---

# Land Claim Settings

## Claim Limits

`Claims.InitialBlocks: 100`

The number of claim blocks a new player starts with. Note that if you allow automatic new player claims, those claims can still be larger than this number (the player will just go into negative claim blocks until he accrues more).

`Claims.BlocksAccruedPerHour: 100`

The number of claim blocks awarded to players for each hour of play time on your server. These are awarded gradually (about every 5 minutes), but only to players who aren't just standing around doing nothing (idling).

`Claims.MaxAccruedBlocks: 80000`

The maximum number of accrued claim blocks any player may amass. This number does not limit bonus claim blocks granted by administrators (see above).

`MaximumNumberOfClaimsPerPlayer: 0`

If you set this to more than zero, players won't be able to own more than the number of claims you specify. To exempt a player from this limit, use permission griefprevention.overrideclaimcountlimit, which operators have by default.

`Claims.AutomaticNewPlayerClaimsRadius: 4`

When a player who doesn't have any claimed land places a chest, he automatically gets a claim with the chest at its center. This configuration variable determines the size of that claim (as number of blocks away from the chest, NOT including the chest itself). So the default radius 4 would create a 9 x 9 = 81 total blocks claim, centered at the placed chest.

To protect only the chest itself, set this to zero.

To disable automatic new player claims entirely, set this to a negative number. Before disabling this feature, consider that it's vital to the user-friendly nature of this plugin, because it protects players who don't know how to use the golden shovel or don't have access to a golden shovel yet, and also educates them about the golden shovel. If you disable it, you'll need a plan to educate new players about the golden shovel, for example by posting signs near the spawn.

`Claims.ExtendIntoGroundDistance: 5`

How far into the ground a new claim should extend from the golden shovel location. If the golden shovel is used at two different heights, the lower value will be used in conjunction with this variable. To guarantee all claims run all the way to bedrock, use a very large number. The default doesn't sink to bedrock because that would effectively claim valuable ore that the player placing them claim hasn't discovered yet. Please note! As a player digs or builds underneath his claim, his claim automatically sinks lower with him. Thus, mine shafts and basements are safe from grief even if you set this variable at a small value.

`Claims.MaximumDepth: 0`

Maximum depth claims are allowed to reach. If you set this greater than zero, some players may have difficulty because they're not accustomed to thinking in terms of coordinates. Further, a future patch may remove the debug screen (which displays coords) from the standard client. Anyway if you don't want players claiming underground, you can set this to something near sea level. Or, lower to prevent players from claiming diamond-laden areas.

`Claims.MinSize: 10`

The minimum size for sides of a claim. If you make this very small, griefers may run around creating very tiny claims all over the place just to annoy other players. And then you'll have to come clean it up. :) Note that administrative claims (`/adminclaims` mode) ignore this rule, so you can use that together with `/transferclaim` to create smaller claims on a claim-by-claim basis, as needed.

---
# Claim Security

`Claims.PreventTheft: true`

Set this to false if you want to allow players to steal from claimed containers (like chests and furnaces) and attack claimed animals.

`Claims.PreventButtonsSwitches: true`

Set this to false if you don't want players to use buttons and swtiches to limit access to their builds. Players can still limit access by simply using solid blocks rather than a door, so this won't guarantee all players can explore all of the world.

`Claims.LockAllDoors: false`

By default, only iron doors are lockable. This encourages players to "earn" their privacy by playing the game enough to gather iron ore, and then learning very basic redstone engineering. If you set this to true, then ALL doors (wooden doors, trap doors, fence gates) will require `/accesstrust` for a player to open, unless the builder has placed a touchplate in front of the door for visitors. Many of your players might not be aware of `/accesstrust`, which could lead to a lot of near-strangers getting `/trust`, which can open a lot of builds to grief.

`Claims.PreventNonPlayerCreatedPortals: false`

By default, any portal created by a player will be checked to ensure that player has access to the claim the remote portal will end up in. Setting this option to true will mean that any portal creation that cannot be attributed to a player will also be blocked. If this option is set to false, only player related portals can be checked and blocked for griefing behavior. 

---

# Restricting Where Claims May Be Created

Use the `claims.worlds` configuration variable to list which worlds players may create claims in. Options are `Survival`, `Creative`, and `Disabled`. Beware - if you set a world to `Disabled` which already includes some land claims, those land claims will stop protecting the blocks inside.

If you want to prevent players from making claims in a specific area without impacting their ability to build there, place an administrative claim and then use `/trust public` while standing inside it. Players can do anything they want there now except for claiming land, because the area is already claimed.

---

# Restricting Who Can Create

By default, all players may create claims with the shovel. To prevent a player from creating land claims with the shovel, take away the `griefprevention.createclaims permission`. This does NOT block new player claims. To disable those for everyone, set the `Claims.AutomaticNewPlayerClaimsRadius to -1`.

If you choose to effectively disable player claims, then you might also want to take away the `griefprevention.claims` permission from all players. This permission is granted to everyone by default, and is necessary for the claims-related slash commands. So by taking it away, you will clean up their `/help` experience.

---

# Expiring Inactive Claims

Claims build up over time. In the most extreme cases, this can eventually hurt the server's performance because there are so many claims to search through. To eliminate this potential issue for long-term successful servers, automatic chest-based land claims which have not been expanded will be automatically deleted when the owner has been inactive for a week (see `ChestClaimDays` config setting).

The `AllClaimDays` config setting is available to you in case you'd like to more aggressively expire land claims for inactive owners of larger land claims. I advise against turning this on, since it will leave awesome builds (which are a credit to your server!) open to grief. It will, however, massively reduce your claim count.

Claims in creative rules worlds (see config notes above on designating creative rules worlds) will be automatically restored to a natural state when expired. Claims in other worlds will not, since building requires more effort in survival mode, which makes any loss greater if the player does one day return to find his work vanished. You can change these settings in the config file.

It's been suggested that there should be a permission which may be given to players to exempt them from claim expiration, for example for when players go on vacation. It's an excellent idea, but Bukkit does not allow for checking an offline player's permissions. :( If this changes in the future, then I will add the requested permission node. In the meantime, you can use `/TransferClaim` without specifying who to transfer to. This will convert a land claim to an administrative claim, which will never be removed due to player inactivity. You can even `/trust <owner>` and `/permissiontrust <owner>` to ensure that when the player comes back online, he'll still have access to his land claim (except to change its dimensions).

---

# Catching Sneaky Griefers

Due to the rock-solid preventative measures built into this plugin, you'll find that even the most resourceful, creative, motivated griefers can do very, very little. However, right-clicking the occasional cobble swastika or dirt penis can be a minor annoyance, so you may be interested in actually catching and banning some griefers. Most griefers are 10 year olds with anger management issues, so they're obvious and easy to catch. Other more sophisticated griefers are clever 10 year olds trapped in 15 year old bodies, with anger management issues. These tools will assist you in catching the almost-clever.

Sometimes, griefers will place signs to communicate secretly or anonymously. For this reason, all sign placements are logged so that you may investigate any issues.

`SmartBan: true`

Many griefers have access to multiple accounts, so a /ban alone doesn't always help. Similarly, IP bans are easy to work around with a quick router reset (it doesn't help that Minecraft notifies players when their IP is specifically banned). When a player is banned, this smart ban option temporarily bans his IP address, so that any players who have NEVER been on your server before who try to log in with that same IP address in the next 24 hours will also be banned, and the ban message will not mention anything about his IP address. This is very effective at blocking a griefer with multiple accounts, and yet it's unlikely to ban another (innocent) player who happens to use the same computer to play on your server, or who coincidentally gets the IP address when it's reused by the griefer's ISP much later.

`AdminsGetWhispers: true` and `AdminsGetSignNotifications: true`

Some almost-clever griefers use whispers and signs to communicate secretly. Unless you disable these features, all whispers and sign placements will be shared with any online administrators (permission: `griefprevention.eavesdrop`). This can be useful for catching players who work together to grief or cheat. You'll also notice a configuration option to list more whisper commands which may be available on your server due to other plugins, like /r and /whisper. Note that anyone who has permission to eavesdrop will not be eavesdropped upon.
Limiting TNT and Monster Damage

`BlockSurfaceExplosions: true`

Set this to false if you like creeper craters and enormous TnT holes all over the surface of your map. When this feature is on, creepers and TnT only destroy blocks underground. Explosions can still kill players, so leaving this on doesn't make creepers safe to fight. :) This option does not retroactively clean up old craters.

`EndermenMoveBlocks: false`

Most players see Enderman vandalism as an annoyance. It's too expensive to always check for claims every time an enderman tries to move a block, so you have this configuration option. If you allow endermen to move blocks, they will be able to move them everywhere, even inside claims. Like creepers, the "vanilla" behavior for endermen has a detrimental effect on your landscape over time, speckling it with potholes.

`CreaturesTrampleCrops: false`

Players can never trample crops. This configuration option stops monsters and animals from trampling crops, which is important because resourceful griefers will "lead" monsters and animals to trample crops. If you allow animals to trample crops with this option, they can trample crops anywhere, even in claimed areas (it's too expensive to make this selective).

`RabbitsEatCrops: true`

This is debatably not "grief", since it's not controlled by players, but Vanilla rabbit behavior can be an annoyance to farmers. You may disable this option to prevent rabbits from eating crops.
Controlling Fire

`FireSpreads: false`

Set this to true if you want to allow fire to spread. Beware, griefers love to start forest fires. Setting this to true could slow your server down (producing server-side lag).

`FireDestroys: false`

Set this to true if you want to allow fire to destroy blocks. This is a TERRIBLE idea unless you have another plugin which stops this kind of destruction, like for example CreeperHeal. Even if you enable this, blocks inside claims will still be protected from fire, but your trees will be at the mercy of griefers.
Preventing Chat Trolling

---

# Auto-muting new players who say banned words

See File: BannedWords.txt

NEW players who spout severe profanity (meaning words which are never acceptable in any context, set by you in the BannedWords.txt file) are automatically muted and not informed about the mute. None of their messages will be received by other players unless an administrator reverses the mute with `/SoftMute`. This is designed to identify players who join a server only to start trouble in the chat using offensive language like racist or homophobic slurs.

For all players (even those who aren't new to your server), messages including banned words will never be sent in the general chat (private messages are not policed). The difference is that they aren't permanently muted like a new player would be, and get a warning message for the first infraction in each play session.

The banned words file does NOT support regular expressions, by design. It's not possible to cover all profanity (including workarounds like misspellings and added symbols/punctuation) even with regular expressions, and allowing regular expressions would also create a problem for me, where everyone wants help developing regular expressions (see this post). Finally, many words are acceptable in certain contexts, and because this feature mutes the entire message (without notification) instead of only censoring the banned word, a lot of chat confusion would result if the banned word list were expanded to include conditionally appropriate terms. This might lead you to suggest that only the banned word be censored, but that would actually make the system LESS effective, because when a mean-spirited player can see whether he's censored or not, he can then easily experiment with workarounds to find one that works (and he will, regular expressions or not).

If you don't believe me and still hold onto hope that one can effectively fight offensive human language with code, there are many plugins available which try very hard to do just that. :) Try shopping around.

You can effectively disable this feature by just leaving the banned words file blank (deleting it will reset it - so just empty the list).

---

# Preventing Tree Grief

`LimitSkyTrees: true`

Prevents trees from being planted in the wilderness when they're in shallow dirt (for example a thin platform in the sky). Griefers like to do this because they get a lot of blocks in the sky by placing only a few. Non-griefing players can get around this by making a thicker platform, claiming the area, or planting in grass instead of dirt.

---

# Preventing Player Traps

Griefers can dig a hole and claim it to create a quick and effective trap for other players to get stuck in. When a player complains about being trapped or stuck in chat, he will be educated about the `/trapped` command, which can save him.

Unfortunately, nothing can be done to completely prevent lethal traps, like lava traps. The presence of the claim to make a trap difficult to disarm (by other players) will also make it easy for you to determine who created the trap and take appropriate action. :)

---

# Creative Claims Mode

`Claims.CreativeRulesWorlds` is the list of worlds where players additionally follow creative-mode rules. In these worlds, players can only build in areas they've claimed, and they're limited in how many entities (monsters, animals, etc) they can spawn in their claims. Also TNT doesn't explode terrain, and any unclaimed blocks will be automatically restored (`/restorenature`). There are more rules than these, but those are the most important and most noticeable. See below for more.

## How is creative GP different from survival GP? The following additional rules apply:

* Players can't build in the wilderness. They must claim land first, and build there. When they try to build in the wilderness, they will get an error message which includes a link to a short creative-mode-specific demo video. Because players have unlimited blocks and the ability to fly, any griefer would be able to make a huge mess very quickly without this rule in place.
* When blocks are unclaimed, they are reverted back to a natural state (the build disappears).
* Because a griefer might want to make a temporarily claim just to build something awful and then unclaim it, any unclaimed blocks will be automatically cleaned-up. Players get a warning about this when they unclaim blocks, and have a couple of minutes to undo their changes in response.
* Empty minecarts which are in motion will be automatically removed. This prevents griefers from building huge tracks with lots of carts just to drag server performance. Note that a rollercoaster is fine - the minecart just has to stop at the end and wait for a player to start it again.
* There's a limit to the total number of entities (animals, NPCs, minecarts) in a claim, which grows based on the size of the claim. This prevents entity spam.
* It's not hard to get an entity you create IN your claim OUT of your claim. To prevent griefers from working around the above rule, any minecarts not on tracks, empty boats, and animals/NPCs in the wilderness will be automatically removed. Griefers may think they're succeeding for a short while, but in reality, all their work will disappear after they've gone. Note players can still enjoy boating - but if they leave empty boats lying about, those will be automatically removed.
* The only way to spawn an animal/monster/NPC is to use a spawner egg or construct a golem.
* It's not possible to toss items on the ground. When blocks are destroyed, they don't drop items.
* TNT doesn't destroy blocks.

If you'd like to lock down a creative world such that players build in plots you specify, then you can disable claims as described above, and use `/transferclaim` with `/adminclaims` to create claims for players in exactly the locations you want them.

---

# Anti-Spam Configuration

`Spam.Enabled: true`

Whether or not to monitor for spam. Disable this if you have another anti-spam plugin, or if you're feeling reckless. Players with `griefprevention.spam` permission can spam all they like.

`Spam.LoginCooldownSeconds: 60`

How long a player must wait before logging in (after the last login). This prevents login/logout spam, a favorite of griefers with hacked clients. Players with permission `griefprevention.spam` bypass the cooldown.

`Spam.ChatSlashCommands: /local, /tell, /me, /global`

This is the list of chat commands (they send messages to multiple recipients), which should be monitored for spam. List any slash commands which generate chat messages (think especially about any other plugins you have installed which allow players to send chat messages).  Players who suffer from administrative `/softmute` can't use these commands at all, because it's not possible to simply reduce the audience for the message.

`Spam.WhisperSlashCommands`:

This is a list of commands which send private messages to individual players. These are the commands which would be eavesdropped-upon by administrators when eavesdropping is enabled, and are also monitored for spam. Players who suffer from administrative `/softmute` can only use these commands when the first parameter names a player who is also soft-muted.

`Spam.BanOffenders: true`

Whether or not spammers will be automatically banned. If banning is disabled, the player will just be kicked (so he can log right back in). That should help get his attention. :) There's no option neither kick nor ban (just mute the single message) because hacked clients can send spam at such a rate that even when muted, processing all the incoming messages can cause server-wide lag.

`Spam.BanMessage: "Banned for spam."`

Message to display to a spammer who's been automatically banned. Consider additions like "Appeal on our forums" or "Appeal to yo mama".

`Spam.AllowedIPAddresses`

A list of IP addresses which you allow players to send via chat. Normally, all IP addresses are muted to prevent server advertisement spam. You may want to add the IP addresses of other Minecraft servers you run, or your Ventrilo/Teamspeak/Mumble server, for example.

---

# PvP Configuration

`PvP.PunishLogout: true`

Griefers often use x-ray cheats to get lots of diamond gear, then start PvPing. To avoid losing their gear, if they think they might lose a fight, they disconnect and come back later. This option will kill any player who tries to log out during PvP combat, allowing the other player to collect his drops. A player is considered "in combat" for 15 seconds after the last time he gave or received PvP damage.

`PvP.ProtectFreshSpawns: true`

Set this to false to disable the automatic no-PvP status for new players and fresh respawns. The immunity lasts at least 10 seconds, during which they can't pick up items (so they can't abuse the invincibility to collect loot and run away), then disappears when they pick up an item the initial 10 second period. This effectively stops spawn camping in all cases, not only when everyone shares a designated no-pvp respawn area.

If you'd like to disable this in specific worlds, use your permissions plugin to grant players in those worlds `griefprevention.nopvpimmunity`. This will effectively disable the anti-spawn-camp feature in those worlds.

`PvP.AllowCombatItemDrop: false`

Turn this on if you want players to be able to toss items on the ground during combat. Beware, some "clever" players will use this to hide some of their valuables before they die, to keep them from their killer.

`PvP.CombatTimeoutSeconds: 15`

The number of seconds after the last PvP damage, during which a player is still considered "in combat". This prevents him from logging out without penalty, dropping items, accessing containers, etc.

---

# Economy Integration

If you have the Vault plugin installed AND a Vault-compatible economy plugin installed (see the Vault page for a list), then you may allow players to buy and/or sell claim blocks using server currency by setting the buy and sell values in the config file `GriefPrevention.Economy.ClaimBlocksPurchaseCost`. By default, all players will be able to buy and sell - if you'd like to restrict that to only some players, then take away the `griefprevention.buysellclaimb­locks` permission from any players or player groups who should not be allowed to buy and sell claim allowance.

If your economy integration doesn't seem to be working after initial setup, check your boot logs for hints about the problem.

---

# Non-Standard World Support

Bukkit doesn't always tell plugins the right value for sea level, so if your world has non-standard sea level, you should specify your actual sea level in the config file (`SeaLevelOverride`). For worlds where sea level is at a 'normal' place, leave the setting at -1 and GriefPrevention will just ask Bukkit. GP uses this setting to decide, for example, whether or not a creeper can destroy a block and how deeply `/RestoreNature` should reach.

---

# Piston Movement

Configuration option `GriefPrevention.PistonMovement`
  * `EVERYWHERE`: Pistons can be used everywhere. All blocks moved are checked to ensure that they do not enter into a claim that is not owned by the owner of the piston's claim.
  * `EVERYWHERE_SIMPLE`: Pistons can be used everywhere. Instead of checking every block moved, the zone surrounding all moved blocks is checked. As long as no part of the zone overlaps a claim with a different owner, pistons are allowed to move freely. This means that certain non-threatening movements will be blocked, but it handles more complex structures much faster.
Example of a valid but blocked piston:
![image](https://user-images.githubusercontent.com/1353270/89216742-f4fa2180-d598-11ea-9640-ac29c02f9ecf.png)
  * `CLAIMS_ONLY` (default): Pistons may only be used inside claims. If blocks outside of the claim that the piston is in are affected (even if the owner is the same!) the piston movement is blocked. This is the only mode that completely prevents pushing blocks out of claims.
  * `IGNORED`: Pistons are not checked. Griefers can use flying machines to destroy or disrupt your builds.

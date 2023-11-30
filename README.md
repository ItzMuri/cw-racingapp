# CW rework of [QB-Racing](https://github.com/ItsANoBrainer/qb-racing)

This is a rework of the superb free resource [QB-Racing](https://github.com/ItsANoBrainer/qb-racing) by ItsANoBrainer.


**Some of the added features:**
- Integration with [cw-performance](https://github.com/Coffeelot/cw-performance) to create class based racing
- Advanced leaderboard for each track and class showing everyones best times
- By-class leaderboard
- Replacement of tire-piles lamps
- Increased size of checkpoints
- Not as harsh checkpoint-pass detection compared to qb-racing
- Remove race tracks you have created
- See your position in the race
- Updated HUD
- Accurate time (old one would vary depending on computer performance) **NOW IN MS!**
- Ability to reset/run the SQL scripts from in game
- Phasing/Ghosting of racers
- Ability to lock tracks down to people by citizen ID
- Support for Renewed Crypto
- Participation payouts
- Post race leaderboard
- Custom UI
- Track curation

**Original features by ItsANoBrainer:**
- Standalone racing script not requiring qb-phone to utilize
- Items to immerse your racing scene with Racer Names
- Config options to adjust item permissions to your liking
- Config options to adjust different options
- Locale Support
- Create Custom Races Tracks

> As of update posted on 1st July -23, racer names are unique. The max limit is by default 3 but can be set individually. If you want to remove names from DB without openign it up, an admin can use `/remracename <racerName>`

> As of update posted on 26th August -23 we will no longer support qb-menu usage. 


# Developed by Coffeelot and Wuggie
[More scripts by us](https://github.com/stars/Coffeelot/lists/cw-scripts)  👈

**Support, updates and script previews**:

[![Join The discord!](https://cdn.discordapp.com/attachments/977876510620909579/1013102122985857064/discordJoin.png)](https://discord.gg/FJY4mtjaKr )

**All our scripts are and will remain free**. If you want to support what we do, you can buy us a coffee here:

[![Buy Us a Coffee](https://www.buymeacoffee.com/assets/img/guidelines/download-assets-sm-2.svg)](https://www.buymeacoffee.com/cwscriptbois )

# Racing App

Options:
 - Join a race
 - View race records
 - Setup a new race
 - Create a new race track
 - Modify old tracks
 - List your own tracks
 - Manage racer users (for master and god rank users)

### GPS settings
At the bottom left corner there's a cog wheel. Clicking this brings up the options menu (more stuff to come). But here you can toggle using the GPS route and the style of it.

### Track Curation
Our idea with this feature is to allow admins to flag a track as "DONE". The track can no longer be edited. Additional features of curated tracks might be only allowing participation money to be paid out on those tracks, for example.

Currently you can only curate/uncurate a track via admin command: `/racingappcurated "<race-id>" true/false` **QUOTATION MARKS AROUND RACE ID IS IMPORTANT**

### Track Creation
The key to this script working is making GOOD tracks. If you're trying to do 200 checkpoint style races with checkpoints randomly thrown around the map, this is not the script for you. There is a max checkpoint variable in the config that will warn users when they reached the level. Some PCs might struggle with different lower/higher amounts tho, so keep that in mind.

- Avoid placing checkpoints on/under/near bridges/overpasses. 
- GTA GPS can't handle opposite-directions on roads: Place checkpoints on the correct side of the road
- Intersections can be tricky for the GPS. We advice to not put checkpoints in the middle of them, but before or after, in the correct lane.
- Alleys can cause issues. Use with caution.
- The script spawns 2 entities + 1 emitter for EVERY checkpoint. If you have 100 checkpoints that might just crash peoples games. 

### Track Sharing
You can grab the checkpoints from either My Tracks tab in game, by using the copy button or directly from the database entry and then pasting to something like https://pastebin.com/
There's an import function (if enabled in config) in the Create Track tab to import via paste.

Hop into the [CW Discord](https://discord.gg/FJY4mtjaKr) and share some tracks in the racingapp-tracks channel! 

### Automated Races
The script offers automated races. You can set these up in the config (`Config.AutomatedRaces`, `Config.AutomatedOptions`). If any of these are commented out/removed the automation will not start.

The Automation will, at random, try to grab one of the tracks from the `Config.AutomatedRaces` table at the interval of what you set in `Config.AutomatedOptions.timeBetweenRaces`, by default this is 20 minutes. The races start after 5 minutes of popping up.

### User Management
The script offers user management now. We've moved away from the basic/master fob and instead users are saved in the database.
To swap your user, open the racingapp and press the cog-icon to open the settings.
To create users you can either buy a user account from a trader/laptop (if this is enabled in the config) or have someone create one for you.

The tiers are racer < creator < master < god and are defined as follows:
```lua
    racer = { 
        join = true, -- join races
        records = true, -- see records
        setup = true, -- setup races
        create = false, -- create races
        control = false, -- control users
        controlAll = false, -- control all users
    }
    ...
```

*join* means you can join races\
*records* means you can access records\
*setup* means you can set up races\
*create* means you can create tracks\
*control* means you can manage users you create\
*controllAll* allows you to control all users, and also permanently delete users

Basically, any racer name/user created by another player will be tied to them. So if person X buys an account from player Y, player Y can also revoke player Xs account via the in game menus, as long as player Y has a user with the *control* authorization.

# Preview 📽
### Note: Before new UI was added

[![YOUTUBE VIDEO](http://img.youtube.com/vi/APtMydz4gF8/0.jpg)](https://youtu.be/APtMydz4gF8)

Update to track editor:
### Note: Before new UI was added

[![YOUTUBE VIDEO](http://img.youtube.com/vi/N_HI0jAsgbg/0.jpg)](https://youtu.be/N_HI0jAsgbg)

### UI Update:

[![YOUTUBE VIDEO](http://img.youtube.com/vi/j0KKvy-2VWc/0.jpg)](https://youtu.be/j0KKvy-2VWc)

### User Management Update:

[![YOUTUBE VIDEO](http://img.youtube.com/vi/YzJjRs2rv2s/0.jpg)](https://youtu.be/YzJjRs2rv2s)
# Setup
You only need either this resource and [cw-performance](https://github.com/Coffeelot/cw-performance).

1. Update or insert the database tables. These are found in the `racing.sql` file
2. Adjust values in the `config.lua` file to your liking
3. Add the items to your `qb-core/shared/items.lua`
```lua
['racing_gps'] = {['name'] = 'racing_gps', ['label'] = 'Racing GPS', ['weight'] = 500, ['type'] = 'item', ['image'] = 'racing_gps.png', ['unique'] = true, ['useable'] = true, ['shouldClose'] = true, ['description'] = 'Wroom wroom.'},
```
4. Add the item images to your inventory image folder

# Updating?
If you're updating from a previous version these might be for you

### New User Management - 30th November 2023
You need to update one of your database tables. Run this:
```sql
ALTER TABLE racer_names
ADD COLUMN auth TEXT DEFAULT 'racer',
ADD COLUMN createdby TEXT,
ADD COLUMN revoked TINYINT DEFAULT 0;
```
You also need to change out the old GPS/fob items to the new one, see setup section. 
You might also want to read up on the new system, see Racing App section.

# Dependencies
* [qb-menu](https://github.com/qbcore-framework/qb-menu)
* [qb-input](https://github.com/qbcore-framework/qb-input)
* [cw-performance](https://github.com/Coffeelot/cw-performance)



## Example Usage
### Interface Images *(Using our custom skin on QB-Menu and QB-Input)*

**Main Menu**

![Interface](https://media.discordapp.net/attachments/977876510620909579/1144989065402405005/image.png?width=781&height=522)
![Interface](https://media.discordapp.net/attachments/977876510620909579/1144989080665473084/image.png?width=781&height=506)

**Leaderboards**
![Interface](https://media.discordapp.net/attachments/977876510620909579/1144989096062754876/image.png?width=781&height=510)

![Interface](https://media.discordapp.net/attachments/977876510620909579/1144989109425811517/image.png?width=781&height=525)

**Setting up a Race**
![Interface](https://media.discordapp.net/attachments/977876510620909579/1144989123430584411/image.png?width=781&height=521)

# Uninstalling or full reset
## /removeracetracks
Drops the `race_tracks` table. Use this if you're uninstalling (warning: all tracks and records will be gone)
## Developed by Coffeelot#1586, Wuggie#1683

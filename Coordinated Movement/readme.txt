So you decided to grab my coordinate based movement system, have you? Good choice, who likes the room system anyway! Not me, that's for damned sure!

So, here's what this library can do for you:

> Simulate several rooms within a single object
> Make large-scale locations possible without flooding your editor with a ton of sub-rooms
> Generate object descriptions based on what's in the same location as people

Conversely, this stuff won't take care of:

> Filling every room with interesting content
> Writing the entire description
> The z axis - Sorry, maybe eventually, but this makes the workload for this project spiral exponentially... but hey, you still have 2 axis.
> Moving objects/npcs around - Either do that yourself or wait and hope that someone (likely me) will make an addon for that.

------------------------------------------------------

But fine, let's look at what you have to do to make this work. And good news, most of what can be automated, is. For the first time setup all you have to do is:

> Load the library into your game
> Under 	game -> Room Description 	turn off auto-descriptions

------------------------------------------------------

And that's it! Sadly the per-room setup is a lot more since, well, I can't exactly do the creative work for you. As such, to create a map you need to (And I recommend you do it in this order, though that's not necessary):

	Room:

> Create the room

> Set the maxx and maxy attributes to the respective maximums of the "box" you want your place to work in

> Set a description for every location in your room by adding the coordinates (x; y) along with the script you want to play out for that location.

> If you've selected a room/object combination, you HAVE to inherit the "TG_ObjectRoom" attribute, or manually create a "isroom" attribute and set it to true.

	Exits:

> Create an Exit for every direction your player should be able to go to (north, west, etc). They don't have to be connected to a room, just have a type. Note that Up, Down, In and Out won't change coordinates based on that whole z axis thing. You can still use them as map exits, though.

> While they don't actually need to have a name (Quest technically calls them exit1, exit2 etc. which the script will happily handle) I do recommend you name them for your sanity

> If you want an exit to be used to actually leave the room, you can add the coordinates where it should happen along with the destination to the exitRoomDestination attribute. This can be accompanied by a script via the exitRoomDesc attribute.

> If you only want your exit to appear in a few specific places (Best used with in, out, up and down), set static to True. This will reverse the blocked attribute so that only coordinates entered there will be where your exit appears.

> If you want to build more than a grid, you'll want to liberally use the blocked attribute to tell the game where the location should not be available at. For example, if North is blocked at 1; 2 it will be hidden if the player enters 1; 2. Remember to then also block South at 1; 3! Also keep in mind that the map edge is blocked off automatically. Excuse this mess, this was by far the simplest way I could think off.

	Objects:

> Set the x / y attributes to where you want your object to be at.

> Use the In-Room Description to set what should be displayed, if the object is visible. Leaving it empty will skip the object for descriptions.

> If you don't want the automatic script to mess with your object, set protected to "true". This will completely skip it over, useful for things that should be seen from everywhere within the location or things you need to handle yourself.

------------------------------------------------------

And that's your setup! Congrats, everything should work fine now. From here on out, it's dry explaining of the attributes and functions. So, only go ahead if you need it!

	Functions:

SetStage([True/False]) - Runs through every object and exit in the room and checks, if they should be visible to the player before calling the description, if the parameter is set True. If you don't want to generate a description, set it to false.
AddExit([Room Name], [Exit Name]) - If you want to completely create an exit mid-game, please run this function afterwards. Don't ask, quest is just terrible.
RemoveExit([Room Name], [Exit Name]) - Same as above, if you want to fully delete an exit mid-game, run this function afterwards.

	Attributes:

Standard:

x - Int. The x coordinate of an object.
y - Int. The y coordinate of an object.
protected - Bool. Makes most scripts completely ignore the object / exit.

Rooms:

maxx - Int. The maximum x coordinate of a room. Used to hide exits and prevent players from moving out of bounds.
maxy - Int. The maximum y coordinate of a room. Used to hide exits and prevent players from moving out of bounds.
exitMessage - String. Controls what is said before all possible exits are displayed.

Exits:

static - Bool. If set to True, the exit will only appear in locations defined by the blocked attribute.
exitRoomDestinations - String Dictionary. Used to determine where an exit should exit the current room instead of moving, to which room the player is moved and what coordinates the player will be moved to. (x; y -> RoomName; x; y)
exitRoomDesc - Script Dictionary. Used to run a script when moving to a new location. (x; y -> Script)
blocked - String List. Used to determine specific locations, where the exit should not appear / exclusively appear if static is set to True. (x; y)

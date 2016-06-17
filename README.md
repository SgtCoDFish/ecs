# Entity Component System Frameworks - Notes and Research
"Entity Component System" (ECS) frameworks are a data-driven approach to managing and processing objects in a game world. Rather than using a rigid, OOP-style class structure with inheritance to represent objects, we say that each object is an "entity" - nothing more than an ID number and a bag of "components" which contain data about the object. We then define "systems" which act on entities with a matching set of components.

## Example

The ubiquitous example of ECS would be implementing a "MovementSystem" which handles movement for game objects. In pseudocode we might say:

```
System movementSystem = new System();
movementSystem.match(PositionComponent, VelocityComponent);
movementSystem.onTick(function(Entity e) {
	e.getComponent(PositionComponent.position).add(e.getComponent(VelocityComponent.velocity));
});

Entity player = new Entity();
player.attachComponent(new PositionComponent(4, 6));
player.attachComponent(new VelocityComponent(1, 1));

Entity wall = new Entity();
wall.attachComponent(new PositionComponent(10, 10));

world.addEntity(player);
world.addEntity(wall);
world.addSystem(movementSystem);

world.tick();
// now player has position (5, 7), wall has not moved
```

We define a movement system which matches all entities which have both a PositionComponent and a VelocityComponent. We also define a player entity and a wall entity; the player has both components and so is matched by the movement system while the wall lacks a velocity (as you might expect!) and so does not match.

We have some over-arching "world" which handles the internal mechanics of the framework, and when we call "tick" each system is run in turn. We see that the player's position is increase by its velocity and the wall's position is unchanged as expected.

# Other Documents
## "Game Engine Architecure", Jason Gregory
Full citation: Jason Gregory, "Game Engine Architecure", Natick, MA. A K Peters, 2009
Pages 728 - 733

- Rob Fermier, ["Creating a Data Driven Engine"](), Game Developer's Conference, 2002.   
Original link to slides from book [at gamasutra.com](http://www.gamasutra.com/features/gdarchive/2002/rob_fermier.ppt) does not give expected result.

- Scott Bilas, ["A Data-Driven Game Object System"](http://www.gdcvault.com/play/1022543/A-Data-Driven-Object), Game Developer's Conference, 2002.   
Original link to slides from book [at drizzle.com](http://drizzle.com/~scottb/gdc/game-objects.ppt) is down.

- Alex Duran, ["Building Object Systems: Features, Tradeoffs and Pitfalls"](http://www.gdcvault.com/play/1022628/Building-An-Object-System-Features), Game Developer's Conference, 2003.   
Original link to slides from book [at gamasutra.com](http://www.gamasutra.com/features/gdcarchive/2003/Duran_Alex.ppt) does not give expected result.

- Jeremy Chatelaine, ["Enabling Data Driven Tuning via Existing Tools"](http://www.gdcvault.com/play/1022653/Enabling-Data-Driven-Design-Tuning), Game Developer's Conference, 2003   
Original link to slides from book [at gamasutra.com](http://www.gamasutra.com/features/gdcarchive/2003/Chatelaine_Jeremy.ppt) does not give expected result.

- Doug Church, ["Object Systems"](http://chrishecker.com/images/6/6f/ObjSys.ppt), from a conference in Seoul, South Korea organised by Chris Hecker, Casey Muratori and Doug Church.
<p align="center"> <img src="https://www.codecollision.dev/git-head.png" alt="code / collision" /> </p>

People enter the coding world in a differently than when I was growing up. The internet increased our reach and many first-steps are in building business, productivity, & lifestyle applications.

I grew up coding games. My peer group was made up of many who built "casual games" with only a small handful building applications. Today's new class of coders has that inverted. 

Building games taught me a lot. There were the same basics you need in a business app - front end and back end, work.  But you also got to do lots of **other** stuff: *Game mechanics, game physics (movement, acceleration, friction, gravity), collision detection*

The best part was building the in-game AI. That's where magic happens - and not just magic. **So much learning.** Translating a game strategy into code ***hard***. And ultimately, it makes you a stronger coder. 

**code / collision is an attempt to expose application developers to the world of game development, while lowering the bar so you can focus on the interesting part.**

The game dynamics are handled. Object collision is handled. **You build the strategy.**

# How does it work?
code / collision is an ever-expand library of games that work on the same set of principles:
- 2 teams
- Can be simultaneous or turn-based
- The game mechanics are handled
- You determine what your team's strategy is for the desired game
- You write the code for that strategy:
 - You are given the game-state in the parameters
 - You return 2 things: Angle you want to move, and overall Power.
- Your code is called periodically, **once per player on your team**
<p align="center"> <img src="https://www.codecollision.dev/git-game.png" alt="code / collision" /> </p>

# How do I code my strategy?
code / collision was built in vanilla JS. As long as you know some basic JavasScript, you can write a strategy.

Strategies look like this:

```javascript
class mySoccerStrategy extends SoccerStrategy
{
	static strategy = CodeCollision.Register(this); //REQUIRED
	
	execute //Return Power (0-100), and Angle (0 is forward, 90 is up, -90 is down, 180 is backwards)
	({
		id, //Represents which player this strategy is for  (Values: -1, 0, 1)
		position, // { x, y }
		field, // { width, height }
		teamMates, // [ {angle, distance, x, y} ]
		otherTeam, // [ {angle, distance, x, y} ]
		ball, // {angle, distance, x, y}
		ownGoal, //{ topPost{angle, distance, x, y},  bottomPost{angle, distance, x, y} }
		otherGoal //{ topPost{angle, distance, x, y},  bottomPost{angle, distance, x, y} }
	})
	{
		if (id==0) { //this player will always go at the ball, with a random power-level
			return { angle: ball.angle, power:Math.random()*100 };
		}

		//this player will go for the ball if the ball is infront of the player,
		//otherwise they'll move straight back
		return { angle: Math.abs(ball.angle<90)? ball.angle : 180, power:Math.random()*100 };
	};
}
```

# How do I compete?
Right now, the idea is anyone to host their own "events" - get a bunch of coders together, pick one of the game types, give yourselves an agreed-upon coding time: 1 hour, 1 day, 1 week. Then host a competition where everyone's code is pitted against each other's!

# How do I get started?
1.  Grab the code / collision repo.
2. Launch codecollision.html in the top level directory.
3. Select one of the games from the drop-down list.
4. Hit **Edit** to use the built-in  [Ace Editor ](https://ace.c9.io/ "Ace Editor ") to build your strategy.
5. You can test your strategy in real-time by hitting **Run**.
6. When you are happy with your strategy hit **Export** to save your strategy as a .JS file.
7. You can then load your strategy and others on the game screen by clicking **Load**.
8. Select which strategies you want to have compete and hit **Start**.

# Check out a demo
[![code / collision demo](https://img.youtube.com/vi/jvfGyRmCilg/0.jpg)](https://www.youtube.com/watch?v=jvfGyRmCilg)

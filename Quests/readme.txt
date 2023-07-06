A new Questing system.

Featuring Quests, SubQuests and SubSubQuests, this library has everything you need to create, manage and display them.


Creating a Quest goes as follows:

Quest add 	("ExampleName", "This is the description of this Quest.")
Goal add 	("ExampleName, "Create a Quest")
SubGoal add	("ExampleName, "Create a Quest", "Finish reading this tutorial")

This Quest can then be seen by the player by typing in "Quests", "Questlog", or "Show Quests". Maybe tell them that, yeah?


Now, let's say you finished reading this tutorial and thus completed the quest.

Well, you would use:

SubGoal finish 	("ExampleName, "Create a Quest", "Finish reading this tutorial")
Goal finish 	("ExampleName, "Create a Quest")
Quest finish 	("ExampleName", false)

Note that that false in Quest finish tells QuestLib that the Quest has been completed succesfully. Setting it to true will count the quest as failed and will show up in a seperate list.

Except you don't need to because just finishing the Quest is enough. It will automatically finish all the Goals and SubGoals for you! This also goes for Goal finish.



Finally, to check if the player even has a Quest/Goal/Subgoal, you can use:

HasQuest 	("ExampleName")
HasGoal 	("ExampleName", "Create a Quest")
HasSubGoal	("ExampleName", "Create a Quest", "Finish reading this tutorial")

Which will return a bool. They'll also upcast, so HasSubGoal will check if HasGoal ist true, which will in turn check if HasQuest is true. 

HasQuest also has three variations to check its current state. These are:

QuestActive 	("ExampleName")		-	Checks if the Quest is both present and not completed yet
QuestFinished	("ExampleName")		-	Checks if the Quest has been completed successfully
QuestFailed		("ExampleName")		-	Checks if the Quest has been failed


And that's all, really! Thank you for using this library, feel free to write me if you think of a feature you'd like to see and go check out my Coordinate Based Movement System!



Documentation:

Commands:

Quests; Questlog; Show Quests;		-	Displays the player's current and finished Quests.


Functions:

	Quest Control:

	Quest add ("QuestName", "QuestDesc")					- 	Adds a Quest and gives it a short description. Will Log and continue if the quest already exists.
	Goal add ("QuestName", "GoalName")						-	Adds a Goal to the specified Quest. If the Quest doesn't exist, it will Log and silently fail.
	SubGaol add ("QuestName", "GoalName", "SubGoalName")	-	Adds a SubGoal to the specified Goal. Will Log and silently fail if Goal does not exist.

	Quest finish ("QuestName", Failed)						-	Finishes the specified Quest. If Failed is set to true, the Quest will count as failed. Will also finish goals and subgoals.
	Goal finish ("QuestName", "GoalName")					-	Finishes the specified Goal. Will also finish subgoals.
	Subgoal finish ("QuestName", "GoalName", "SubGoalName")	-	Finishes the specified SubGoal.


	Query:

	HasQuest ("QuestName")									-	Checks if a Quest exists. Returns a Bool.
	HasGoal ("QuestName", "GoalName")						-	Checks if a Goal exists. Will also check if the Quest exists. Returns a Bool.
	HasSubGoal ("QuestName", "GoalName", "SubGoalName")		-	Checks if a SubGoal exists. Will also check for Quest and Goal. Returns a Bool.

	QuestActive 	("QuestName")							-	Checks if the Quest is both present and not completed yet
	QuestFinished	("QuestName")							-	Checks if the Quest has been completed successfully
	QuestFailed		("QuestName")							-	Checks if the Quest has been failed

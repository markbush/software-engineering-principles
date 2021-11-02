Source Code Repositories
========================

The key reasons for using source code repositories are:

* protection from accidental loss;
* easily sharing the latest versions of code;
* tracking changes (including *why* things changed);
* being able to refer back to earlier versions of code.

The first of these covers the situations where you might lose a laptop or your computer might become damaged somehow (even if that is just a disk drive corruption).  It also covers the situation where you inadvertently delete files you didn't mean to.  For this to be meaningful, the repository should be on a different computer system and it should be secure and backed up.

If you are working with a team, then the repository will need to be available on some sort of central system that is readily accessible to everyone.  If everyone works for the same company, then this can easily be an on-site server.  Otherwise, it may need to be "in the cloud" for maximum availability.

I have seen many applications where almost the entire project has been completed and then added to a repository in one go with the log message "initial commit".  This doesn't help anyone to understand the parts of the system and means that everything was at risk of loss while it was being developed.  Similarly, if code is only ever updated in the repository when there are significant changes (for example, the implementation of an entire feature), then log messages will not really say anything about when actual code changes have occurred.

In general, it is best to be committing code often and regularly to a repository.  When you write a test, commit it.  When you write a function, commit it (even if the test is still not working).  If you feel that you no longer need a piece of code, ensure there is a commit of the existing code, then delete the lines and immediately commit.  At least then you can easily track the change down and recover just the deleted lines if you realise you did need them.

The result of all these little commits will be a log of changes that are actually meaningful.  You will easily be able to refer back to any change and understand exactly what is was and why it happened.

There are (at least) three good reasons for wanting to refer back to previous code.  Firstly, to remind yourself how you implemented something that you may want to repeat; secondly to make use of old code that you thought was not going to be needed; and thirdly, to remind yourself of something you tried that didn't work.  This last reason should not be overlooked.  It is not uncommon to forget a "mistake".  Indeed, those new to a codebase will not know about things that went wrong in the past.  Having a recorded history of things that have been tried (with comments about why they were removed) will help avoid trying the same things again.

There is a distinction between committing and pushing code. When you commit, you give a log message about what has changed and save that change locally on your own machine.  When you push, you copy any local changes to the central repository so that they are secure and everyone else has visibility.  Committing often gives you the granularity of meaningful log messages and recovery points and pushing regularly gives you the security of protection against problems.

I would recommend pushing code to the central repository at least once a day at the end of the day.  Common times for problems to occur to a laptop are during journeys to and from your workplace.  Having your latest code secure in the repository every day also ensures that everyone else has access to the latest code if something happens to you, such as an illness.

It is easy to forget to push your changes if you are distracted by meetings and lunch breaks, so I would also recommend getting into the habit of pushing before lunch.  In fact, the end of any coding session would be a good time to push so that you don't forget.

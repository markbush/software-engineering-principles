:index:`Lazy Programming`
=========================

I have already suggested that *lazy programming* is the same as top-down development, however it is so much more.  Most of us have a certain understanding of what top-down development means, but the name doesn't really help us understand exactly how to go about it.  Or, rather, how to do it well.

The name "lazy programming" embodies a mindset.  It represents a cultural shift in how you approach the whole concept of software engineering.  It also has implications beyond mere "coding".

In one sense, being lazy is about doing the least possible work.  However, it is also about efficiency.  That is, using the least effort to achieve the required results.  This is not just about short term goals.  This is also about efficiency in the long term.  Whenever you are working, there are always at least two participants.  There is you, right there, performing the task.  But there is also your future self looking back over your shoulder.  There is no point doing something quick now if it results in them looking back at you in dismay.

To embrace laziness, you need to balance simplicity now without creating more work for yourself later.  There are a number of ways in which you can do this.  The most important of which is not to overthink what you are doing.  Each function or method you write should contain the least amount of code necessary to convey the *intent*.  It should read like a tiny story.  Good choices of variable and function names will achieve this goal.

I have often been in the situation of having someone show me some code and immediately feel the need to explain it.  This always suggests that the code is more complex than it needs to be.  The same follows for code that someone has felt the need to comment significantly.  If the code was more descriptive in terms of *what* it is supposed to be achieving rather than coding *how* it will produce the results, that both of these situations can be avoided for all but the lowest levels of the code.  In fact, the remaining code in those lowest levels will then be small enough that extra comments or explanations will still not be necessary.

Code Performance
----------------

One argument that often crops up for writing complex code with larger functions is the need for performance.  I think there are always three questions that must be asked by anyone taking this approach:

1. Is the code being written guaranteed to still be a part of the final version of the application?
2. Is the complex code guaranteed to perform better than more structured code?
3. Are there specific performance requirements for the piece of code that can only be met by manually optimising it?

The first question is important because the content of an application changes over time.  You can't be certain of exactly what will be needed until the application develops and the intended users give feedback.  It is not uncommon for ideas about what is needed or how that will be implemented to change and for some code to be thrown away.  What a waste if you have spent weeks trying to get that code to run as fast as possible!

The second is more subtle.  It is not always clear how a pice of code will run and simple tests often don't take into account the actual environment in which the application will run.  For example, if a piece of code will run many times, the JVM can update on the fly by inlining suitable code which will increase performance over time without needing to restructure the code.  This process that the JVM goes through as it gathers runtime statistics to be used for restructuring is called "warming up."  There is no point manually inlining code that the runtime would inline for you automatically.  If the code will not run much during production, then it is less likely that manual optimisation will make much difference to execution time.  Other languages also have similar functionality where code can be automatically inlines either at run time or compile time.

It is very rare with modern compilers that humans can do a better job at increasing performance by tweaking the code.  In practice, such improvements are more likely seen through better choices of data structures than actual code.  The more code that is produced which is purely functional (that is, where the result only depends on the function arguments), the easier it will be for the compiler or runtime to inline code and increase performance automatically for you.

In general, the best approach here is to write code for humans as a priority.  People (often including yourself) are going to be returning to the code in the future in order to fix bugs or extend the functionality and their task will be easier if the existing code is well structured and obvious in its purpose.

Once an application has been developed and is working correctly, then analysis tools can be brought to bear on it in order to highlight any areas of concern.  Manual optimisation efforts can then be focused on just those areas where the analysis has shown that automatic processes cannot meet the required performance requirements.

Getting "In the Zone"
---------------------

It's very common to hear people talk about being "in the zone" while working on some code.  This is often accompanied by stories of ending up working through lunch or late into the night.  The feeling is often that when you are "in the zone" then you want to make the most of it and keep going.

Most people consider this to be a good thing and that it means they are being productive.  While it may be true that they are writing lots of code, it doesn't follow that they must be writing *good* code.  It usually means that the person is currently juggling lots of aspects of an intricate piece of code and doesn't want to take their attention away in case they lose track of what they are doing.  That suggests they are very much thinking in terms of *how* the code will work, rather than *what* it is intended to achieve.

In my experience, the results are usually complex pieces of code that are not obvious in what they do.  The argument that it will be refactored later is a very poor one.  As we all know, work has many pressures and the first thing to suffer under the strain is time to review and clean up code.

It is much better to be creating clean code right from the start.  Think about *what* you want your code to achieve rather than *how* it will achieve it.  When you are writing a function, either it will be immediately obvious what the content needs to be, or you will be able to describe what it needs to do.  In the latter case, you just need to create code that describes what you want to achieve and you are done.  Make each part of the description the name of another function.  You'll have successfully split the code into smaller chunks that are easier to think about.

The most important aspect of all of this, in my opinion, is that when you concentrate more on the *what* rather than the *how*, then you are more able to take breaks.  Having breaks from coding sessions is extremely important.  Furthermore, you are much less likely to be building technical debt for the future.

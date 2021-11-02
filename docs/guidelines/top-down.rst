Top-Down or Bottom-Up?
======================

It seems that software engineers are pretty split when it comes to top-down or bottom-up development.

I plan to convince you that a top-down approach is far superior, however let's have a look at what bottom-up can achieve first.

:index:`Bottom-Up Development`
------------------------------

A bottom-up approach tends to occur in one of two scenarios.  The first of these is in pure research.  In this area, you don't necessarily have a goal in mind, or even have an idea where your work is likely to lead you.

You start off with a number of known building blocks.  You try various ways of combining these to see what the results are.  Sometimes, something useful comes out of your endeavours.  More often, however, the results are meaningless.  Regardless, the outcomes allow you to focus progress.

Eventually, you build up a whole framework of concepts and tools for future research.

Another area is solving problems.  You need a solution and it is not clear how to attain the goal, so you look at what solutions are already available to you and see how you can combine them to solve your original problem.

If you rely on existing building blocks like this, then the solution will be determined by what is already available.  If there are a small number of components, then you will have very little freedom in how you can solve the problem (if, indeed, it is solvable with what is available).  You will often find yourself using components in awkward ways to get them to help with the solution.  This approach can also be overwhelming as you try and keep everything in your head so that you can work out how you are putting things together and how all the components will relate to each other.

If you have a rich and varied set of components, then you have a much better chance of finding ones that exactly suit your purpose, though this is not guaranteed.  You are also likely to end up with plenty of components that were not necessary.  If you spent a lot of time creating them, then that time will be wasted.

There is also the matter of testing.  All these components need testing.  The tests for the unused components are more unnecessary work and you are testing components without knowing yet what you need the components for.  How can you be sure that your tests are appropriate?

If you just need an "adequate" solution to a problem to get something done as a one-off and can discard everything afterwards, then this approach can work out to be fairly useful.

In software engineering, if you build an application in this way by creating the low level components first, then you are restricting the way the higher levels of the application can work.  By the time you try to compose the building blocks together, you'll often find yourself making compromises over how to plumb things together.  This is not a good route to understandable and maintainable code.

It is very common, and natural, for software engineers to work in this way, though.  After all, the high level code is just connecting things together.  It is the small components where the interesting coding lies.  When solving problems, we are often reminded of previous tasks (or even of :doc:`Design Patterns </patterns/index>` that we are familiar with) and are sure that the techniques used will help in solving the current problem.  We leap at the chance to get straight in to writing that low-level code.

I urge you not to get drawn into this approach.  While working on these small components can feel very worthwhile, and can often make us feel great when we have solved a tricky little bit of coding, it is distracting from the real goal: that of creating a working, useful application for *someone else*.  Software engineering is not about *you*.

:index:`Top-Down Development`
------------------------------

The alternative is top-down development.  This is the traditional *divide and conquer* approach which I like to refer to as *lazy programming*.

The idea here is that most problems to solve and applications to create are fairly large and too unwieldy for you to keep all in your head at once.  You can easily feel overwhelmed by it.  Instead of rushing in trying to work out the details, try to step back and just think in terms of what needs to be achieved.

If you need to process a collection of data, then a loop over the data calling a processing function on each item is all you need.  The details of that function can be left until later:

.. code-block:: java

  public void doProcessing(List<Thing> things) {
    for (Thing thing : things) {
      process(thing);
    }
  }

If you need to achieve a number of tasks sequentially (say, A then B then C), then these just need to be method calls for those tasks:

.. code-block:: java

  public void doProcessing() {
    doA();
    doB();
    doC();
  }

If there are a lot of things that need to be achieved, then you should be able to group them.  You then just need to achieve those phases, each of which will now be a small list of tasks.

With this approach, you are only creating components that you really need.  Also, the interfaces to those components exactly fit how the higher level code wants to be able to call in to them.

This also lends well to good testing.  Since you are defining what the lower level functionality needs to achieve before writing it, then you know exactly how it should behave.  You can write tests before writing the code to ensure that it meets those requirements.  This is the heart of Test Driven Development and means you are creating *exactly* the components you need and have confidence in them providing correct functionality.

Eventually, you will certainly have components that do actual work.  Following this process through, however, will mean those functioning components will be very small.  You'll usually find they write themselves since, by that point, there is usually only one way they could be written.

This may not seem very satisfying - code writing itself and, seemingly, no space for your creativity to flourish.  Remember, though, that your goal is to provide a working solution for *someone else* that can easily be understood and maintained by others.

If people look at your code and say "wow, that's amazing, I could never create that" then they are not going to be able to easily maintain it.  Instead, you want them to be saying "well, obviously that's what you'd do".  That doesn't give your ego the boost that the previous comment would, but it tells you that they understand your code and could maintain it.

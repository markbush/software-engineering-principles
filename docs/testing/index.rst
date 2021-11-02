Testing
=======

When creating code, it is clearly important that what we create is correct.  Testing is the process by which we ensure this.  There are two expressions which always raise alarm bells with me.  These are "testing code" and "test coverage".  This might be the opposite of what most people would think, so let me explain what I mean.

Both of these expressions tend to imply that the code comes first.  That is, that there is existing code and that there needs to be tests to confirm it is performing as expected.  This is especially true of "test coverage".  The result is that we end up assuming the code works and we write the test to fit that assumption.  If the test fails, then it is the test that is wrong and needs to be updated to fit what the code is doing.

While it is very much the case that a test can be wrong (and should, therefore, be changed to comply with expectations), if the code existed first, then the test is not providing any value.  Sure, it might tell us if something changes in the future, but right now, it is not actually telling us if the code is correct.  It just affirms the assumed truth of the code.

When striving for "test coverage", we usually end up with all sorts of contrived tests just to ensure that every line of actual code has a way of affecting some test case.  This produces very fragile tests since the implementation details of the code may change and either the tests will break because the assumptions about how to exercise those specific lines of code have changed, or some of the tests will now be superfluous since they are now no longer testing aything in addition to other tests.

A much better approach is Test Driven Development.  This is a process where we write the tests in advance of the code under test.  It is very much misunderstood and I will try to explain the idea and purpose here.

Sometimes, we are faced with an application which is already completed.  Or, at least, large parts of it are.  For systems which have been created with time pressures, it is common for testing to have taken a back seat.  There is then a scramble to create tests in order to have confidence in what was created.  As I have argued, tests written in this way do not really provide this confidence if they are only being written to say they exist or to claim a certain level of coverage.

Since this is so common, I will also describe how we can approach solving this in a way which actually does give confidence in what we are doing.

.. toctree::
   :maxdepth: 2
   :hidden:

   tdd
   legacy

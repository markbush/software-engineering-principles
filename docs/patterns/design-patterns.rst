What are Design Patterns?
=========================

Whenever we find ourselves solving problems, we notice that some types of problem occur again and again.  Over time, we begin to recognise these repeating *patterns*.  We can then either directly reuse the solution we remember, or adapt it slightly for our needs.  These common patterns have become known as *design patterns*.

Some patterns are so simple and obvious that we don't think of them as such.  For example, naming variables according to the *role* they will play.  Others, we might think of as simple *tips and tricks* that we have picked up over time.  Many more lie as yet undiscovered.  Over time, they will be discovered and move from the unknown, to the known.  If used often enough, they may even be remembered!

There are a couple of key things to remember about design patterns.

Firstly, never force a pattern onto a problem.  Even if the problem looks identical to the description of the pattern.  Check that the solution makes sense in context.  That it will be easy for someone to come along later and understand.  When used inappropriately, they become *anti-patterns*, making code less understandable and harder to maintain.

Secondly, using patterns is a key to :index:`lazy programming` (a most desirable thing).  Whenever you need to solve a problem, your first thought should be "is it likely that something like this has been solved before?"  If so, then there is likely to be either a language feature, framework, application component, or pattern that will provide your solution for you.  Reuse existing code or ideas where possible.

I will not list all design patterns you might come across here.  I intend to stick to ones that usually have challenging descriptions or where it is not clear exactly how they might be related to typical situations.

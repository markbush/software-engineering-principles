:index:`Inversion of Control`
=============================

A typical piece of code might have the general structure:

.. code-block:: java

  public void doTheThings() {
    doThingOne();
    if (thingTwoRequired()) {
      doThingTwo();
    }
    doThingThree();
  }

The code knows exactly what needs to happen and where that code is.  This piece of code is in control of the whole process.

For precise requirements, this is perfectly fine, which is why most code looks like this.

If requirements start changing, then we can look for patterns in the changes.  For example, suppose that the above code has to become this under certain situations:

.. code-block:: java

  public void doTheThings() {
    if (thingOneRequired()) {
      doThingOne();
    }
    if (thingTwoRequired()) {
      doThingTwo();
    }
    if (thingThreeRequired()) {
      doThingThree();
    }
  }

This is starting to look a mess!  We can see a pattern emerging, though.  Clearly, there are a number of steps that need to be achieved and mechanisms for determining which ones are needed.  If this code continues to be in control, the problem will escalate.  Instead, we can view the steps as components in recipes.  The conditions are selecting which components form the specific recipe we need to follow in a given situation.

We can rewrite this as:

.. code-block:: java

  public void doTheThings(Recipe recipe) {
    for (Step step : recipe.steps()) {
      step.perform();
    }
  }

We are no longer in control of which steps to perform.  That has been given to the layer above which is, presumably, responsible for either creating the recipe, or selecting one from a known collection of them.

This code is still going to perform the same function.  It no longer controls precisely what or when.  Control has been *inverted*.  The result is that it is much less likely that this code will ever need to change again.  Changes will be related to new recipes.  We could imagine some managed mapping of situations to recipes which we might be able to externalise, turning into application configuration.

This is a specific example of how we can use inversion of control in a very specific situation.  (If we found ourselves doing this on several occasions, we could consider it a pattern and call it the *Recipe Pattern*.)  There are a number of well known design patterns which use inversion of control and we'll discuss some of these individually here:

* :doc:`Dependency Injection <ioc-injection>`
* The :doc:`Factory Pattern <ioc-factory>`
* The :doc:`Strategy Pattern <ioc-strategy>`
* The :doc:`Template Pattern <ioc-template>`

.. toctree::
   :maxdepth: 2
   :hidden:

   ioc-injection
   ioc-factory
   ioc-strategy
   ioc-template

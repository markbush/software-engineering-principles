The :index:`Factory Pattern`
============================

We often find ourselves writing code like the following:

.. code-block:: java

  public Response process(Thing thing) {
    if (thing.isOne()) {
      return doOneThing(thing.getOneValue());
    } else if (thing.isTwo()) {
      return doTwoThing(thing.getType(), thing.getLocation());
    } else {
      doOtherThing();
      return new Response();
    }
  }

This function has clearly got things in hand.  It is even delegating responsibility for getting things done to other functions.  Plenty of boxes being ticked.  And yet looking at it raises the hackles.  You get a sinking feeling in the pit of your stomach as you realise this is going to end up a maintenance nightmare.  You can feel your future self looking over your shoulder with dismay.

Well, firstly, we can recognise that the things to do are each a separate responsibility.  They each deserve to be encapsulated in their own class.  That will clean up the rest of this class, but not the above method.  What we need to do is delegate the *structure* of the method.  A perfect way to achieve this is with a factory.

A factory is something which, as its name suggests, creates new things.  It is given specific requests and knows exactly how to create the right thing for that request.  Note that a factory doesn't actually *do* anything (other than create things).  It doesn't make any assumptions about what you want the things for.  It just builds them for you.

For small applications, or when the factory is used at the top level to control the entire operation, it is common for the factory to be implemented as a singleton.  In larger applications or where the factory may be required in lower level code, it is much better for the factory to be replaceable to help with testing.  We can then use :doc:`injection <ioc-injection>` to make it available.

A typical factory contains conditionals that make use of the input to determine which object to create and return like this:

.. code-block:: java

  public class ThingHandlerFactory implements ThingFactory {
    public ThingHandler thingFor(ThingEvent event) {
      switch (event.type()) {
        case ThingType.ONE:
          return new ThingOneHandler(event);
          break;
        case ThingType.TWO:
          if (event.isA()) {
            return new ThingTwoAHandler(event);
          } else {
            return new ThingTwoBHandler(event);
          }
          break;
        case ThingType.THREE:
          return new ThingThreeHandler(event);
          break;
        default:
          throw new UnmatchedThingException(event);
          break;
      }
    }
  }

Note that it is fine for the factory to make specialised things if the situation merits it.  The factory should not need extra information for this.  If it did, that would suggest the distinction should be the responsibility of another layer.  The output of a factory should only be determined by the input.

The original code would now look something like this:

.. code-block:: java

  public Response process(ThingEvent thingEvent) {
    ThingHandler thingHandler = thingHandlerFactory.thingFor(thingEvent);
    return thingHandler.process();
  }

The code is no longer in control of what is done or how.  That control has been delegated to the factory and the handlers.  It is just responsible for ensuring that something *is* done.  Your future self is looking much happier.  Is that a thumbs-up you're getting?

As for the factory, now that the selection control is encapsulated, you can choose other ways to implement it, if appropriate.  For example, you could have the mapping from event type to class in some configuration file.

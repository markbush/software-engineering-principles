:index:`Dependency Injection`
=============================

The whole purpose of object-oriented programming is to have a population of objects that communicate with each other as they collaborate to perform a task.  At some point, those objects have to be created.  This can lead to code like this:

.. code-block:: java

  public class ThingSupport {
    public void doTheThing(Thing thing) {
      ThingHandler handler = new ThingHandler();
      handler.process(thing);
    }
  }

When the objects being created, and the requirements of them, are simple, then this is perfectly fine.  It is not long, however, before we decide that we need to use an object of a different, but related, class to do the work.  The thing is, we don't actually *care* what does the work, as long as it gets done.

At the application level, we might only have one option available to us, so it might seem reasonable to reference it directly like this.  If we want to replace the handler here, it is not so difficult.  But what if this handler is used in several places?  We have created very tight :index:`coupling` between our code and the class that can do what we need.  If we change our mind, then we could have a number of places where we need to make changes.

A first step in changing this would be to provide the object in question as an argument:

.. code-block:: java

  public class ThingSupport {
    public void doTheThing(Thing thing, Handler handler) {
      handler.process(thing);
    }
  }

This code is no longer in control of determining exactly what class of object to use.  It can be reused with multiple handlers as necessary.  The specific handler has been *injected* into the function.  (This is a very common option when the value to be injected is a function!)

If it makes sense for the caller to know what specific handler to use, then this works well.  But what if the caller has no idea about handlers?  Then all we have done is move the coupling.

In this situation, it is usually the case that there is only one choice of handler anyway.  But it may need to change later.  For example, suppose the handler is currently interfacing with files, but later will use a database.  Eventually, it might use a web service.  Each of these implementations would probably have class names describing their nature - we wouldn't be likely to just replace the internal implementation of the single handler class.

What we need is some global configuration that says *when we need a handler anywhere,* **this** *is the current class we are using*.  There are two common ways of implementing this.  One is very similar to the :doc:`Factory Pattern <ioc-factory>`:

.. code-block:: java

  public class HandlerProvider implements Provider {
    public ThingHandler thingHandler() { return new FileThingHandler(); }
  }

  public class ThingSupport {
    public void doTheThing(Thing thing) {
      ThingHandler handler = handlerProvider.thingHandler();
      handler.process(thing);
    }
  }

The difference to a factory is that there is no provided information to specify which object to build and return.  The selection is done via distinct methods for each outcome.

The :code:`HandlerProvider` is a configuration file written in code.  We can easily change implementations used by the rest of the application.  We should be careful to ensure that this configuration can easily be replaced for testing, so that we can control specific objects to be used by code under test.

Another common way is to use automatic injection.  We can do this because this is such a common scenario that the Java language has built in features to support it.  For example, we can declare that we need a handler, without needing any reference to *how* we obtain it as follows:

.. code-block:: java

  import javax.inject.Inject;

  public class ThingSupport {
    @Inject private ThingHandler handler;
    public void doTheThing(Thing thing) {
      handler.process(thing);
    }
  }

This mechanism is only suitable if we really don't care about the item being injected and just want to use it as some opaque service provider.  Otherwise, the code becomes obfuscated and we feel we need to keep looking at the implementation of things in order to understand what is going on.

Several frameworks exist to manage this for us and they may have their own annotations to ensure successful implementation (such as :code:`@Autowired` in `Spring <https://spring.io>`_).  These frameworks often allow us to give extra hints in case we need different implementations in different places of our code.

We can often configure these frameworks at run time using an external file.  This has the advantage that we can run the same application in multiple contexts where different classes would be needed to provide the same functionality.  The disadvantage is that the configuration is now inaccessible to the compiler, so we no longer have compile-time checks that we are specifying things correctly.  A typo in the configuration will result in a runtime error which might occur much later and in a way that is hard to debug.

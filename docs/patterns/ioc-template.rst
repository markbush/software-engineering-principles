The :index:`Template Pattern`
=============================

With the :doc:`Strategy Pattern <ioc-strategy>`, we saw that we can easily delegate components of a process to subclasses if those components are related to each other.  Suppose, however, that we need to do something like the following where the processing at the start and end are independent of each other:

.. code-block:: java

  public abstract class ThingProcessor implements Processor {
    abstract protected void doPreProcessing(Thing thing);
    abstract protected void doPostProcessing(Thing thing);
    public void process(Thing thing) {
      doPreProcessing(thing);
      for (Step step : thing.steps()) {
        step.perform();
      }
      doPostProcessing(thing);
    }
  }

If we created a whole load of subclasses for all the available combinations of options, then we could end up with an explosion of classes and an enormous amount of repetition.  We couldn't factor it all out in a hierarchy because we might need all possible combinations.  The code selecting the subclasses would also become unwieldy, too.

Since the calling code would need to be selecting which subclass to use, it knows something about the pre-processing and post-processing necessary.  It can then select appropriate implementations and pass them in like this:

.. code-block:: java

  public class ThingProcessor implements Processor {
    private final PreProcessor preProcessor;
    private final PostProcessor postProcessor;
    public ThingProcessor(PreProcessor preProcessor, PostProcessor postProcessor) {
      this.preProcessor = preProcessor;
      this.postProcessor = postProcessor;
    }
    public void process(Thing thing) {
      preProcessor.process(thing);
      for (Step step : thing.steps()) {
        step.perform();
      }
      postProcessor.process(thing);
    }
  }

Now, each type of processing only needs to be implemented once and we can mix and match as necessary.  The items to fill in are holes in a *template* which are filled in by anyone wanting a concrete version of the control flow.

This technique is common when the components are functions being passed in.  This is the heart of functional programming!

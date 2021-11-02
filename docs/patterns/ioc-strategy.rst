The :index:`Strategy Pattern`
=============================

Often, we have a problem that is very similar to a generic one where there is a reasonably known way of solving it.  We just need to adapt that solution a little.

We then discover that we have a second situation that needs a slightly different adaptation.  Our solution might start looking like this:

.. code-block:: java

  public class ThingProcessor implements Processor {
    public void process(Thing thing, ProcessController controller) {
      doPreparation(thing);
      if (controller.isTypeA()) {
        doPostPrepA(thing);
      } else {
        doPostPrep(thing);
      }
      for (Step step : thing.steps()) {
        step.perform();
        if (!controller.isTypeA()) {
          doExtraStep(step);
        }
      }
      if (controller.isTypeA()) {
        finishProcessing(thing);
      }
    }
  }

Yuk!  The class is definitely in control, but it is micro-managing.  This is certainly not scalable.  Fortunately, we can see a pattern emerging.  This time, we can keep the core of the structure in this class, and implement the adaptations in subclasses.  We just need to add callouts at all places where we need to adapt:

.. code-block:: java

  public abstract class ThingProcessor implements Processor {
    abstract protected void doPostPrep(Thing thing);
    abstract protected void doExtraStep(Step step);
    abstract protected void finishProcessing(Thing thing);
    public void process(Thing thing) {
      doPreparation(thing);
      doPostPrep(thing);
      for (Step step : thing.steps()) {
        step.perform();
        doExtraStep(step);
      }
      finishProcessing(thing);
    }
    protected void doPreparation(Thing thing) {
    }
  }
  public class GeneralThingProcessor extends ThingProcessor {
    @Override protected void doPostPrep(Thing thing) {
    }
    @Override abstract protected void doExtraStep(Step step) {
    }
    @Override abstract protected void finishProcessing(Thing thing) {
    }
  }
  public class ThingAProcessor extends ThingProcessor {
    @Override protected void doPostPrep(Thing thing) {
    }
    @Override abstract protected void doExtraStep(Step step) {
    }
    @Override abstract protected void finishProcessing(Thing thing) {
    }
  }

The controller is no longer required (in this scenario).  It is used by the caller to determine which of the specific processors to use to process the item.

Each of the subclasses is a different *strategy* for solving the problem.  Sometimes, we can determine precisely which one to use in a given situation, as above.  There are times, however, when we might want to run several strategies to see which is best before doing something with the results.

For the Strategy Pattern to be meaningful, the implementations of all of the abstract methods need to be relatable in some way.  A particular class encapsulates all of the information about a particular way of adapting the solution.  If the implementations of these methods are independent of each other, then we may end up with the number of strategies growing exponentially.  In that case, we would be better off using the :doc:`Template Pattern <ioc-template>`.
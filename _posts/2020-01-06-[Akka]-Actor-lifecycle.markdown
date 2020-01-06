---
layout: post
title:  "[Akka] Actor lifecycle"
categories: akka
---
The actor will stay in the `Started` state until it's stopped, at which point the actor is in the `Terminated` state.

- `Created` → `preStart()` → `Started` → `Stopped` → `postStop()` → `Terminated`
- `Created` → `preStart()` → `Started` → `preRestart()` → `Stopped` → `postStop()` → `postRestart()` → `preStart()` → `Started` → `Stopped` → `postStop()`

### Methods in `trait Actor {}`
```scala
trait Actor {
  // ...

  /**
   * User overridable callback.
   * <p/>
   * Is called when an Actor is started.
   * Actors are automatically started asynchronously when created.
   * Empty default implementation.
   */
  @throws(classOf[Exception]) // when changing this you MUST also change ActorDocTest
  //#lifecycle-hooks
  def preStart(): Unit = ()

  //#lifecycle-hooks

  /**
   * User overridable callback.
   * <p/>
   * Is called asynchronously after 'actor.stop()' is invoked.
   * Empty default implementation.
   */
  @throws(classOf[Exception]) // when changing this you MUST also change ActorDocTest
  //#lifecycle-hooks
  def postStop(): Unit = ()

  //#lifecycle-hooks

  /**
   * Scala API: User overridable callback: '''By default it disposes of all children and then calls `postStop()`.'''
   * @param reason the Throwable that caused the restart to happen
   * @param message optionally the current message the actor processed when failing, if applicable
   * <p/>
   * Is called on a crashed Actor right BEFORE it is restarted to allow clean
   * up of resources before Actor is terminated.
   */
  @throws(classOf[Exception]) // when changing this you MUST also change ActorDocTest
  //#lifecycle-hooks
  def preRestart(@unused reason: Throwable, @unused message: Option[Any]): Unit = {
    context.children.foreach { child =>
      context.unwatch(child)
      context.stop(child)
    }
    postStop()
  }

  //#lifecycle-hooks

  /**
   * User overridable callback: By default it calls `preStart()`.
   * @param reason the Throwable that caused the restart to happen
   * <p/>
   * Is called right AFTER restart on the newly created Actor to allow reinitialization after an Actor crash.
   */
  @throws(classOf[Exception]) // when changing this you MUST also change ActorDocTest
  //#lifecycle-hooks
  def postRestart(@unused reason: Throwable): Unit = {
    preStart()
  }
  //#lifecycle-hooks

  // ...
}
```

### When overriding `preRestart`, `postRestart`  hooks.

Be careful when overriding these hooks, have to call the super implementation.

```scala
override def preRestart(reason: Throwable, message: Option[Any]): Unit = {
  println("preRestart")
  super.preRestart(reason, message)
}

override def posotRestart(reason: Throwable): Unit = {
  println("postRestart")
  super.postRestart(reason)
}
```

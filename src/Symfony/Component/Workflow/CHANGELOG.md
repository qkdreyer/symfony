CHANGELOG
=========

4.3.0
-----

 * Trigger `entered` event for subject entering in the Workflow for the first time.
 * Added a context to `Workflow::apply()`. The `MethodMarkingStore` could be used to leverage this feature.
 * The `TransitionEvent` is able to modify the context.
 * Add style to transitions by declaring metadata:

    use Symfony\Component\Workflow\Definition;
    use Symfony\Component\Workflow\Metadata\InMemoryMetadataStore;

    $transitionsMetadata = new \SplObjectStorage();
    $transitionsMetadata[$transition] = [
        'color' => 'Red',
        'arrow_color' => '#00ff00',
    ];
    $inMemoryMetadataStore = new InMemoryMetadataStore([], [], $transitionsMetadata);

    return new Definition($places, $transitions, null, $inMemoryMetadataStore);
 * Dispatch `GuardEvent` on `workflow.guard`
 * Dispatch `LeaveEvent` on `workflow.leave`
 * Dispatch `TransitionEvent` on `workflow.transition`
 * Dispatch `EnterEvent` on `workflow.enter`
 * Dispatch `EnteredEvent` on `workflow.entered`
 * Dispatch `CompletedEvent` on `workflow.completed`
 * Dispatch `AnnounceEvent` on `workflow.announce`
 * Added support for many `initialPlaces`
 * Deprecated the `MultipleStateMarkingStore` class, use the `MethodMarkingStore` instead.
 * Deprecated the `SingleStateMarkingStore` class, use the `MethodMarkingStore` instead.

4.1.0
-----

 * Deprecated the `DefinitionBuilder::reset()` method, use the `clear()` one instead.
 * Deprecated the usage of `add(Workflow $workflow, $supportStrategy)` in `Workflow/Registry`, use `addWorkflow(WorkflowInterface, $supportStrategy)` instead.
 * Deprecated the usage of `SupportStrategyInterface`, use `WorkflowSupportStrategyInterface` instead.
 * The `Workflow` class now implements `WorkflowInterface`.
 * Deprecated the class `ClassInstanceSupportStrategy` in favor of the class `InstanceOfSupportStrategy`.
 * Added TransitionBlockers as a way to pass around reasons why exactly
   transitions can't be made.
 * Added a `MetadataStore`.
 * Added `Registry::all` to return all the workflows associated with the
   specific subject.

4.0.0
-----

 * Removed class name support in `WorkflowRegistry::add()` as second parameter.

3.4.0
-----

 * Added guard `is_valid()` method support.
 * Added support for `Event::getWorkflowName()` for "announce" events.
 * Added `workflow.completed` events which are fired after a transition is completed.

3.3.0
-----

 * Added support for expressions to guard transitions and added an `is_granted()`
   function that can be used in these expressions to use the authorization checker.
 * The `DefinitionBuilder` class now provides a fluent interface.
 * The `AuditTrailListener` now includes the workflow name in its log entries.
 * Added `workflow.entered` events which is fired after the marking has been set.
 * Deprecated class name support in `WorkflowRegistry::add()` as second parameter.
   Wrap the class name in an instance of ClassInstanceSupportStrategy instead.
 * Added support for `Event::getWorkflowName()`.
 * Added `SupportStrategyInterface` to allow custom strategies to decide whether
   or not a workflow supports a subject.
 * Added `ValidateWorkflowPass`.
---
uid: General_Main_Release_10.2.0_CU18
---

# General Main Release 10.2.0 CU18 – Preview

> [!IMPORTANT]
> We are still working on this release. Some release notes may still be modified or moved to a later release. Check back soon for updates!

> [!TIP]
> For information on how to upgrade DataMiner, see [Upgrading a DataMiner Agent](xref:Upgrading_a_DataMiner_Agent).

### Enhancements

#### DataMiner upgrade: New upgrade action added that will clean up default ListView column configuration data [ID_36475]

<!-- MR 10.2.0 [CU18]/10.3.0 [CU6] - FR 10.3.9 -->

During a DataMiner upgrade, from now on, all default ListView column configuration data left on the server will automatically be cleaned up if no more than one Cube client has taken a copy of that data.

#### SLLogCollector will now also collect the scheduled tasks configured in Microsoft Task Scheduler [ID_36645]

<!-- MR 10.2.0 [CU18]/10.3.0 [CU6] - FR 10.3.9 -->

SLLogCollector will now also collect the scheduled tasks configured in Microsoft Task Scheduler.

#### Smart baselines: Information event generation at 5-minute intervals has been disabled [ID_36691]

<!-- MR 10.2.0 [CU18]/10.3.0 [CU5] - FR 10.3.8 -->

When smart baselines were configured, by default information events would be generated every 5 minutes. This information event generation has now been disabled to avoid information event floods in e.g. EPM environments.

#### DataMiner upgrade: Presence of Visual C++ 2010 redistributable will no longer be checked [ID_36745]

<!-- MR 10.2.0 [CU18]/10.3.0 [CU6] - FR 10.3.9 -->

During a DataMiner upgrade, from now on, the presence of the Visual C++ 2010 redistributable will no longer be checked.

#### DataMiner Cube - Resources: Enhanced logging when function resources failed to initialize [ID_36763]

<!-- MR 10.2.0 [CU18]/10.3.0 [CU6] - FR 10.3.9 -->

A more detailed entry will now be added to the Cube logging when a function resource failed to initialize.

#### SLWatchdog: Additional logging & retry mechanism for restarts [ID_36839]

<!-- MR 10.2.0 [CU18]/10.3.0 [CU6] - FR 10.3.9 -->

When SLWatchdog starts, restarts or stops DataMiner, extra information will now be logged to help pinpoint certain issues that may arise:

- the SLDataMiner process ID,
- the output of the batch scripts that are being executed while DataMiner is (re)starting,
- etc.

Also, if DataMiner did not start up correctly for some reason, a retry will now be attempted in that same startup routine.

In the `C:\Skyline DataMiner\Tools` folder, you can also find the following new startup scripts:

- *DataMiner Start DataMiner And SLNet.bat*
- *DataMiner Start DataMiner.bat*

### Fixes

#### Failover: Problems when running BPA tests [ID_36445]

<!-- MR 10.2.0 [CU18]/10.3.0 [CU6] - FR 10.3.9 -->

When the backup agent was active, certain BPA tests would incorrectly return the following error:

`This BPA does not apply for this Agent: cannot run on Offline Failover Agents`

Also, certain managers in SLNet (e.g. BPA Manager) would not properly initialize if the following Failover settings were configured in the *SLDMS.xml* file:

- `State="Offline"`
- `StateBeforeShutDown="Online"`

#### SNMPv3 credentials would not get deleted when an SNMPv3 element was deleted [ID_36573]

<!-- MR 10.2.0 [CU18]/10.3.0 [CU6] - FR 10.3.9 -->

When an SNMPv3 element was deleted, its SNMPv3 credentials would incorrectly not get deleted. Also, when users were deleted, their DCP credentials would not get deleted.

#### DataMiner Cube: Report or dashboard would not be selected after 'Email', 'Upload to FTP' or 'Upload to shared folder' action was initialized [ID_36631]

<!-- MR 10.2.0 [CU18]/10.3.0 [CU6] - FR 10.3.9 -->

In *Automation*, *Correlation* and *Scheduler*, you can select a report of a dashboard in an *Email*, *Upload to FTP* or *Upload to shared folder* action. When such an action was initialized, in some rare cases, the report or dashboard would not be automatically selected.

#### Dashboards app: Black boxes on top of first or last field of selection boxes on small screens [ID_36738]

<!-- MR 10.2.0 [CU18]/10.3.0 [CU6] - FR 10.3.9 -->

When you reduced the screen size to the point at which the navigation pane got hidden, a black box would incorrectly appear on top of the first or last field of a selection box.

#### NT Notify type NT_ADD_VIEW could be executed with an invalid parent view ID [ID_36739]

<!-- MR 10.2.0 [CU18]/10.3.0 [CU6] - FR 10.3.9 -->

Up to now, when an `NT_ADD_VIEW` call was executed with `parentViewID` set to a non-existing view ID, the newly added view would not be visible in the Surveyor. Hence, there was no way of correcting the situation using the UI. Cube logging would include a warning that a `parentViewID` cannot be resolved.

Validation has now been added to `NT_ADD_VIEW`. When a request enters to create a view with an invalid parent view ID, the view will not be created. Also, views with an invalid parent view ID will now be placed directly under the root view. This will allow you to drag the view to its correct location, updating its parent view ID to a valid ID in the process. An error will also be logged and the *View Recursion* BPA test will report the view in question.

#### Low-Code Apps: Creating an app with an existing name would incorrectly be possible [ID_36744]

<!-- MR 10.2.0 [CU18]/10.3.0 [CU6] - FR 10.3.9 -->

Up to now, it would incorrectly be possible to create a low-code app with a name that was identical to that of an existing app.

From now on, when you try to create an app with a name that is identical to that of an existing app, an error will be thrown.

#### DataMiner Cube - Trending: Panning across the graph would not work [ID_36769]

<!-- MR 10.2.0 [CU18]/10.3.0 [CU6] - FR 10.3.9 -->

When you opened a trend graph showing trend data of a parameter that only had average trending enabled, in some cases, it would not be possible to pan across the graph.

#### Dashboards app: Problem when clicking 'Start with a blank dashboard' [ID_36798]

<!-- MR 10.2.0 [CU18]/10.3.0 [CU6] - FR 10.3.9 -->

When you clicked *Start with a blank dashboard* twice in rapid succession, two pop-up windows would open.

#### DataMiner Cube - Visual Overview: Problem with [this EnhancedServiceID] placeholder [ID_36808]

<!-- MR 10.2.0 [CU18]/10.3.0 [CU6] - FR 10.3.9 -->

In some cases, the *[this EnhancedServiceID]* placeholder would not resolve correctly when used inside another placeholder.

For example, when you had specified `[param: [this EnhancedServiceID], 1]`, the parameter of the service element with parameter ID 1 would not be displayed correctly in the shape text.

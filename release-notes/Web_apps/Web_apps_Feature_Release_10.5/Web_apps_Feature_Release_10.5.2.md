---
uid: Web_apps_Feature_Release_10.5.2
---

# DataMiner web apps Feature Release 10.5.2 – Preview

> [!IMPORTANT]
> We are still working on this release. Some release notes may still be modified or moved to a later release. Check back soon for updates!

> [!TIP]
>
> - For release notes related to the general DataMiner release, see [General Feature Release 10.5.2](xref:General_Feature_Release_10.5.2).
> - For release notes related to DataMiner Cube, see [DataMiner Cube Feature Release 10.5.2](xref:Cube_Feature_Release_10.5.2).

## Highlights

*No highlights have been selected yet.*

## New features

## Changes

### Enhancements

#### Web apps: Angular and other dependencies have been upgraded [ID 41488]

<!-- MR 10.4.0 [CU11] - FR 10.5.2 -->

In all web apps (e.g. Low-Code Apps, Dashboards, Monitoring, etc.), Angular and other dependencies have been upgraded.

#### Video thumbnails will now have a default volume of 100% [ID 41597]

<!-- MR 10.4.0 [CU11] - FR 10.5.2 -->

Video thumbnails will now have a default volume of 100%.

Up to now, when you clicked the sound icon of a video thumbnail, the video would unmute, but the volume would stay at 0%. From now on, when a video is unmuted, its volume will be at 100%.

### Fixes

#### Dashboards/Low-Code Apps - Timeline component: Boundaries of the vertical timeline sections would not be correct [ID 41514]

<!-- MR 10.4.0 [CU11] - FR 10.5.2 -->

In some cases, the boundaries of the vertical timeline sections would not be correct. For example, one-month sections would not start on the first day of the month.

#### Dashboards app: Dashboard lists would incorrectly not be shown on mobile devices [ID 41548]

<!-- MR 10.4.0 [CU11] - FR 10.5.2 -->

When you opened the Dashboards app on a mobile device, none of the following dashboard lists would be shown:

- Overview
- Recent
- Private
- Shared

#### Web API: Client applications would not receive any new events due to a WebSocket clean-up issue [ID 41560]

<!-- MR 10.4.0 [CU11] - FR 10.5.2 -->

Due to a WebSocket clean-up issue, in some rare cases, client applications would incorrectly not receive any new events.

#### Dashboards/Low-Code Apps - Visual overview component: Loading indicator would not be shown [ID 41565]

<!-- MR 10.4.0 [CU11] - FR 10.5.2 -->

In some cases, a *Visual overview* component would incorrectly not show any loading indicator when it was loading a visual overview.

#### Dashboards app: Users without access to the root folder would see a 'Loading' bar in the navigation pane [ID 41566]

<!-- MR 10.4.0 [CU11] - FR 10.5.2 -->

When you had not been granted access to the root folder, the navigation pane would keep on showing a "Loading" bar.

#### Low-Code Apps: State of newly created duplicate would be 'published' instead of 'draft' [ID 41623]

<!-- MR 10.4.0 [CU11] - FR 10.5.2 -->

When you duplicated a published app, and then previewed the newly created duplicate, in the version history, its state would incorrectly be set to "published" instead of "draft".

#### Dashboards/Low-Code Apps - Visual overview component: Problem when changing the page to be displayed to the first page of the Visio file [ID 41628]

<!-- MR 10.4.0 [CU11] - FR 10.5.2 -->

When, in the settings of a *Visual overview* component, you changed the page to be displayed to the first page of the Visio file (i.e. page 0), up to now, the component would incorrectly continue to display the page that was selected before.

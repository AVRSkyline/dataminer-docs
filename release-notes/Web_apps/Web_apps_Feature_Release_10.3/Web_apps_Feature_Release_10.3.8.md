---
uid: Web_apps_Feature_Release_10.3.8
---

# DataMiner web apps Feature Release 10.3.8 – Preview

> [!IMPORTANT]
> We are still working on this release. Some release notes may still be modified or moved to a later release. Check back soon for updates!

> [!TIP]
> For release notes for this release that are not related to the web applications, see [General Feature Release 10.3.8](xref:General_Feature_Release_10.3.8).

## Highlights

*No highlights have been selected for this release yet*

## Other features

*No other features have been added yet*

## Changes

### Enhancements

#### Monitoring app: Parameter values that are URLs will now be rendered as clickable hyperlinks [ID_36423]

<!-- MR 10.4.0 - FR 10.3.8 -->

From now on, when a parameter value is a URL starting with one of the following prefixes it will be rendered as a clickable hyperlink:

- file://
- ftp://
- http://
- https://
- mailto://

#### Low-Code Apps - Action editor: 'Which scheduler?' button has now been renamed to 'Which timeline?' [ID_36530]

<!-- MR 10.3.0 [CU5] - FR 10.3.8 -->

In the action editor, the *Which scheduler?* button has now been renamed to *Which timeline?*.

#### Dashboards app & Low-Code Apps - Clock components: Custom time zone [ID_36534]

<!-- MR 10.4.0 - FR 10.3.8 -->

When configuring an analog or digital *Clock* component, you can now make the clock display the date and time in a specific time zone.

To do so, select the *Custom time zone* option, and select a time zone from the *Time zone* selection box.

### Fixes

#### Dashboards app & Low-Code Apps: Only one of the tables sharing an empty query would show a visual replacement [ID_36233]

<!-- MR 10.4.0 - FR 10.3.8 -->

When an empty query was used by more than one table component, in some rare cases, only one of those components would display a visual replacement.

#### Low-Code Apps: A blank screen would appear when users without permission to access a low-code app tried to log on [ID_36422]

<!-- MR 10.4.0 - FR 10.3.8 -->

When users without permission to access a low-code app tried to log on to that app, an error would be thrown and a blank screen would appear. From now on, when users without permission to access a low-code app try to log on to that app, an appropriate message will appear instead.

#### Low-Code Apps: Application would be updated each time you hit a key after changing a page name [ID_36479]

<!-- MR 10.2.0 [CU17]/10.3.0 [CU5] - FR 10.3.8 -->

When you changed the name of a low-code app page, the application would incorrectly be updated each time you hit a key. From now on, the application will be updated 250 ms after the last keystroke.

#### Dashboards app & Low-Code Apps: Problem when migrating a query to the current GQI version [ID_36552]

<!-- MR 10.3.0 [CU5] - FR 10.3.8 -->

When you opened a query that was created using an older GQI version, and that query was configured to start from another query recursively in combination with joins, in some cases, it would incorrectly be migrated to the current GQI version.

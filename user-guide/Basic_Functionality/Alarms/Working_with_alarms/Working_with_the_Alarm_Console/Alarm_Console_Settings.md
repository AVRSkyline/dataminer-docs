---
uid: AlarmConsoleSettings
---

# Alarm Console settings

To access specific settings for the Alarm Console, click the hamburger button in the top-left corner of the console.

The following settings are available:

- **Automatically remove cleared alarms**: Select to remove alarms from the console automatically as soon as their severity returns to normal. To ensure alarms stay in the console until cleared by the user, clear the selection.

- **History tracking**: Select to attach the life cycle of an alarm to the alarm. To show the alarm history as separate alarm records in the list instead, clear the selection. If this option is selected, you can expand an alarm in the Alarm Console to view all attached alarm records.

  > [!NOTE]
  > When you create a filtered history tab, in a fixed or sliding window, history tracking is off by default. However, if you explicitly enable history tracking in a history tab, a dialog box appears asking if you want to load the full history:
  >
  > - Click *All* to include all alarms in the specified time range in the alarm trees, regardless of the filter.
  > - Click *Filtered* to only include alarms matching the current filter settings.
  >
  > For more information on creating filtered tabs, see [Manually applying an alarm filter in an Alarm Console tab](xref:ApplyingAlarmFiltersInTheAlarmConsole#manually-applying-an-alarm-filter-in-an-alarm-console-tab).

- **Correlation tracking**: Select to hide raw alarms of a correlated alarm. To show the raw alarms as separate alarm records in the list, clear the selection. If this option is selected, you can expand an alarm in the Alarm Console to view all attached alarm records.

  > [!NOTE]
  > In case a filter is applied in the alarm tab, the behavior of this feature is different depending on the type of filter:
  >
  > - If a filtered alarm tab is created (e.g. by dragging an item onto the Alarm Console or by selecting *Apply filter* in a new tab):
  >   - If only the base alarm matches the filter, only that alarm is displayed.
  >   - If only the correlated alarm matches the filter, only that alarm is displayed.
  >   - If both base and correlated alarm match the filter, only the correlated alarm is displayed.
  >   - If neither base nor correlated alarm match the filter, neither are displayed.
  > - If a quick filter is applied with the filter box in the lower right corner, the behavior is similar, except in case both base alarm and correlated alarm match the filter, as then both alarms will be displayed.

- **Automatic incident tracking**: This option is only available in a DMS using Cassandra, and only if automatic incident tracking is enabled in System Center. It is also only available for active alarms, not for history alarms. For more information, see [Automatic incident tracking](xref:Automatic_incident_tracking).

- **Text to speech**: Select to enable Text to speech, so that new alarm events are read out loud.

- **Freeze**: Select to stop displaying new incoming events in the currently selected alarm tab. Other open alarm tabs will not be frozen.

  > [!NOTE]
  > While the alarm tab is frozen, any incoming alarms are kept in a buffer. However, if the buffer should reach more than 10,000 alarms, the Alarm Console will automatically no longer be frozen.

- **Show alarm duration indicator**: Select to show a progress bar in the alarm severity color, indicating how long the alarm has been active in the DMS.

- **Automatically group according to arrangement**: Select to enable automatic grouping by the column header used to sort the alarm list.

- **Full alarm coloring**: Select to give all alarm records a background color indicating the current alarm severity.

- **Show in banner**: Select to display a banner at the top of the Cube window when new alarms enter the tab. The banner shows the number of new alarms, the color of the most severe among them, and service impact information. When you click the banner, the Alarm Console tab will open and the new alarm(s) will be selected.

  > [!NOTE]
  > It is possible to set a delay timer on when the alarm banner hides. For more information, see [User settings](xref:User_settings).

- **Statistical view**: Select to view the alarms in the alarm tab as statistics. For more information, see [Using the statistical view](xref:ChangingTheAlarmConsoleLayout#using-the-statistical-view).

- **Reports view**: This option is only available in a DMS using Cassandra. Select to view severity timelines per element or per parameter. For more information, see [Using the reports view](xref:ChangingTheAlarmConsoleLayout#using-the-reports-view).

- **Show side panel**: Select to show the collapsible side panel in the Alarm Console.

- **Audible alert**: Select to specify a custom alert sound that should be used when a new alarm enters the alarm tab. See [Configuring a custom alert sound for an alarm tab](xref:ConfiguringACustomAlertSoundForAnAlarmTab).

- **Delay**: Select to specify a delay between the creation of a new alarm and its appearance in the selected alarm tab.

  E.g. if you set the delay to 30 seconds, when an alarm enters the Alarm Console, it will only be added to the list 30 seconds later. If in this interval the alarm has already been cleared, it will not be added to the list at all.

  > [!TIP]
  > See also: [Alarm Console – Delay & refresh rate of alarms](https://community.dataminer.services/video/alarm-console-delay-refresh-rate-of-alarms/) on DataMiner Dojo.

- **Refresh rate**: Select to specify how frequently the selected tab will be refreshed. This rate will be applied from the moment this setting is set.

  E.g. if you set the refresh rate to 30 seconds at 11:48:00, the Alarm Console will be updated every 30 seconds with all the alarms that entered during those 30 seconds. The first refresh will take place at 11:48:30, the next at 11:49:00, etc.

  > [!TIP]
  > See also: [Alarm Console – Delay & refresh rate of alarms](https://community.dataminer.services/video/alarm-console-delay-refresh-rate-of-alarms/) on DataMiner Dojo.

- **Merge alarm trees**: This setting is only available if *History tracking* is enabled and *Automatically remove cleared alarms* and *Freeze* are disabled in the alarm tab (from DataMiner 9.6.13 onwards). When these settings are used, by default, when an alarm is cleared and then reappears, this results in a separate alarm tree. Activating *Merge alarm trees* combines these alarm trees, which can result in a better overview, e.g. in a sliding window tab. If you activate the option, you can also select an additional option to only merge alarm trees in case the time between the alarm trees is less than a particular time span (between 1 second and 1 day).

- **Default alarm list**: Select to make the currently selected tab the default tab, i.e. the tab that will be shown when you open DataMiner Cube. If the selected tab is already the default tab, this option will be unavailable.

> [!NOTE]
> To display Alarm Console group statistics, to display a horizontal scrollbar in the alarm list, or to configure the Alarm Console, refer to the general settings in Cube instead. See [User settings](xref:User_settings).

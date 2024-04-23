---
uid: General_Feature_Release_10.4.6
---

# General Feature Release 10.4.6 – Preview

> [!IMPORTANT]
> We are still working on this release. Some release notes may still be modified or moved to a later release. Check back soon for updates!

> [!IMPORTANT]
> When downgrading from DataMiner Feature Release version 10.3.8 (or higher) to DataMiner Feature Release version 10.3.4, 10.3.5, 10.3.6 or 10.3.7, an extra manual step has to be performed. For more information, see [Downgrading a DMS](xref:MOP_Downgrading_a_DMS).

> [!TIP]
>
> - For release notes related to DataMiner Cube, see [DataMiner Cube Feature Release 10.4.6](xref:Cube_Feature_Release_10.4.6).
> - For release notes related to the DataMiner web applications, see [DataMiner web apps Feature Release 10.4.6](xref:Web_apps_Feature_Release_10.4.6).
> - For information on how to upgrade DataMiner, see [Upgrading a DataMiner Agent](xref:Upgrading_a_DataMiner_Agent).

## Highlights

*No highlights have been selected yet.*

## New features

#### MessageBroker: New NATS reconnection algorithm [ID_38809]

<!-- MR 10.5.0 - FR 10.4.6 -->

From now on, when NATS reconnects, it will no longer perform the default reconnection algorithm of the NATS library. Instead, it will perform a custom reconnection algorithm that will do the following:

1. Re-read the NATS configuration file.
1. Update the endpoints to which MessageBroker will connect.

Also, the `NatsSession` class has the following new property:

- *DisconnectedHandler*: Forces NATS to override the handler when disconnecting.

  By setting *DisconnectedHandler* to true, you can force NATS to invoke a custom handler when it disconnects.

  > [!IMPORTANT]
  > When *DisconnectedHandler* is set to true, NATS will not perform the new reconnection algorithm described above. However, it will re-read its configuration.

#### Simple alarm filters can now be translated to Elasticsearch/OpenSearch queries [ID_38898]

<!-- MR 10.4.0 [CU3] - FR 10.4.6 -->

Simple alarm filters (without operators and/or brackets) can now be translated to Elasticsearch/OpenSearch queries. This will increase overall performance of Elasticsearch/OpenSearch queries containing alarm filters as alarm filtering will now be performed by the database itself. Post-filtering query results will no longer be needed.

#### User-defined APIs: An event will now be sent when an ApiToken or ApiDefinition is created, updated or deleted [ID_39117]

<!-- MR 10.5.0 - FR 10.4.6 -->

From now on, the user-defined API manager will send out an event whenever an `ApiToken` or `ApiDefinition` object is created, update or deleted.

| Event name | Description |
|---|---|
| ApiTokenChangedEventMessage      | Generated when an [ApiToken](xref:UD_APIs_Objects_ApiToken) is created, updated, or deleted. |
| ApiDefinitionChangedEventMessage | Generated when an [ApiDefinition](xref:UD_APIs_Objects_ApiDefinition) is created, updated, or deleted. |

When subscribing to event messages, you can use the `SubscriptionFilter` to only receive the messages matching a specific filter. See the following example.

```csharp
// In this example, you will take the Connection object from the script's Engine object
var connection = engine.GetUserConnection();

// Create a random set ID that identifies our subscription
var setId = $"ApiTokenSubscription_{Guid.NewGuid()}"

// Create the filter for the ApiToken events, only enabled tokens should match
var filter = ApiTokenExposers.IsDisabled.Equal(false);
var subscriptionFilter = new SubscriptionFilter<ApiTokenChangedEventMessage, ApiToken>(filter);

// Attach a callback when a new event message arrives
connection.OnNewMessage += (sender, args) =>
{
    // Handle the events
}

// Subscribe
connection.AddSubscription(setId, subscriptionFilter);
```

#### Storage as a Service: Support for data migration towards a STaaS system using a proxy server [ID_39313]

<!-- MR 10.5.0 - FR 10.4.6 -->

As from DataMiner version 10.4.5, Storage as Service (STaaS) supports the use of a proxy server.

From now on, it is also possible to migrate data towards a STaaS system that is using a proxy server.

## Changes

### Enhancements

#### MessageBroker: Each individual chunk will now be sent with a dynamic timeout [ID_38633]

<!-- MR 10.5.0 - FR 10.4.6 -->

When chunked messages are being sent using MessageBroker, from now on, each individual chunk will be sent with a dynamic timeout instead of a static 5-second timeout.

The dynamic timeout will be calculated as the time it would take to send the chunk at a speed of 1 Mbps, rounded up to the nearest second.

> [!NOTE]
> The minimum timeout will always be 5 seconds.

#### Security enhancements [ID_38869]

<!-- 38869: MR 10.5.0 - FR 10.4.6 -->

A number of security enhancements have been made.

#### MessageBroker: 'Subscribe' method of the 'NatsSession' class has now been made completely thread-safe [ID_38939]

<!-- MR 10.5.0 - FR 10.4.6 -->

The *Subscribe* method of the `NatsSession` class has now been made completely thread-safe.

#### Service & Resource Management: Enhanced performance when activating function DVEs [ID_38972]

<!-- MR 10.5.0 - FR 10.4.6 -->

Because of a number of enhancements, overall performance has increased when activating function DVEs.

#### GQI: Errors related to real-time GQI data updates will now also be logged [ID_38986]

<!-- MR 10.5.0 - FR 10.4.6 -->

From now on, errors related to real-time GQI data updates will also be logged.

For example:

- When an ad hoc data source is not able to send an update due to API methods being used incorrectly.
- When a built-in data source is not able to send an update.
- When the connection used to send the updates to the client gets lost.

Exceptions associated with a custom data source will be logged in the log file of the data source in question.

#### Enhanced performance when processing changes made to service properties [ID_39011]

<!-- MR 10.3.0 [CU15]/10.4.0 [CU3] - FR 10.4.6 -->

Because of a number of enhancements, overall performance has increased when processing changes made to service properties.

#### NATS configuration files will now use plain JSON syntax [ID_39078]

<!-- MR 10.4.0 [CU3] - FR 10.4.6 -->

All NATS configuration files will now use plain JSON syntax.

#### Enhanced performance when logging on to cloud-connected DataMiner Agents or DaaS systems with an older version of a DataMiner Cube client [ID_39211]

<!-- MR 10.3.0 [CU15]/10.4.0 [CU3] - FR 10.4.6 -->

Performance has increased when logging on to cloud-connected DataMiner Agents or DaaS systems with an older version of a DataMiner Cube client.

#### SLAnalytics - Behavioral anomaly detection: A decreasing trend slope will now be labeled as a trend change instead of a variance decrease [ID_39249]

<!-- MR 10.5.0 - FR 10.4.6 -->

Up to now, in some cases, a decreasing trend slope would be labeled as a variance decrease. From now on, a decreasing trend slope will be labeled as a trend change instead.

#### SLAnalytics - Proactive cap detection: Enhanced clearing of proactive detection suggestion events [ID_39296]

<!-- MR 10.5.0 - FR 10.4.6 -->

A proactive detecting suggestion event indicating a forecasted crossing of a critical alarm threshold will now be cleared sooner. As soon as the system detects that the predicted trend has dropped below the threshold in question will the suggestion event be cleared.

#### GQI: Changing the minimum log level no longer requires an SLHelper restart [ID_39309]

<!-- MR 10.5.0 - FR 10.4.6 -->

Up to now, when you changed the *serilog:minimum-level* setting in `C:\Skyline DataMiner\Files\SLHelper.exe.config`, the change would only take effect after an SLHelper restart.

From now on, when you change this setting, the change will take effect the moment you save the configuration file. Restarting SLHelper will no longer be necessary.

#### Enhanced performance when starting up a DataMiner Agent [ID_39331]

<!-- MR 10.4.0 [CU3] - FR 10.4.6 -->

Because of a number of enhancements, overall performance has increased when starting up a DataMiner Agent.

#### SLDataGateway: Enhanced logging [ID_39341]

<!-- MR 10.5.0 - FR 10.4.6 -->

A number of enhancements have been made with regard to the logging of the SLDataGateway process.

The *SLDBConnection.txt* and *SLCloudStorage.txt* log files will now contain cleaner entries, and entries of type "Error" will also be added to the *SLError.txt* file.

Also, run-time log level updates will now be applied at runtime without requiring a DataMiner restart.

#### GQI now also logs requests to SLNet [ID_39355]

<!-- MR 10.5.0 - FR 10.4.6 -->

From now on, when the *serilog:minimum-level* setting in `C:\Skyline DataMiner\Files\SLHelper.exe.config` is set to "Debug" or lower, GQI will also log information about requests sent to SLNet.

Types of log entries related to SLNet requests:

- `Started SLNet request <RequestID> with <MessageCount> messages`

  This type of entry will be added to the log when GQI starts a request to SLNet, before the messages included in the request are sent.

  - *RequestID*: A unique ID that will allow you to find all log entries associated with one particular SLNet request.
  - *MessageCount*: The number of SLNet messages included in the request.

- `Sending SLNet message <RequestID>.<Index>: <Description>`

  This type of entry will be added to the log for each individual message in an SLNet request.

  - *RequestID.Index*: The unique ID of the message, consisting of the *RequestID* (which identifies the request) and an *Index* (i.e. the sequence number of the message).
  - *Description*: The string representation of the actual SLNet message, which should give a short but meaningful description of the message.

- `Finished SLNet request <RequestID> in <Duration>ms`

  This type of entry will be added to the log when GQI finishes a request to SLNet, regardless of whether the request was successful or not.

  - *RequestID*: The unique ID of request.
  - *Duration*: The duration of the request, including the time it took for GQI to process it (in milliseconds).

#### Enhanced error message 'Failed to create one or more storages' [ID_39360]

<!-- MR 10.5.0 - FR 10.4.6 -->

When DataMiner fails to start up due to a problem that occurred while connecting to the database, a `Failed to create one or more storages` message will be thrown.

From now on, this error message will include a reference to the StorageModule log file, in which you can find more information about the problem that occurred:

`More info might be available in C:\ProgramData\Skyline Communications\DataMiner StorageModule\Logs\DataMiner StorageModule.txt.`

#### No longer possible to create new elements as long as SLDataMiner has not finished loading all element information [ID_39392]

<!-- MR 10.4.0 [CU3] - FR 10.4.6 -->

From now on, it will no longer be possible to create new elements as long as SLDataMiner has not finished loading all element information. If an attempt is made to create an element while SLDataMiner is still loading element information, an `Agent is starting up` error will now be returned.

### Fixes

#### Automatic incident tracking: Incomplete or empty alarm groups after DataMiner startup [ID_38441]

<!-- MR 10.3.0 [CU15]/10.4.0 [CU3] - FR 10.4.6 -->

After a DataMiner startup, in some cases, certain alarm groups would either be incomplete or empty due to missing remote base alarms.

#### Protocols: Parsing problem could lead to string values being processed incorrectly [ID_39314]

<!-- MR 10.3.0 [CU15]/10.4.0 [CU3] - FR 10.4.6 -->

When string parameters are parsed, both an ASCII version and a Unicode version of the string value should be returned. However, up to now, when a string parameter was a table column parameter, the `Interprete` type of the table would be used. As a result, string values would be processed incorrectly.

From now on, when a table cell is saved, the `Interprete` type of the column will be used to determine whether or not it has to be processed as a string.

#### SLProtocol would return an error when it encountered the parameter type 'matrix' [ID_39398]

<!-- MR 10.4.0 [CU3] - FR 10.4.6 -->

Up to now, SLProtocol would add the following line in the log file of an element when it encountered the [parameter type "matrix"](xref:UIComponentsTableMatrix).

`CParameter::ReadSettings|CRU|-1|!! Unknown <Type> MATRIX for parameter`

#### Redundancy group and derived element no longer visible in UI after deleting a protocol used by elements in that redundancy group [ID_39411]

<!-- MR 10.4.0 [CU3] - FR 10.4.6 -->

When a protocol that was being used by elements in a redundancy group was deleted, the redundancy group and the derived element would no longer be visible in the UI after a DataMiner restart, even if their definitions existed on disk. As a result, it would not be possible to delete the redundancy group in a DataMiner client application (e.g. DataMiner Cube).

#### SLAutomation: Problem when clearing the internal parameter cache [ID_39441]

<!-- MR 10.3.0 [CU15]/10.4.0 [CU3] - FR 10.4.6 -->

In some cases, an error could occur in SLAutomation when its internal parameter cache was being cleared.

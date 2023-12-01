---
uid: General_Main_Release_10.3.0_CU11
---

# General Main Release 10.3.0 CU11 – Preview

> [!IMPORTANT]
> We are still working on this release. Some release notes may still be modified or moved to a later release. Check back soon for updates!

> [!TIP]
> For information on how to upgrade DataMiner, see [Upgrading a DataMiner Agent](xref:Upgrading_a_DataMiner_Agent).

### Enhancements

#### SNMPv3 responses now have a dynamic size [ID_37948]

<!-- MR 10.3.0 [CU11] - FR 10.4.2 -->

Up to now, the size of SNMPv3 responses was limited to 16000 bytes. When larger responses were received, a timeout message would appear in StreamViewer.

From now on, the size of SNMPv3 responses will no longer be limited, meaning that the only constriction will be the maximum size of a UDP packet (i.e. 65000 bytes).

> [!NOTE]
> When sending SNMPv3 messages, the size of those messages is still limited to 16000 bytes.

#### Enhanced performance when compiling QActions in SLScripting [ID_37993]

<!-- MR 10.3.0 [CU11] - FR 10.4.2 -->

When QActions are compiled in SLScripting, several resources need to be loaded. Up to now, those resources would be loaded for every QAction individually. From now on, they will be loaded only once and stored in a cache in order to reduce memory and CPU overhead.

Every 10 seconds, resources that have not been referenced in the last 30 seconds will be removed from the cache.

### Fixes

#### SLDataGateway: Problem with casing when retrieving data from Elasticsearch/OpenSearch [ID_37835]

<!-- MR 10.3.0 [CU11] - FR 10.4.2 -->

When SLDataGateway retrieved data from Elasticsearch/OpenSearch on behalf of a DataMiner app (e.g. Ticketing), in some cases, it would pass an incorrect result set to that app due to a casing issue.

#### Service & Resource Management: Timeout script in end event of booking would not get executed when DMA was stopped within the time range of the booking [ID_37911]

<!-- MR 10.3.0 [CU11] - FR 10.4.2 -->

When the end event of a booking used a timeout script, in some cases, that script would not get executed when the DataMiner Agent was stopped within the time range of the booking.

#### DataMiner Taskbar Utility: Problem when making SLTaskbarUtility perform an action using the command prompt [ID_37952]

<!-- MR 10.3.0 [CU11] - FR 10.4.2 -->

When you made the DataMiner Taskbar Utility perform some action using the command prompt, the arguments would not be parsed correctly when no instance of SLTaskbarUtility was running.

#### GQI: 'Could not find PK column' error after performing a query against an empty parameter table [ID_37978]

<!-- MR 10.3.0 [CU11] - FR 10.4.1 -->

Up to now, in some rare cases, performing a GQI query against an empty parameter table would result in a `Could not find PK column` error. From now on, GQI will return an empty result set instead.

#### SLDataGateway would incorrectly keep waiting for acknowledgements from SLDataGatewayAPI [ID_37985]

<!-- MR 10.3.0 [CU11] - FR 10.4.2 -->

SLDataGateway would incorrectly keep waiting for an acknowledgement from SLDataGatewayAPI, causing numerous `Waiting for SLDataGatewayAPI to acknowledge ...` entries to be added to the *SLDataGateway.txt* log file.

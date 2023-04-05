---
uid: Databases_about
---

# About databases

DataMiner supports multiple different [system data storage architectures](xref:Supported_system_data_storage_architectures).

- Often an **on-premises** [Cassandra database](xref:Cassandra_database) and [Elasticsearch](xref:Elasticsearch_database) or [OpenSearch](xref:OpenSearch_database) database are used.
- Instead of on-premises databases, you can use **managed services from a cloud provider**, e.g. the [Amazon Keyspaces Service](xref:Amazon_Keyspaces_Service) and [Amazon OpenSearch Service](xref:Amazon_OpenSearch_Service).
- As a third alternative, soon it will be possible to use **Storage As A Service** on dataminer.services, so you no longer have to maintain the databases yourself, and all the scaling and complexity is taken care of for you.

In addition to the system databases, you can also configure an [offload database](xref:Offload_database), for example to produce reports without interfering with the live DataMiner System. [Additional databases](xref:Configuring_an_additional_database) can also be configured, for example for DataMiner Inventory & Asset Management.

> [!TIP]
> See also: [Securing the DataMiner databases](xref:Database_security)

> [!NOTE]
> When the main database is offline, file offloads are used to store write/delete operations. You can configure a limit for the file size of these offloads in the file [DBConfiguration.xml](xref:DBConfiguration_xml).

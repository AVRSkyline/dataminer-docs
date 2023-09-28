---
uid: Configuring_multiple_OpenSearch_clusters
---

# Configuring multiple OpenSearch clusters

From DataMiner 10.3.0/10.3.3 onwards, you can have data offloaded to multiple OpenSearch clusters, i.e. one main cluster and several replicated clusters. Data is always read from the main cluster, but data updates are sent to all clusters.

To configure this setup, proceed as follows:

## [From DataMiner 10.3.12/10.4.0 onwards]

> [!IMPORTANT]
> From DataMiner 10.3.12/10.4.0 onwards, the configuration for multiple OpenSearch clusters is saved in [DB.xml](xref:DB_xml)

1. For each OpenSearch cluster a *DataBase* tag must be added with the following configuration:

    - *active* attribute: Set this to "true" if you wish your elastic cluster to be added to the list of clusters to offload data to.
    
    - *search* attribute: Always set this to "true". 

    - *ID* attribute: This should be a unique number, preferably starting at 0 and increasing by 1 for each additional cluster.
    
    - *priorityOrder* attribute: Indicates the priority of the different clusters. The lower the value, the greater the priority. The cluster with the lowest value is the main cluster, from which data will be read.
    
    - *type* attribute: Always set this to "ElasticSearch". Referral to ElasticSearch here is for legacy and compatibility reasons.
    
    - *DBServer*: The hosts of the cluster, separated by commas (see [Indexing database settings](xref:DB_xml#indexing-database-settings))
    
    - *UID*: The username to connect to OpenSearch.
    
    - *PWD*: The password to connect to OpenSearch.
    
    - *DB*: The prefix for the OpenSearch indexes. 
    
    - *FileOffloadIdentifier*: String used to identify this connection. Each connection should have a different identifier, which will be used for file offloads.
     
     Example:

   ```xml
   <DataBases>
        <!-- Reads will be handled by the ElasticCluster with the lowest priorityOrder -->
        <DataBase active="true" search="true" ID="0" priorityOrder="0" type="ElasticSearch">
            <DBServer>localhost</DBServer>
            <UID />
            <PWD>root</PWD>
            <DB>dms</DB>
            <!--
            Used by file offload (i.e. when the connection with the Elastic cluster is not
            available) for tagging the offloaded data with.
           Should be different for each defined Elastic cluster connection.
            -->
            <FileOffloadIdentifier>cluster1</FileOffloadIdentifier>
        </DataBase>
        <DataBase active="true" search="true" ID="0" priorityOrder="1" type="ElasticSearch">
            <DBServer>10.11.1.44,10.11.2.44,10.11.3.44</DBServer>
            <UID />
            <PWD>root</PWD>
            <DB>dms</DB>
            <FileOffloadIdentifier>cluster2</FileOffloadIdentifier>
        </DataBase>
   </DataBases>
   ```

1. Remove or disable any previous Elasticsearch configuration from the DB.xml.

1. Restart DataMiner.

> [!NOTE]
> If an exception occurs for one of the replicated clusters, an alarm will be generated in the Alarm Console, indicating that not all data might be replicated. If further errors occur, no new alarms are created until the DMA is restarted.

## [Prior to DataMiner 10.3.12/10.4.0]

> [!NOTE]
> For reasons of legacy and compatibility with Elasticsearch, the *DBConfiguration.xml* file will have XML tags referring to Elasticsearch instead of OpenSearch such as the \<ElasticConnections\> or \<ElasticCluster\> tags. Tags such as \<OpenSearchCluster\> will not work.

1. Create and configure a *DBConfiguration.xml* file as illustrated below. For each OpenSearch cluster, an *ElasticCluster* tag must be added with the following configuration:

   - **priorityOrder** attribute: Indicates the priority of the different clusters. The lower the value, the greater the priority. The cluster with the lowest value is the main cluster, from which data will be read.

   - **Hosts**: The hosts of the cluster, separated by commas. This is the equivalent of the *DBServer* tag in the *DB.xml* file (see [Indexing database settings](xref:DB_xml#indexing-database-settings)).

   - **Username**: The username that will be used to connect to OpenSearch. This is the equivalent of the *UID* tag in the *DB.xml* file.

   - **Password**: The password that will be used to connect to OpenSearch. This is the equivalent of the *PWD* tag in the *DB.xml* file.

   - **Prefix**: The prefix for the OpenSearch indexes. This is the equivalent of the *DB* tag in the *DB.xml* file.

   - **FileOffloadIdentifier**: The string used to identify this connection. Each connection should have a different identifier, which will be used for file offloads.

   Example:

   ```xml
   <DatabaseConfiguration>
      <SearchConfiguration>
         <ElasticConnections>
            <!-- Reads will be handled by the ElasticCluster with the lowest priorityOrder -->
            <ElasticCluster priorityOrder="0">
               <Hosts>localhost</Hosts>
               <Username />
               <Password>root</Password>
               <!--
                  Prefix corresponds with the DB tag in DB.xml.
                  The content of the Prefix tag gets prefixed to the names
                 of the aliases and indices created by DataMiner.
               -->
               <Prefix>dms</Prefix>
               <!--
                  Used by file offload (i.e. when the connection with the Elastic cluster is not
                  available) for tagging the offloaded data with.
                  Should be different for each defined Elastic cluster connection.
               -->
               <FileOffloadIdentifier>cluster1</FileOffloadIdentifier>
            </ElasticCluster>
            <ElasticCluster priorityOrder="1">
               <Hosts>10.11.1.44,10.11.2.44,10.11.3.44</Hosts>
               <Username />
               <Password>root</Password>
               <Prefix>replica</Prefix>
               <FileOffloadIdentifier>cluster2</FileOffloadIdentifier>
            </ElasticCluster>
         </ElasticConnections>
      </SearchConfiguration>
   </DatabaseConfiguration>
   ```

1. Add this file in the `C:\\Skyline DataMiner\\Database` folder on each DataMiner Agent in your DMS. Currently, this file is not synchronized automatically.

1. After the file has been added, restart DataMiner. The *DBConfiguration.xml* file will now take precedence over the Elasticsearch configuration defined in the *DB.xml* file.

> [!NOTE]
> If an exception occurs for one of the replicated clusters, an alarm will be generated in the Alarm Console, indicating that not all data might be replicated. If further errors occur, no new alarms will be created until the DMA is restarted.

> [!TIP]
> For troubleshooting information, see [Investigating OpenSearch issues](xref:Investigating_OpenSearch_Issues)

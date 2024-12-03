---
uid: Inter-process_communication
---

# Inter-process communication

The number of interactions between SLScripting, the process executing the QAction, and other processes should be considered wisely, as these consume a considerable amount of resources. Also limit the number of interactions per second.

It can occur that a QAction needs to perform an operation that requires some time to complete (e.g. a DMS call). In case another call is needed to determine if the operation has finished, you must avoid continuously repeating the call that checks the operation status without leaving time between the calls (for example, by including a Thread.Sleep call in the loop).

Typically, QActions mainly interact with the SLProtocol process using an instance of the SLProtocol (or SLProtocolExt) class. As each protocol object call results in inter-process communication between the SLScripting and SLProtocol processes, consider the following:

- Use bulk method calls (e.g. GetParameters, SetParameters, GetColumns, FillArray, etc) instead of many specific method calls (e.g. GetParameter, SetParameter, GetRow, GetParameterIndexByKey, etc) to get and set multiple parameters, respectively. This is not so much about reducing the number of calls to the absolute minimum but more about finding the right balance between readability/maintainability on one side and performance on the other side and about keeping things scalable. Examples:
    - Splitting the retrieval of several standalone parameters into 2 or 3 method calls for readability/maintainability reasons is very fine. Indeed, the number of method calls is still kept under control and will not grow as the data-source scales up.
    - Splitting the retrieval of a whole table into many GetParameterIndexByKey method calls via a loop is not acceptable. Indeed, as the data-source scales up, the number of method calls will also grow and go out of control which is not scalable.

- The implementation with the best performance should be used when retrieving or updating tables. A QAction implementation that retrieves or sets column(s) is generally preferred over a QAction that triggers on every row of a table (row=true).

- Protocol calls inside a loop should be avoided as much as possible.

- Grouping protocol calls into a single bulk one should be prefered but only to some extend. More information on this can be found [here](xref:Data_handling#guidelines)

In order to improve readability (and type safety) of code in QActions, the following guidelines should be considered:

- In case a wrapper method is available for a NotifyProtocol call, the use of the wrapper method is favored.

- With DataMiner versions prior to DataMiner 9.0, the use of the GetKeys method to retrieve the primary keys (NotifyProtocol.KeyType.Index) should be avoided, as up to DataMiner 9.0 the implementation to retrieve the primary keys is based on the SLElement process (an NT_GET_INDEXES call is executed, which retrieves both the primary keys and the display keys.). As it is possible that there is a delay in SLElement (e.g. due to a large number of calls that it is processing), it is possible that the returned data is not up to date.

    Since DataMiner 9.0, the implementation of the GetKeys method has been updated. Retrieving the primary keys no longer involves the SLElement process. However, note that obtaining the display keys (NotifyProtocol.KeyType.DisplayKey) is still based on SLElement.

> [!NOTE]
>
> - The implementation of the Keys property of the QActionTable class also makes use of the GetKeys method. Therefore, the use of the Keys property should also be avoided prior to DataMiner 9.0.
> - The ClearAllKeys() method still uses the NT_GET_INDEXES call, so for this reason the use of this method should be avoided.

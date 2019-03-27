Picking up from where we left off, lets explore few more tables that one may end up looking for.

'ImanType' - All the different types of objects that are present in Teamcenter have a type defined in the database. This type information would be saved in this `pImanType` table. For instance, the 'CMHasSolutionItem' is a relationship between an Engineering Change Revision object and a Solution Item revision. This means there would be a row in this ImanType database table where the type name would be declared as 'CMHasSolutionItem'. This would be created as part of the typical BMIDE deployment. We would look at this usecase in more detail downstream, trust me!.

`DispatcherRequest` represents a request from Teamcenter to the Dispatcher framework. This request manages the state and 
execution of a request lifecycle. The corresponding database table is `pDispatcherRequest`. In essence, a count query on this table where the request state is INITIAL gives the number of requests that are yet to be picked up by a given dispatcher client.

`ImanVolume` and `ImanFile` represent the Teamcenter volumes and the Teamcenter's Dataset's named references - the physical file information. `ImanFile` tells which volume a file resides in. `ImanVolume` tells which storage location a volume resides in.

Export Records - `pImanExportRecord` and `pItemExportRecord` are used for tracking multisite data transfers. When an Item is transferred to a different site an Item Export Record gets created for it and for any other type of object, an Iman Export Record is created. It is these export records that tell in the source site that it is indeed replicated to other sites.

BOM Information - 'pPSBomViewRevision' and 'pPSBomView' store information related to the BOM View Revisions and BOM Views.

As promised, in the next page, we would see how the different tables come into action for a simple scenario.


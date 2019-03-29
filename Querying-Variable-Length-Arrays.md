Variable Length Arrays, or in short, VLAs are nothing but the array properties on Teamcenter business objects.

***

Examples of this sort of properties are:

### `process_stage_list` on Item Revisions
  This property contains the referencing workflow processes. In other words, all the workflows that were ever executed on an item revision are trackable via this property ( unless they are cleared via the clear_process_stage_list.exe ).
### `release_status_list` on Item Revisions
  This property contains the list of all the release statuses that are present on an item revision.
### `bvr_occurrences` on PSBomViewRevisions
  This property tracks the occurrences under the given Bom View Revision.

As you can see, all these are arrays, a collection.

***

VLAs are stored in a different table altogether. For instance, there is a separate database table called `pRelease_Status_List`, which holds all the release status information of all the Item Revisions in the database. This information is directly not present on the Item Revision table i.e., pItemRevision itself. This means that the piece of information that joins both of them is the Item Revision puid.

To be more precise, all the entries in the pRelease_Status_List where its puid column is equal to a particular pItemRevision.puid value, are all the different release statuses that given Item Revision has. 

Please do note that there are implementations of PLM where an ItemRevision holds multiple release statuses and there are other implementations where an item revision can have only one.

I have written a sample SQL to query such release status information on Item Revisions and it is presented in the Code section with the name 'List_All_Release_Statuses_On_Item_Revisions.sql'. Please do check it out!.
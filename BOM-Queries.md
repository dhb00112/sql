Lets take couple of examples putting what we learnt in the 'BOM World' page to test.

`PSBOMView`, `PSBOMViewRevision`, `PSOccurrence `are the classes that we need for these BOM traversals / listing in SQL.

* Querying a given BVR to get its constituent Items. Note that since we are assuming the BVR to be precise, the join at
the end specifies the Item table. Also note that a given BVR may not have any children for all we know - the left outer join is for that very reason.

`select distinct wso.pobject_name as RootBVR, child.pitem_id as Occurrence Child Item`
`from ppsoccurrence occ`
`join ppsbomviewrevision bvr on bvr.puid = occ.rparent_bvru`
`join pworkspaceobject wso on wso.puid = bvr.puid`
`left join pitem child on child.puid = occ.rchild_itemu`
`where wso.pobject_name like '<item-id>/AA-View'`

Sometimes, when importing and exporting structures from a Production instance or if you have a multisite setup, the sync would end up with replica BOMLines. These can be identified with the below tweak to the query above.

`select distinct wso.pobject_name as RootBVR, child.puid as OccurrencePUID`
`from ppsoccurrence occ`
`join ppsbomviewrevision bvr on bvr.puid = occ.rparent_bvru`
`join pworkspaceobject wso on wso.puid = bvr.puid`
`left join pitem child on child.puid = occ.rchild_itemu`
`where wso.pobject_name like '%-View'`
`and child.pitem_id is null;`

Same as the earlier one, the additional part is the where clause update to include 'child.pItem_Id is null' to ensure that we get the BVRs, whose children are stubs. If an Item is a stub ( stub is a placeholder for an object that is not in the current database in its entirety ), then it would be present in the pPOM_Stub table and not in its regular storage location. Note that the occurrences sycn from one site to another when the partent Item ( and so its BVRs ) are successfully sent. But the Items/ItemRevisions the occurrences refer to, do not sync, unless manually forcefully synched. This query would tell you the BVRs that have occurrences which have un-synched Item / ItemRevision data.


Typically some Teamcenter development groups add new properties on `Form` class and then compound them onto the `Item Revision` for display.`Form` in Teamcenter has a special class where the data attributes get stored. This is called as Form Storage Class.

The Form instance has an attribute called `data_file`, which would refer to this form storage class where the attributes get stored. This storage class, is typically a `POM_Object`'s subclass.

To retrieve the properties in cases like this, a query of the below format should help.

```
select item.pItem_id as ItemId, itemRev.PITEM_REVISION_ID as RevisionId, Formstorageclass.<formproperty>
from infodba.pItemRevision itemRev
inner join infodba.pImanRelation relation on itemRev.puid = relation.RPRIMARY_OBJECTU
inner join infodba.pForm formObj on formObj.puid = relation.RSECONDARY_OBJECTU
inner join infodba.<formstorageclass> formStorageClass on formStorageClass.puid = infodba.formObj.RDATA_FILEU
inner join infodba.pItem item on itemRev.RITEMS_TAGU = item.puid
and item.pItem_id = '<an-item-id>';
```

* Replace the `<formproperty>` with the property on the form that you would like to retrieve.
* Replace the `<an-item-id>` with the item id which you would like to query on.
BOM is the `Bill of Materials`. BOM represents the different components that are needed in the design/manufacturing of an assembly. If you have a product, say, a Car, it can always be visualized as an assembled structure of different components - say axle, wheels, engine etc. All these combined form the BOM of the Car.

In this section, we will take up a sample Teamcenter BOM and analyze how the BOM is persisted in the database.

Let us assume that our BOM looks as shown below:

![Teamcenter BOM](https://i.imgur.com/2VEW3xs.png)

This is a literally saying that Car is comprised of Axle and Engine. Now in BOM terminology, each line is called a `BOMLine`. So Axle and Engine are two BOMLines in the BOM of the Car.

In Teamcenter, Product structures such as these are modelled using both a runtime Business Object ( BOMLine ) as well as a persistent Business object ( PSOccurrence ). More on this later.

The fact that the Item called Axle and Engine occurs in the BOM View of Car in itself is referred to as an `Occurrence`. The equivalent database table for an Occurrence is `PSOccurrence`. But there is no database table for a `BOMLine`, because it is a run-time business object. That means no property on the BOMLine is stored in the database in the table pBOMLine ( because, there is no such table ). Instead, every property that gets seen in Structure Manager or MPP on a BOMLine is either dynamically constructured ( ex: Rule Configured By ) or persistent data stored in other Teamcenter classes like Occurrence and Item/Item Revision.

Let us take a moment to understand how the datamodel of a BOM gets persisted:

`PSBomView` and `PSBomViewRevision` - If you observe the image above, we are looking at the BOM of the top item revision ( that got configured by a revision rule ). This way/view of an Item revision where the BOM could be seen is referred to as the Product Structure BOM View. This is managed by the databases classes pPSBOMView and pPSBOMViewRevision. Each of the children Items ( EngineV800 and Axle ) under this parent Item ( Car ), have something called as Occurrences and they get stored registering to the pPSBOMViewRevision. The below diagram would help in understanding more on the same.

![BOM Persistence](https://i.imgur.com/D7s4roX.png)

As a fun fact, `BOMWorld` typically refers to the array of different BOM Windows that are opened in Teamcenter BOM applications but not yet closed :).








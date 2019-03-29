BOM is the `Bill of Materials`. BOM represents the different components that are needed in the design/manufacturing of an assembly. If you have a product, say, a Car, it can always be visualized as an assembled structure of different components - say axle, wheels, engine etc. All these combined form the BOM of the Car.

In this section, we will take up a sample Teamcenter BOM and analyze how the BOM is persisted in the database.

Let us assume that our BOM looks as shown below:

![Teamcenter BOM](https://i.imgur.com/2VEW3xs.png)

This is a literally saying that Car is comprised of Axle and Engine. Now in BOM terminology, each line is called a `BOMLine`. So Axle and Engine are two BOMLines in the BOM of the Car.

In Teamcenter, Product structures such as these are modelled using both a runtime Business Object ( BOMLine ) as well as a persistent Business object ( PSOccurrence ). More on this later.

The fact that the Item called Axle and Engine occurs in the BOM View of Car in itself is referred to as an `Occurrence`. The equivalent database table for an Occurrence is PSOccurrence. But there is no database table for a BOMLine, because it is a runtime business object.

So this is how the persistent datamodel of a BOM gets stored:

`PSBomView` and `PSBomViewRevision` - If you observe the image above, we are looking at the BOM of the top item revision ( that got configured by a revision rule ). This way/view of an Item revision where the BOM could be seen is referred to as the Product Structure BOM View. Each of the components that construct the BOM 











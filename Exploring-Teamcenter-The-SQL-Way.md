Hello There!.

   I would like to use this repository to talk about the Teamcenter datamodel in general. 
We would see how the basic connections between objects work in Teamcenter and device SQLs to navigate 

**Caution:** Teamcenter database exploring is quite rewarding. The time it takes to execute complex queries and return results is the fastest in this mode. All other ways of doing so, say, an ITK executable to pull up needed information or a Teamcenter Query Builder query would not be straightforward. And so this mode has to be used with utmost diligence. I advice you to use a READ-ONLY privileged account and not the infodba account to prevent accidental mis-use or updates to the database.

   `POM_Object` At the top of the Teamcenter class ( database table ) hierarchy lies this table. This is the core class of Teamcenter around with other database tables take life. And as such it holds some crucial and minimal information within itself that every single Teamcenter object should have. These are the `Owning site` and `timestamp` properties. Also a `puid` column is also available for the table. This puid is the unique identifier for a given Teamcenter object. There are complex C++ classes and C structures ( called Data Managers ) that are involved in generating a puid based on the object type and the time it gets created for a given site. Note that the corresponding database table name is pPOM_Object. The usual notation is to have a prefix character 'p' beside the BMIDE class name for the corresponding table.

desc infodba.pPOM_Object
Name               Null     Type         
------------------ -------- ------------ 
PLSD                        DATE         
ROWNING_SITEC               NUMBER       
ROWNING_SITEU               VARCHAR2(15) 
POBJECT_PROPERTIES NOT NULL NUMBER       
PPID               NOT NULL NUMBER       
PTIMESTAMP         NOT NULL VARCHAR2(33) 
PUID               NOT NULL VARCHAR2(15) 
AOID               NOT NULL VARCHAR2(15) 
AREV_CATEGORY      NOT NULL NUMBER       
ASPACE_UID                  VARCHAR2(15) 
AVALID_FROM        NOT NULL DATE         
AVALID_TO                   DATE         

   `POM_Application_Object` We have seen that POM_Object stores the site information of an object in Teamcenter. If we take an object like an Item or a dataset, our natural question would be to understand how the metadata like Owning user or creation timestamp gets saved. Well, this is where POM_Application_Object comes into picture. This table contains information like the Owning user, creation date, Last Modification User and Last Modified Date. The corresponding database table is pPOM_Application_Object.





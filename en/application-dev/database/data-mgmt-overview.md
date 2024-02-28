# Data Management Overview


## Function

Data management provides the following functionalities:

- Data storage: provides capabilities for persisting user preference data, key-value (KV) store data, and relational database (RDB) store data.

- Data management: provides efficient data management capabilities, including permission management, data backup and restore, and dataShare framework.

- Data synchronization: provides data synchronization across devices. For example, distributed data objects support sharing of memory objects across devices, and distributed databases support database access across devices.

The database stores created by an application are saved to the application sandbox directory. When the application is uninstalled, the database stores are automatically deleted.


## Working Principles

The data management module includes preferences, KV data management (KV-Store), relational data management (RelatoinalStore), distributed data object (DataObject), cross-application data management (DataShare), and unified data management framework (UDMF). The interface layer provides standard JavaScript APIs for application development. The Frameworks & System Service layer implements storage and synchronization of component data, and provides dependencies for SQLite and other subsystems.

**Figure 1** Data management architecture

![dataManagement](figures/dataManagement.jpg)


- **Preferences**: implements persistence of lightweight configuration data and supports subscription of data change notifications. Preferences are used to store application configuration information and user preference settings and do not support distributed synchronization.

- **KV-Store**: implements read, write, encryption, and manual backup of data in KV stores and notification subscription. When an application needs to use the distributed capabilities of a KV store, KV-Store sends a synchronization request to DatamgrService, which implements data synchronization across devices.

- **RelationalStore**: implements addition, deletion, modification, query, encryption, manually backup of data in RDB stores, and notification subscription. When an application needs to use the distributed capabilities of an RDB store, RelationalStore sends a synchronization request to DatamgrService, which implements data synchronization across devices.

- **DataObject**: independently provides distributed capabilities for the data object structs. **DatamgrService** implements temporary storage of the object data, which is still required after the application (either the application of your device or cross-device application) is restarted.

- **DataShare**: provides the data provider-consumer mode to implement addition, deletion, modification, and query of cross-application data on a device, and notification subscription. **DataShare** is not bound to any database and can interact with RDB and KV stores. You can also encapsulate your own databases for C/C++ applications.<br>In addition to the provider-consumer mode, **DataShare** provides silent access, which allows direct access to the provider's data via the DatamgrService proxy without starting the data provider. Currently, only the RDB stores support silent access.

- **UDMF**: defines the language and data standards for cross-application and cross-device data interaction, improving data interaction efficiency. The UDMF provides secure and standard data transmission channels and supports different levels of data access permissions and lifecycle management policies. It helps implement efficient data sharing across applications and devices.

- **DatamgrService**: implements synchronization and cross-application sharing for other components, including cross-device synchronization of **RelationalStore** and **KV-Store**, silent access to provider data of **DataShare**, and temporary storage of **DataObject** data.

### MetaServer Models
#### 1. VERSION (metadata version corresponding to MetaServer)
| NAME           | TYPE             | COMMENT              |
|----------------|------------------|----------------------|
| verId          | int32            | version of MetaServer|

#### 2. DBS (database information)
| NAME           | TYPE             | COMMENT              |
|----------------|------------------|----------------------|
| dbId           | int64            | unique database id   |
| dbName         | string           | unique database name |
| locationUrl    | string           | path in filesystem   |
| userId         | int64            | owner        id      |

#### 3. DB_PARAMS (user specified parameters related to database) [optional]
| NAME           | TYPE             | COMMENT               |
|----------------|------------------|-----------------------|
| dbId           | int64            | referenced database id|
| paramKey       | string           | key as string         |
| paramValue     | string           | value as string       |

#### 4. DB_PRIVS(database privileges)
| NAME            | TYPE             | COMMENT               |
|-----------------|------------------|-----------------------|
| dbPrivId        | int64            | unique sequential id  |
| grantTime       | int64            | grant time            |
| userId          | int64            | user id               |
| privType        | int32            |                       |
| dbId            | int64            | database id           |

Available privilege types:    
1: read, 2: write, 3: read + write, 5: read + grant read to other,
6: write + grant write to other, 7: read + write + grant read/write to other.
(4: grant current privilege to other users)

#### 5. TBLS (table information)
| NAME           | TYPE             | COMMENT                                 |
|----------------|------------------|-----------------------------------------|
| tblId          | int64            | unique table id                         |
| dbId           | int64            | database belonging to                   |
| createTime     | int64            | timestamp stored as long                |
| lastAccessTime | int64            | timestamp stored as long                |
| userId         | int64            | user_id is owner's                      |
| tblName        | string           | table name                              |
| tblType        | int32            | 0 represents regular, 1 represents fiber|
| fiberColId     | int64            | -1 means no fiber column                |
| locationUrl    | string           | path in filesystem                      |
| storageFormat  | int32            |                                         |
| fiberFuncId    | int64            | table partition function                |

#### 6. TBL_PARAMS (user specified parameters related to table) [optional]
| NAME           | TYPE             | COMMENT              |
|----------------|------------------|----------------------|
| tblId          | int64            | unique table id      |
| paramKey       | string           | key as string        |
| paramValue     | string           | value as string      |

#### 7. TBL_PRIVS(table privileges)
| NAME           | TYPE             | COMMENT               |
|----------------|------------------|-----------------------|
| tblPrivId      | int64            |                       |
| grantTime      | int64            | grant time            |
| privType       | int32            |                       |
| tblId          | int64            |                       |

#### 8. SFS (storage format information)
| NAME           | TYPE             | COMMENT                      |
|----------------|------------------|------------------------------|
| storageFormatId| int32            |                              |
| compression    | string           | uncompressed \| snappy \| etc|
| serialFormat   | string           | serial class name            |

#### 9. COLS (column information)
| NAME           | TYPE             | COMMENT                                   |
|----------------|------------------|-------------------------------------------|
| colId          | int64            |                                           |
| tblId          | int64            | table id                                  |
| colName        | string           | column name                               |
| colType        | string           | column type: regular \| fiber \| timestamp|
| dataType       | string           | data type: integer \| char(x) \| float    |
| colIndex       | int32            | index of column in table                  |

#### 10. FIBER_FUNCS
| NAME               | TYPE             | COMMENT              |
|----------------    |------------------|----------------------|
| fiberFuncId        | int64            | function id          |
| fiberFuncName      | string           | function name        |
| fiberFuncContent   | bytes            | function template id |

#### 11. BLOCK_INDEX
| NAME            | TYPE             | COMMENT              |
|-----------------|------------------|----------------------|
| blockIndexId    | int64            | block id             |
| tblId           | int64            | table id             |
| fiberValue      | int64            | fiber value          |
| timeBegin       | int64            | block begin timestamp|
| timeEnd         | int64            | block end timestamp  |
| timeZone        | string           | time zone            |
| blockPath       | string           | block file path      |

#### 12. USERS
| NAME           | TYPE             | COMMENT               |
|----------------|------------------|-----------------------|
| userId         | int64            | all recorded users    |
| createTime     | int64            | creation time         |
| userName       | string           | user name             |
| lastVisitTime  | int64            | last visit time       |
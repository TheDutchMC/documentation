# Database indexes

Proper database indexes can drastically improve a performance of list view loading, reports, search operations etc.

## Defining indexes

Indexes are defined in metadata > entityDefs. 

### Example

`custom/Espo/Custom/Resources/metadata/Lead.json`:


```json
{

    "indexes": {
        "myIndexNameOne": {
            "columns": ["columnName"]   
        },
        "myIndexNameTwo": {
            "columns": ["columnNameOne", "columnNameTwo"]  
        },
        "myUniqueIndexName": {
            "type": "unique",
            "columns": ["id", "columnNameOne", "columnNameTwo"]  
        }
    }
}
```

You need to run rebuild: Administratin > Rebuild.

## Forcing index usage in ORM

You need to specify an index name in *useIndex* param.

```php
$repository->where($whereClause)->find([
    'useIndex' => 'myIndexNameOne',
]);

```

Multiple indexes:

```php
$repository->where($whereClause)->find([
    'useIndex' => ['myIndexNameOne', 'myIndexNameTwo'],
]);
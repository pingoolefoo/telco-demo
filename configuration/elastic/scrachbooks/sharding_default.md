# Configuration du sharding par défaut

```
PUT _template/default-sharding
{
    "index_patterns": ["*"] ,
    "order": 0,
    "settings": {
        "number_of_shards": 1,
        "number_of_replicas": 0
    }
}
```

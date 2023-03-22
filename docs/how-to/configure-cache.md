Open-age provides a unified way to verious cache storage provider like redis and memcache.

in order to enable caching 

step 1. 
Specify which caching provider to be used, by default it is redis and can be changed to memcache
cache provider can be specified at tenant or config file level

Ex: At tenant level 
https://github.com/openage/openage.github.io.gitfor memcache replace "redis" by "memcache"

step 2.  
Specify an object with key "cache" for the api for which cache supposed to be configure  
object structure is like - 

- to cache response of an GET api
```
"cache" : {
	key: <key with which value will be saved><type: string>
	ttl: <time in seconds after which key and it's value will get deleted>
	action: "add"
	condition: <object to specify condition to cache response of the api>
}
```

example: 
```
cache: {
	"key": 'category_list_${query}', 
	"ttl": 2000, 
	action: "add", 
	condition: {
		"operator": "AND",
		"value": [{
			"key": "query.k",
			"operator": "==",
			"value": '9'
		}]
	}
}
```

Note - 
	In case no condition is specified 
	- if response of the GET api is not a list , response will get cached
	- if response of the GET api is a list , response won't get cached

- To invalidate cache
```
"cache" : {
	key: [<array of keys that supposed to get deleted>]
	action: "remove"
}
```

example: 
```
cache: { 
	"key": ["category_list*", "category_item_${params.id}"],
	action: "remove" 
}
```

Note - 
	- Regex pattern can be specified as an element in key array of above object


### Cache server configuration

Object Structure -
```
 "cache" : {
	 "provider": <name of cache provider redis/memcache>
	 "host": <IP of cache server>
	 "port": <Port for connection>,
	 "password": <Password if any>,
	 "maxmemory": <maximum memory that can be consumend in GB>
	 "maxmemory-policy" : <Cache eviction policy> {'allkeys-lru' by default}
 }
```

Example: 

```
"cache": {
	"provider": "redis",
	"host": "127.0.0.1",
	"port": 6379,
	"maxmemory": "1gb",
	"password": "foobared",
	"maxmemory-policy": "allkeys-lru"
}
```

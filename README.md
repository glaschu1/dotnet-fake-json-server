.NET Fake JSON Server
--------------------------

[![Build status](https://ci.appveyor.com/api/projects/status/hacg7qupp5oxbct8?svg=true)](https://ci.appveyor.com/project/ttu/dotnet-fake-json-server)

Fake REST API for developers for prototyping
 
* .NET Core Web API
* Uses [JSON Flat File DataStore](https://github.com/ttu/json-flatfile-datastore)

## Routes

```
GET    /
GET    /status
GET    /api
GET    /api/{item}
POST   /api/{item}
GET    /api/{item}/{id}
PUT    /api/{item}/{id}
DELETE /api/{item}/{id}
```

For now supports only id as key field and integer as it's value type.

Dyanamic routes are defined by the name of item's collection and id: `api/{item}/{id}`. All eamples below use user as collection name.

##### Example JSON Data

```json
{
  "user": [
    { "id": 1, "name": "Phil", "age": 40, "city": "NY" },
    { "id": 2, "name": "Larry", "age": 37, "city": "London" },
    { "id": 3, "name": "Thomas", "age": 40, "city": "London" }
  ],
  "movie": []
}
```

##### Root

`GET /`

Returns static files from wwwroot. Default file is `index.html`.

##### Status

Status endpoint, which returns current status of the service.

```sh
$ curl http://localhost:57602/status
```
```json
{"status": "Ok"}
```

#####  List collections 

`GET /api`

```sh
$ curl http://localhost:57602/api
```

```json
[ "user", "movie" ]
```

##### Get items

`GET /api/{item}`

Returns list of items. Amount of items can be defined with `skip` and `take` parameters. By default request returns first 10 items. 
```sh
$ curl http://localhost:57602/api/user
```

Example request returns items from 6 to 26

```sh
$ curl http://localhost:57602/api/user?skip=5&take=20
```


##### Get items with query 

`GET api/user?field=value&otherField=value`

```sh
$ curl http://localhost:57602/api/user?age=40
```
```json
[ 
 { "id": 1, "name": "Phil", "age": 40, "city": "NY" },
 { "id": 3, "name": "Thomas", "age": 40, "city": "London" }
]
```

##### Get item with id 

`GET /api/{item}/{id}`

```sh
$ curl http://localhost:57602/api/user/1
```

```json
{ "id": 1, "name": "Phil", "age": 40, "city": "NY" }
```

#### CORS

CORS is enabled and it allows everything.

### License

Licensed under the [MIT](LICENSE) License.
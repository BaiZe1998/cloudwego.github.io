---
title: 'hz annotation'
date: 2023-02-21
weight: 6
description: >
---
### Supported api annotations

> Field annotation can be used for[parameter binding and validation](https://www.cloudwego.io/docs/hertz/tutorials/basic-feature/binding-and-validate/)
>
> Method annotation can be used to generate code that related to route registration

#### Supported api annotations

| _Field annotation_                       |                                                                    |
| ---------------------------------------- | ------------------------------------------------------------------ |
| annotation                               | description                                                        |
| api.raw_body                             | generate "raw_body" tag                                            |
| api.query                                | generate "query" tag                                               |
| api.header                               | generate "header" tag                                              |
| api.cookie                               | generate "cookie" tag                                              |
| api.body                                 | generate "json" tag                                                |
| api.path                                 | generate "path" tag                                                |
| api.form                                 | generate "form" tag                                                |
| api.go_tag (protobuf)<br>go.tag (thrift) | passing go_tag through will generate the content defined in go_tag |
| api.vd                                   | generate "vd" tag                                                  |

| _Method annotation_ |                                   |
| ------------------- | --------------------------------- |
| annotation          | description                       |
| api.get             | define GET methods and routes     |
| api.post            | define POST methods and routes    |
| api.put             | define PUT methods and routes     |
| api.delete          | define DELETE methods and routes  |
| api.patch           | define PATCH methods and routes   |
| api.options         | define OPTIONS methods and routes |
| api.head            | define HEAD methods and routes    |
| api.any             | define ANY methods and routes     |

#### Usage:

##### Field annotation:

Thrift:

```thrift
struct Demo {
    1: string Demo (api.query="demo", api.path="demo");
    2: string GoTag (go.tag="goTag:"tag"");
    3: string Vd (api.vd="$!='your string'");
}
```

Protobuf:

```protobuf
message Demo {
  string Demo = 1[(api.query)="demo",(api.path)="demo"];
  string GoTag = 2[(api.go_tag)="goTag:"tag""];
  string Vd = 3[(api.vd)="$!='your string'"];
}
```

##### Method annotation:

Thrift:

```thrift
service Demo {
    Resp Method(1: Req request) (api.get="/route");
}
```

Protobuf:

```protobuf
service Demo {
  rpc Method(Req) returns(Resp) {
    option (api.get) = "/route";
  }
}
```

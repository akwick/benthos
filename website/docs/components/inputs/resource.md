---
title: resource
type: input
status: stable
categories: ["Utility"]
---

<!--
     THIS FILE IS AUTOGENERATED!

     To make changes please edit the contents of:
     lib/input/resource.go
-->

import Tabs from '@theme/Tabs';
import TabItem from '@theme/TabItem';


Resource is an input type that runs a resource input by its name. This input
allows you to run the same configured input resource in multiple places.

```yaml
# Config fields, showing default values
input:
  resource: ""
```

Resource inputs also have the advantage of name based metrics and logging. For
example, the config:

```yaml
input:
  broker:
    inputs:
      - kafka:
          addresses: [ TODO ]
          topics: [ foo ]
          consumer_group: foogroup
      - gcp_pubsub:
          project: bar
          subscription: baz
```

Is equivalent to:

```yaml
input:
  broker:
    inputs:
      - resource: foo
      - resource: bar

resources:
  inputs:
    foo:
      kafka:
        addresses: [ TODO ]
        topics: [ foo ]
        consumer_group: foogroup

    bar:
      gcp_pubsub:
        project: bar
        subscription: baz
 ```

But now the metrics path of Kafka input will be
`resources.inputs.foo`, this way of flattening observability
labels becomes more useful as configs get larger and more nested.



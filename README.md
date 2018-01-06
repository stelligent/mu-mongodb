# mu-mongodb

This is a mongodb extension for the mu framework.

# Working with mu

This extension currently only works with mu version 1.3.1-develop. To install this version:

```
curl -s https://getmu.io/install.sh | INSTALL_VERSION=1.3.1-develop sh
```

# Using the Extension

Here's some example code of this extension in action:

```
namespace: ext
environments:
  - name: acceptance
    loadbalancer:
      hostedzone: elasticoperations.com
      name: ext
    cluster:
      instanceType: t2.medium
      desiredCapacity: 1
      maxSize: 2
  - name: production
    loadbalancer:
      hostedzone: demo.elasticoperations.com
      name: ext
    cluster:
      instanceType: t2.medium
      desiredCapacity: 1
      maxSize: 2
service:
  name: ext
  memory: 1024
  healthEndpoint: /
  port: 80
  pathPatterns:
  - /*
  database:
    name: mu-extension-example
    engine: mongodb
  pipeline:
    source:
      provider: GitHub
      repo: stelligent/mu-extension-example

parameters:
  'ext-database-ext-acceptance':
    DatabaseMasterUsername: stelligent
  'ext-database-ext-production:
    DatabaseMasterUsername: stelligent

extensions:
- url: https://github.com/stelligent/mu-mongodb/archive/v0.15.zip
```

This example mu.yml file will create acceptance and production environments along with a mongodb instantiation. Mongodb will be accessible to your instances on port 27017

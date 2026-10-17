___
- tags: #GraphQL #owasp #idors #mutations
___
## GraphQL
Es un lenguaje de consulta para **APIs**. A diferencia de las APIs tradicionales que tienen endpoints fijos, GraphQL permite a los clientes solicitar sólo la información que necesitan y obtener una respuesta personalizada en función de sus necesidades.
### Introspection
Es un mecanismo que permite a los clientes **obtener información sobre el esquema Graphql** de una API. Esto significa que los clientes pueden explorar y descubrir los tipos de datos, los campos y las relaciones que existen en la API.
### Mutations
Son operaciones que permiten a los clientes **modificar los datos en la API**. A diferencia de las consultas, que sólo permiten la lectura de datos, las mutaciones permiten a los clientes agregar, actualizar o eliminar datos.
### IDORs
Estas pueden ocurrir cuando un atacante es capaz de adivinar o enumerar identificadores **(IDs)** de objetos dentro de la API


## Introspection Query Fixed From Hacktricks
```graphql
fragment FullType on __Type {
  kind
  name
  description
  fields {
    name
    description
    args {
      ...InputValue
    }
    type {
      ...TypeRef
    }
  }
  inputFields {
    ...InputValue
  }
  interfaces {
    ...TypeRef
  }
  enumValues {
    name
    description
  }
  possibleTypes {
    ...TypeRef
  }
}

fragment InputValue on __InputValue {
  name
  description
  type {
    ...TypeRef
  }
  defaultValue
}

fragment TypeRef on __Type {
  kind
  name
  ofType {
    kind
    name
    ofType {
      kind
      name
      ofType {
        kind
        name
        ofType {
          kind
          name
          ofType {
            kind
            name
            ofType {
              kind
              name
              ofType {
                kind
                name
              }
            }
          }
        }
      }
    }
  }
}

query IntrospectionQuery {
  __schema {
    queryType {
      name
    }
    mutationType {
      name
    }
    types {
      ...FullType
    }
    directives {
      name
      description
      locations
      args {
        ...InputValue
      }
    }
  }
}
```

___
## Referencia
- [GraphQL - Hacktricks](https://book.hacktricks.wiki/en/network-services-pentesting/pentesting-web/graphql.html).
- [Visual GraphQL Schema - Voyager](https://apis.guru/graphql-voyager/)

___
## Laboratorios
- [GraphQL IDOR -> skf-labs](https://github.com/blabla1337/skf-labs/tree/master/nodeJs/Graphql-IDOR).
- [GraphQL Introspectoin -> skf-labs](https://github.com/blabla1337/skf-labs/tree/master/nodeJs/Graphql-Introspection).
- [GraphQL Mutation-> skf-labs](https://github.com/blabla1337/skf-labs/tree/master/nodeJs/Graphql-Mutations).
- [GraphQL Injection -> skf-labs](https://github.com/blabla1337/skf-labs/tree/master/nodeJs/Graphql-Injection).
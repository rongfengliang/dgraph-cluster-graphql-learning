# dgraph cluster with graphql


## How to Running


* Start service

```code
docker-compose up -d
```

* deploy schema

>  can execute in any alpha server (Note: change request url)

```code
curl -X POST localhost:8080/admin/schema -d '@schema.graphql'
```

* Do some mutation

```code
mutation {
  addProduct(input: [
    { name: "GraphQL on Dgraph"},
    { name: "Dgraph: The GraphQL Database"}
  ]) {
    product {
      productID
      name
    }
  }
  addCustomer(input: [{ username: "Michael"}]) {
    customer {
      username
    }
  }
}

---------
mutation {
  addReview(input: [{
    by: {username: "Michael"}, 
    about: { productID: "0x3"}, 
    comment: "Fantastic, easy to install, worked great.  Best GraphQL server available",
    rating: 10}]) 
  {
    review {
      comment
      rating
      by { username }
      about { name }
    }
  }
}
```

* Do some query

```code
query {
  queryProduct {
    productID
    name
    reviews {
      id
      rating
      comment
    }
  }
}
```
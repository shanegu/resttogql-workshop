+++
title = "Changing Queries"
chapter = false
weight = 2
+++

## Our Goal
The goal of this section is to change how the initial page loads.   Currenly it is using the following RESTful endpoint.  We want to change this to use oue new GraphQL schema that we looked at in the last section.

The good news is we can add this query is such a way to be able to query the existing REST endpoint - we do this by using an HTTP Resolver.

This method sometimes called the service facade pattern allows us with minimal code changes to facade the existing API with our new one, so reducing the introduction of bugs.
Typically this pattern is used when the service being facaded is legacy code that no-one is maintaining.




{{% notice info %}}
For more information on resolvers see [https://docs.aws.amazon.com/appsync/latest/devguide/configuring-resolvers.html](https://docs.aws.amazon.com/appsync/latest/devguide/configuring-resolvers.html)
{{% /notice %}}

### Testing Queries
With AppSync you can test queries that you clients will use from inside the AWS Console Appsync UI:

1. Select Queries from the left hand
2. Select 'Login wit User Pools' 
3. For Client id - fill in your user pool client id ( previously generated in last section)
4. Enter the User Name and Password of the user you created in the last section
5. Read / Delete everything that is already in the Query console.

We can test our query by using the Query browser thats built into AWS AppSync.  Copy and paste the following, that will call the ListCompanies query we have defined and returns 4 attributes(company_id, company_name, stock_name, stock_value) of that company.

```tsx
query ListCompanies {
    listCompanies { 
        company_id 
        company_name
        stock_name
        stock_value
    }
}

```

Try changing the return values and executing the query again - this is where we begin to see the flexibility of GraphQL. The output will change based on the query - it should look like this.

![Smalleer Query](/images/SmallerQuery.png)


### Exploring the Docs
Because GraphQL is strongly typed, the documents for it can be easily introspected and we can
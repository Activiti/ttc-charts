# ttc-charts

Not a GitHub Pages repo - clone the repo to use the chart.

Currently only the backend of the example as the UI is not yet fully parameterised. To be used for running ttc-acceptance-tests

UI can be configured to point to deployed backend - https://github.com/Activiti/ttc-docs/blob/master/workshop.md#dashboard-ui-angular-app

Go to /graphiql path off gateway to see graphiql. Subscribe to variable creation events with:

```
subscription {
  engineEvents{
    processDefinitionKey
    VARIABLE_CREATED {
      timestamp
      entity{
        processInstanceId
        value
        name
      }
    }
  }
}
```

You'll need to start the feed to see anything, either from POSTMAN or the button in the UI
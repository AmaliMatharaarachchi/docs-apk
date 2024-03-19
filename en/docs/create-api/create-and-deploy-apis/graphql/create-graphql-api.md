# GraphQL

GraphQL, which has been developed by Facebook, is a data query language for APIs. When using GraphQL, users can explicitly specify as to what data they need from an API. GraphQL APIs are an alternative to REST-based APIs.

You can use a Schema Definition Language (SDL) schema to design a GraphQL API in WSO2 APK, similar to developing REST APIs using OpenAPI Specifications (a.k.a. Swagger Definitions).

## Creating and deploying a GraphQL API

Follow the instructions below to design a GraphQL API.

### Using apk-conf file

1. Save and download the sample [StarWarsAPI.graphql](../../../assets/files/get-started/StarWarsAPI.graphql) file. This is the GraphQL SDL of the API that we are going to deploy in APK.

2. Execute the following request to generate the APK configuration. Use the values provided in the table below in the body of your request. 

    |    Field     |                               Value                                                      |
    |--------------|------------------------------------------------------------------------------------------|
    | definition   | `StarWarsAPI.graphql` file that was downloaded at the beginning of Step 1.

    === "Sample Request"

        ```
        curl -k --location 'https://api.am.wso2.com:9095/api/configurator/1.0.0/apis/generate-configuration' \
        --header 'Host: api.am.wso2.com' \
        --form 'definition=@"/Users/user/StarWarsAPI.graphql"'
        --form 'apiType="GRAPHQL"' \
        ```

    === "Sample Request"

        ```
        ---
        name: ""
        basePath: "/"
        version: ""
        type: "GRAPHQL"
        defaultVersion: false
        subscriptionValidation: false
        operations:
        - target: "hero"
          verb: "QUERY"
          secured: true
          scopes: []
        - target: "reviews"
          verb: "QUERY"
          secured: true
          scopes: []
        - target: "search"
          verb: "QUERY"
          secured: true
          scopes: []
        - target: "character"
          verb: "QUERY"
          secured: true
          scopes: []
        - target: "droid"
          verb: "QUERY"
          secured: true
          scopes: []
        - target: "human"
          verb: "QUERY"
          secured: true
          scopes: []
        - target: "allHumans"
          verb: "QUERY"
          secured: true
          scopes: []
        - target: "allDroids"
          verb: "QUERY"
          secured: true
          scopes: []
        - target: "allCharacters"
          verb: "QUERY"
          secured: true
          scopes: []
        - target: "starship"
          verb: "QUERY"
          secured: true
          scopes: []
        - target: "createReview"
          verb: "MUTATION"
          secured: true
          scopes: []
        - target: "reviewAdded"
          verb: "SUBSCRIPTION"
          secured: true
          scopes: []

        ```

    === "Request Format"

      ```
      curl --location 'https://<host>:9095/api/configurator/1.0.0/apis/generate-configuration' \
      --header 'Host: <host>' \
      --form 'apiType="<api-type>"' \
      --form 'definition=@"<path/to/StarWarsAPI.graphql>"'
      ```

3. You will get the apk-conf file content as the response, as seen in the above sample response. Save this content into a file named `StarWars.apk-conf`. You will need to fill in the name, basePath, version and endpoint configuration fields before deploying the API.

5. To invoke the system APIs such as for deploying, we need a valid access token issued by an identity provider (IdP). Follow the ["Generate Access Token"](../../../develop-and-deploy-api/security/generate-access-token.md) documentation to generate an access token.

6. After generating the token, you can deploy the GraphQL API with the command

    === "Sample Request"

        ```
        curl -k --location 'https://api.am.wso2.com:9095/api/deployer/1.0.0/apis/deploy' \
        --header 'Host: api.am.wso2.com' \
        --header 'Authorization: bearer eyJhbGciOiJSUzI1NiIsICJ0eXAiOiJKV1QiLCAia2lkIjoiZ2F0ZXdheV9jZXJ0aWZpY2F0ZV9hbGlhcyJ9.eyJpc3MiOiJodHRwczovL2lkcC5hbS53c28yLmNvbS90b2tlbiIsICJzdWIiOiI0NWYxYzVjOC1hOTJlLTExZWQtYWZhMS0wMjQyYWMxMjAwMDIiLCAiZXhwIjoxNjg4MTMxNDQ0LCAibmJmIjoxNjg4MTI3ODQ0LCAiaWF0IjoxNjg4MTI3ODQ0LCAianRpIjoiMDFlZTE3NDEtMDA0Ni0xOGE2LWFhMjEtYmQwYTk4ZjYzNzkwIiwgImNsaWVudElkIjoiNDVmMWM1YzgtYTkyZS0xMWVkLWFmYTEtMDI0MmFjMTIwMDAyIiwgInNjb3BlIjoiZGVmYXVsdCJ9.RfKQq2fUZKZFAyjimvsPD3cOzaVWazabmq7b1iKYacqIdNjkvO9CQmu7qdtrVNDmdZ_gHhWLXiGhN4UTSCXv_n1ArDnxTLFBroRS8dxuFBZoD9Mpj10vYFSDDhUfFqjgMqtpr30TpDMfee1wkqB6K757ZSjgCDa0hAbv555GkLdZtRsSgR3xWcxPBsIozqAMFDCWoUCbgTQuA5OiEhhpVco2zv4XLq2sz--VRoBieO12C69KnGRmoLuPtvOayInvrnV96Tbt9fR0fLS2l1nvAdFzVou0SIf9rMZLnURLVQQYE64GR14m-cFRYdUI9vTsFHZBl5w-uCLdzMMofzZaLQ' \
        --form 'apkConfiguration=@"/Users/user/StarWars.apk-conf"' \
        --form 'definitionFile=@"/Users/user/StarWarsAPI.graphql"'
        ```

    === "Sample Response"

        ```
        ---
        name: "StarWarsAPI"
        basePath: "/starwars"
        version: "1.0.0"
        type: "GRAPHQL"
        defaultVersion: false
        subscriptionValidation: false
        operations:
        - target: "hero"
          verb: "QUERY"
          secured: true
          scopes: []
        - target: "reviews"
          verb: "QUERY"
          secured: true
          scopes: []
        - target: "search"
          verb: "QUERY"
          secured: true
          scopes: []
        - target: "character"
          verb: "QUERY"
          secured: true
          scopes: []
        - target: "droid"
          verb: "QUERY"
          secured: true
          scopes: []
        - target: "human"
          verb: "QUERY"
          secured: true
          scopes: []
        - target: "allHumans"
          verb: "QUERY"
          secured: true
          scopes: []
        - target: "allDroids"
          verb: "QUERY"
          secured: true
          scopes: []
        - target: "allCharacters"
          verb: "QUERY"
          secured: true
          scopes: []
        - target: "starship"
          verb: "QUERY"
          secured: true
          scopes: []
        - target: "createReview"
          verb: "MUTATION"
          secured: true
          scopes: []
        - target: "reviewAdded"
          verb: "SUBSCRIPTION"
          secured: true
          scopes: []
        ```

    === "Request Format"

        ```
        curl --location 'https://<host>:9095/api/deployer/1.0.0/apis/deploy' \
        --header 'Host: <host>' \
        --header 'Authorization: bearer <access-token>' \
        --form 'apkConfiguration=@"path/to/StarWars.apk-conf"' \
        --form 'definitionFile=@"path/to/StarWarsAPI.graphql"'
        ```

7. Execute the command below. You will be able to see that the `StarWars` API is successfully deployed.
    
    === "Command"
        ```
        kubectl get apis
        ```

### Using CRs



## Invoking a GraphQL API

You will need a GraphQL backend in order to invoke the API and get a correct response. A sample backend for the GraphQL Star Wars API has been provided under [this section.](./create-graphql-api.md#sample-backend-for-graphql)

Once your GraphQL API has been deployed, you can invoke it. The endpoint of the API would be <apk-gateway-url>/<api-basepath>. 

For the above API, the base path is "/starwars/1.0.0", so the API URL would be <apk-gateway-url>/starwars/1.0.0.

A sample GraphQL call is provided below.

```
curl --location 'https://default.gw.wso2.com:9095/starwars/3.14' \
--header 'Host: default.gw.wso2.com' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer access-token' \
--data '{"query":"query hero ($episode: Episode) {\n    hero (episode: $episode) {\n        id\n        name\n        appearsIn\n    }\n}","variables":{"episode":1}}'
```

!!! note
    As of now, WSO2 APK only supports QUERY and MUTATION operations for GraphQL.


## Sample Backend for GraphQL

A sample GraphQL backend for the Star Wars GraphQL API that can be used for testing purposes is provided below.

```yaml
apiVersion: v1
kind: ConfigMap
metadata:
  name: graphql-faker-schema
  namespace: apk
data:
  schema.graphql: |
    schema {
      query: Query
      mutation: Mutation
      subscription: Subscription
    }

    # The query type, represents all of the entry points into our object graph
    type Query {
      hero(episode: Episode): Character
      reviews(episode: Episode!): [Review]
      search(text: String): [SearchResult]
      character(id: ID!): Character
      droid(id: ID!): Droid
      human(id: ID!): Human
      allHumans(first: Int): [Human]
      allDroids(first: Int): [Droid]
      allCharacters(first: Int): [Character]
      starship(id: ID!): Starship
    }

    # The mutation type, represents all updates we can make to our data
    type Mutation {
      createReview(episode: Episode, review: ReviewInput!): Review
    }

    # The subscription type, represents all subscriptions we can make to our data
    type Subscription {
      reviewAdded(episode: Episode): Review
    }

    # The episodes in the Star Wars trilogy
    enum Episode {
      # Star Wars Episode IV: A New Hope, released in 1977.
      NEWHOPE

      # Star Wars Episode V: The Empire Strikes Back, released in 1980.
      EMPIRE

      # Star Wars Episode VI: Return of the Jedi, released in 1983.
      JEDI

      # Star Wars Episode III: Revenge of the Sith, released in 2005
      SITH
    }

    # A character from the Star Wars universe
    interface Character {
      # The ID of the character
      id: ID!

      # The name of the character
      name: String!

      # The friends of the character, or an empty list if they have none
      friends: [Character]

      # The friends of the character exposed as a connection with edges
      friendsConnection(first: Int, after: ID): FriendsConnection!

      # The movies this character appears in
      appearsIn: [Episode]!
    }

    # Units of height
    enum LengthUnit {
      # The standard unit around the world
      METER

      # Primarily used in the United States
      FOOT
    }

    # A humanoid creature from the Star Wars universe
    type Human implements Character {
      # The ID of the human
      id: ID!

      # What this human calls themselves
      name: String!

      # The home planet of the human, or null if unknown
      homePlanet: String

      # Height in the preferred unit, default is meters
      height(unit: LengthUnit = METER): Float

      # Mass in kilograms, or null if unknown
      mass: Float

      # This human's friends, or an empty list if they have none
      friends: [Character]

      # The friends of the human exposed as a connection with edges
      friendsConnection(first: Int, after: ID): FriendsConnection!

      # The movies this human appears in
      appearsIn: [Episode]!

      # A list of starships this person has piloted, or an empty list if none
      starships: [Starship]
    }

    # An autonomous mechanical character in the Star Wars universe
    type Droid implements Character {
      # The ID of the droid
      id: ID!

      # What others call this droid
      name: String!

      # This droid's friends, or an empty list if they have none
      friends: [Character]

      # The friends of the droid exposed as a connection with edges
      friendsConnection(first: Int, after: ID): FriendsConnection!

      # The movies this droid appears in
      appearsIn: [Episode]!

      # This droid's primary function
      primaryFunction: String
    }

    # A connection object for a character's friends
    type FriendsConnection {
      # The total number of friends
      totalCount: Int

      # The edges for each of the character's friends.
      edges: [FriendsEdge]

      # A list of the friends, as a convenience when edges are not needed.
      friends: [Character]

      # Information for paginating this connection
      pageInfo: PageInfo!
    }

    # An edge object for a character's friends
    type FriendsEdge {
      # A cursor used for pagination
      cursor: ID!

      # The character represented by this friendship edge
      node: Character
    }

    # Information for paginating this connection
    type PageInfo {
      startCursor: ID
      endCursor: ID
      hasNextPage: Boolean!
    }

    # Represents a review for a movie
    type Review {
      # The movie
      episode: Episode

      # The number of stars this review gave, 1-5
      stars: Int!

      # Comment about the movie
      commentary: String
    }

    # The input object sent when someone is creating a new review
    input ReviewInput {
      # 0-5 stars
      stars: Int!

      # Comment about the movie, optional
      commentary: String

      # Favorite color, optional
      favorite_color: ColorInput
    }

    # The input object sent when passing in a color
    input ColorInput {
      red: Int!
      green: Int!
      blue: Int!
    }

    type Starship {
      # The ID of the starship
      id: ID!

      # The name of the starship
      name: String!

      # Length of the starship, along the longest axis
      length(unit: LengthUnit = METER): Float

      coordinates: [[Float!]!]
    }

    union SearchResult = Human | Droid | Starship

---
apiVersion: apps/v1
kind: Deployment
metadata:
  name: graphql-faker
  namespace: apk
  labels:
    app: graphql-faker
spec:
  replicas: 1
  selector:
    matchLabels:
      app: graphql-faker
  template:
    metadata:
      labels:
        app: graphql-faker
    spec:
      containers:
        - name: graphql-faker
          image: apisguru/graphql-faker
          args: ["--open=false", "/etc/graphql-faker/schema.graphql"]
          ports:
            - containerPort: 9002
          volumeMounts:
            - name: schema-volume
              mountPath: /etc/graphql-faker
          resources:
            requests:
              memory: "256Mi"
              cpu: "250m"
            limits:
              memory: "512Mi"
              cpu: "500m"
      volumes:
        - name: schema-volume
          configMap:
            name: graphql-faker-schema
---
apiVersion: v1
kind: Service
metadata:
  name: graphql-faker-service
  namespace: apk
spec:
  type: LoadBalancer
  ports:
    - port: 9002
      targetPort: 9002
      protocol: TCP
  selector:
    app: graphql-faker
```

To apply the above CRs, copy and paste them into a yaml file and then use the following command in the same directory as the yaml file. You may have to replace the namespace value in the above CRs to match your namespace.
```
kubectl apply -f . -n <namespace>
```

You can check the status of the pods by using 
```
kubectl get pods -n <namespace>
```

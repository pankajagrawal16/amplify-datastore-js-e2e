# Amplify Datastore - JS

This is the sample code to illustrate the [offline data store](https://docs.amplify.aws/lib/datastore/getting-started/q/platform/js)

## Prerequisite:

Install Amplify CLI

```sh
npm i -g @aws-amplify/cli
```

## Clone repo to host inside codecommit

```sh
    aws codecommit create-repository --repository-name amplify-datastore-js-e2e
    git clone --bare git@github.com:pankajagrawal16/amplify-datastore-js-e2e.git
    git push --mirror codecommit://amplify-datastore-js-e2e
    cd ..
    rm -rf amplify-datastore-js-e2e.git/
    git clone codecommit://amplify-datastore-js-e2e
    cd amplify-datastore-js-e2e/
```

## Init project and setup CI/CD

```
    amplify init
```

- Example 

```
    ~/amplify-datastore-js-e2e (master)$ amplify init
    Note: It is recommended to run this command from the root of your app directory
    ? Enter a name for the environment dev
    ? Choose your default editor: IntelliJ IDEA
    Using default provider  awscloudformation
    
    For more information on AWS Profiles, see:
    https://docs.aws.amazon.com/cli/latest/userguide/cli-configure-profiles.html
    
    ? Do you want to use an AWS profile? Yes
    ? Please choose the profile you want to use usermgt

```

```
    amplify add hosting
```

- Example

```
    ~/amplify-datastore-js-e2e (master)$ amplify add hosting
    ? Select the plugin module to execute Hosting with Amplify Console (Managed hosting with custom domains, Continuous deployment)
    ? Choose a type Continuous deployment (Git-based deployments)
    ? Continuous deployment is configured in the Amplify Console. Please hit enter once you connect your repository 
    Amplify hosting urls: 
    ┌──────────────┬──────────────────────────────────────────────┐
    │ FrontEnd Env │ Domain                                       │
    ├──────────────┼──────────────────────────────────────────────┤
    │ master       │ https://master.<hash>.amplifyapp.com │
    └──────────────┴──────────────────────────────────────────────┘

```

## Add DataStore to your app

Add support for datastore and api.

```
    amplify add api
```

- Example

Its important that you enable conflict resolution feature while setting up GraphQL API.

```
    ~/amplify-datastore-js-e2e (master)$ amplify add api
    ? Please select from one of the below mentioned services: GraphQL
    ? Provide API name: amplifydatastorejse2
    ? Choose the default authorization type for the API API key
    ? Enter a description for the API key: Demo
    ? After how many days from now the API key should expire (1-365): 7
    ? Do you want to configure advanced settings for the GraphQL API Yes, I want to make some additional changes.
    ? Configure additional auth types? No
    ? Configure conflict detection? Yes
    ? Select the default resolution strategy Auto Merge
    ? Do you have an annotated GraphQL schema? Yes
    ? Provide your schema file path: schema.graphql
  
```

## Create the cloud-based backend

```sh
    amplify push
```

## Run modelgen

Model-Gen generates code to implement language specific model classes.

```sh
    amplify codegen models
```

At this stage, you can already use the app in standalone mode.  No AWS Account is required.

## Implement & Start the App 

```sh
# start the app 
npm run start
```

## Cleanup 

At the end of your test, you can delete the backend infrastructure

```sh
amplify delete
```

You might need to manually delete two Amazon S3 buckets created.
In the [AWS Console](https://s3.console.aws.amazon.com/s3/home), search for the two buckets having `datastore` part of their name.

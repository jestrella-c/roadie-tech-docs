humanName: CircleCI
logoImage: '../../../assets/logos/circle-ci/circle-ci-logo-only-black.png'
integrationType: OSS plugin
---

## Introduction

The Backstage Circle CI plugin integrates with Circle CI to show your build information inside Backstage where it can be associated with your services.

## Using the Plugin

1. Add a proxy configuration in Roadie at `/administration/settings/proxy` - see guide [here](../../custom-plugins/proxy/#setup).

Path: `/circleci/api`
Target: `https://circleci.com/api/v1.1`
Headers: `Circle-Token`: `${CIRCLECI_AUTH_TOKEN}`

2. Get and provide a CIRCLECI_AUTH_TOKEN as an environment variable in Roadie at `/administration/settings/secrets` - see below for instructions on how to get the token. 

3. Add a circleci.com/project-slug annotation to your respective catalog-info.yaml files following the Component format

```yaml
# Example catalog-info.yaml entity definition file
apiVersion: backstage.io/v1alpha1
kind: Component
metadata:
  # ...
  annotations:
    # This also supports bitbucket/xxx/yyy
    circleci.com/project-slug: github/my-org/my-repo
spec:
  type: service
# ...
```

4. Add the CircleCi plugin to one of your entities with the correct annotation in Roadie as a new tab. 


## Creating a token

In order to make requests to the CircleCI API, you must provide Roadie with an API key.

1. Make sure you are logged in to Circleci as the user you want to use for Backstage. We recommend creating a Github bot account for this.

2. Go to https://app.circleci.com/settings/user/tokens and select Create New Token.

   ![Personal API Tokens screen in CircleCI with no tokens selected](./personal-api-tokens.png)

3. Give the token a name and click Add API Token.

   ![The Create API Token modal in CircleCI with an input with the name Backstage inside it](./create-api-token.png)

4. Circleci will print the token that Backstage needs.

5. Follow the instructions on how to share the API Token with Roadie.


## References

- [CircleCI docs for creating API tokens](https://circleci.com/docs/api/#add-an-api-token)

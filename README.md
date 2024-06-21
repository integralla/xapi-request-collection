# xAPI Request Collection

The [Experience API (xAPI)](https://xapi.ieee-saopen.org/) Standard is an open-source e-learning
specification that defines a standard format for representing, and securely sharing, data regarding
a wide variety of learning experiences.

This API request collection provides a basic set of requests that can be used to interact with the
Learning Record Store (LRS) endpoint resources defined by the specification. Common use cases for
the collection would include prototyping an integration, data exploration, or troubleshooting an
issue.

The collection is defined using [Bruno](https://www.usebruno.com/), an API client similar to
Postman or Insomnia. We've chosen Bruno because it's Git-friendly, open source, and offline (no
account required) with collections stored locally in a folder on your filesystem.

## Getting Started

### 1. Download Bruno

Download and install the [Bruno](https://www.usebruno.com/downloads) API client if you have not
already.

### 2. Clone Project

Clone this project into a folder of your choice on your local file system.

```shell
git clone https://github.com/integralla/xapi-request-collection.git
```

### 3. Import Collection

1. Open Bruno
2. Click on `Import Collection`
3. In the "Import Collection" dialog, click `Bruno Collection`
4. When prompted, use the file system navigator to open the folder where you cloned the collection
   and open the file named `bruno.json`

### 4. Setup DotEnv File

Bruno supports specifying environment configuration details, including secrets, in a DotEnv
file (`.env`) stored in the same folder where the project was cloned. This is where you can
configure things like the host name or base URL of the LRS endpoint, the xAPI version you're
targeting, as well as the credentials used to authenticate requests to secure resources.

The configuration values used by the collection can be viewed in the provided `.env.sample` file.
Copy or rename this file to `.env` and change the variables documented there as needed.

### 5. Configure Authentication

By default, requests to secure resources are configured to use HTTP Basic Authentication, using the
username and password defined in the project's `.env` file. If your LRS supports Basic
Authentication, you should be able to issue requests at this point.

The project also defines a request to an `/xapi/oauth/token` endpoint which can be used to request
an
access token if the LRS supports authentication using an OAuth 2.0 client credentials grant type. If
you use this authentication mechanism, you'll need to edit the collection's `Auth` configuration. To
do so, follow the steps below:

1. Click on the gear icon at the top right of the client window
2. Select the `Auth` header
3. Select the `Bearer Token` auth type
4. In the token field, enter the following variable: `{{access_token}}`
5. Save your changes.

Now, when you issue a request to the `/xapi/oauth/token` resource, it will set that variable with
the `access_token` value in the returned response.

You should now be ready to start issuing requests to your LRS.

## Integralla LRS Extensions

We are the developers of Integralla LRS ([integralla.com](https://integralla.com)) so we've also
added support for a few features that are unique to that implementation, or otherwise not defined by
the specification.

### Extension Resources

Integralla LRS provides two extension resources to help organizations to comply with data privacy
regulations, specifically:

* An extension that can be used to anonymize the personal data for a given agent identifier (IFI)
* An extension that can be used to restrict processing for the personal data associated with a given
  agent identifier

Both of these can be found under the `agents` request folder.

### Pseudonymization

Integralla LRS also provides built in support for pseudonymizing personal data captured in `Agent`
or `Group` objects wherever they are supported in the xAPI `Statement` data model. The `GET` request
examples for the `/statements` resource include a `pseudonymized` parameter not defined by the
specification which enables a requester to retrieve pseudonymized `Statement` objects.

### OAuth 2.0 Client Credentials Grant

Integralla LRS support authentication using an OAuth 2.0 Client Credentials
Grant [[RFC 6749](https://datatracker.ietf.org/doc/html/rfc6749#section-4.4)].
The `/xapi/oauth/token`
endpoint can be used to request an access token for this purpose. Refer to the `Docs` tab of the
request for further information.

## Request Documentation

We've attempted to provide minimal documentation under the `Docs` tab for each request. At minimum,
this includes links to the relevant sections of the specification, as well as links to documentation
specific to Integralla LRS, which is hosted
at [https://docs.integralla.com/](https://docs.integralla.com/).

## Contributing

We welcome contributions through issue reports, feature requests, and pull requests.



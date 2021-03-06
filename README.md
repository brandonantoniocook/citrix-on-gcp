## Overview
This repository contains scripts and templates to simplify deployment of the resources described in Citrix's [Deploying Citrix Cloud XenApp and XenDesktop Service on the Google Cloud Platform](https://citrix.sharefile.com/d-sd6bf3fabc954f608) published December 2017.

## Before you begin
You'll need a PowerShell environment with the [Google Cloud SDK](https://cloud.google.com/sdk/) installed.

## Deploying Citrix
Clone the repository and run deploy.ps1.

``` shell
.\deploy.ps1
```

You will be prompted for three values to allow the script to interact with Citrix Cloud APIs:
- CTXSecureClientID: This is the client ID of a client configured at Citrix Cloud ([cloud.com](https://cloud.com/)) > Identity and Access Management > API Access.
- CTXSecureClientSecret: This is the secret you were provided when the client ID was created.
- CTXCustomerID: This is the Customer ID identified on Citrix Cloud ([cloud.com](https://cloud.com/)) > Identity and Access Management > API Access.

The script will use gcloud defaults to initialize parameters such as region and project.

The deployment takes about 30 minutes to complete.

## Retrieving passwords

Use get-domain-admin-password.ps1 to retrieve the password associated with the domain administrator (ctx-[SUFFIX]\Administrator where [SUFFIX] is the randomly-assigned suffix associated with you deployment).

``` shell
.\get-domain-admin-password.ps1
```

You can use the domain administrator credentials to Remote Desktop to the mgmt instance.

The ctx-[SUFFIX] domain will be populated with ten sample users.  The usernames and passwords can be retrived with get-domain-users.ps1.

``` shell
.\get-domain-users.ps1
```

These ten domain users are configured with access to Notepad as a sample application through your xendesktop.net Citrix Storefront.

## Resizing
Add VDA instances by running resize.ps1 and specifying a larger number for the "Workers" parameter.

``` shell
.\resize.ps1 -Workers 3
```

## Cleaning up
Remove billable GCP resources with cleanup.ps1.

``` shell
.\cleanup.ps1
```

## Contributing
See [CONTRIBUTING](CONTRIBUTING.md).

## License
Copyright 2018, Google, Inc.

Licensed under the Apache License, Version 2.0

See [LICENSE](LICENSE).


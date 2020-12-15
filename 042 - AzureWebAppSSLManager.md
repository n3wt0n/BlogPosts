Do you want to have __FREE SSL Certificates__ for your Azure WebApps and Azure Functions, renew them automatically and manage them hassle-free?

Keep reading then...

### Intro

Today I want to talk to you about a project of mine, which is completely Open Source and free to use, that allows you to create free SSL Certificates (_thanks to Let's Encrypt_), install it on your Azure WebApp or Azure Function, and automatically renew them before their expiration.

__SSL Certificates are very important__, they allow you (among other things) to enable HTTPS on your websites, web applications and serverless functions.

### Welcome Azure WebApp SSL Manager

![Logo](https://dev-to-uploads.s3.amazonaws.com/i/s801j2bu5zit5sqj6j3l.png)

The project name is ___Azure WebApp SSL Manager___, and it's an Azure Function that acquires and manages __free SSL certificates__ for applications hosted on Azure Web Apps and Azure Function Apps.

It is fully Open Source, and [hosted on GitHub](https://github.com/n3wt0n/AzureWebAppSSLManager):

{% github n3wt0n/AzureWebAppSSLManager no-readme %}

You can use it to acquire FREE certificates for any domain you own, __including wildcards__. Those certificate are __completely trusted__ since they are generated using the [Let's Encrypt](https://letsencrypt.org/) Certification Authority.

Azure WebApp SSL Manager is also __listed on the official Let'S Encrypt website__ as the first client for Azure ([take a look here](https://letsencrypt.org/docs/client-options/#clients-microsoft-azure))

### Why use your project instead of Let's Encrypt directly?

Good question. __Azure WebApp SSL Manager makes it super easy and automatic__ to create, renew and manage all the certificates.

#### Without Azure WebApp SSL Manager

If you use Let's Encrypt directly, instead, you would need to:

- Manually generate the certificate with a multi-step flow
- Save the _account key_ somewhere
- Convert the certificate file in something usable by your service
- Remember to renew your certificates every 3 months
- Re-upload the certificate file
- Replace the old certificate with the new one
- ___Repeat this for every and each certificate!___

And what happens if you forget to renew on time? Or you are away? Or if you lose the account key?

__Why going through all those problems when you can have everything automatically done?__

#### WITH Azure WebApp SSL Manager

- Deploy the Azure Function (___can be done automatically as well from the GitHub repo!___)
- Add the list of domains you need the certificate for to the configuration file
- Forget about everything and __Azure WebApp SSL Manager will do all the work for you__

Give Azure WebApp SSL Manager a try, check out the [GitHub repo](https://github.com/n3wt0n/AzureWebAppSSLManager) now! 

### How it works - some details

The main Tasks performed are:

- Order/Renewal of SSL certificates from Let's Encrypt free trusted CA
- Validation of the order using Azure DNS TXT record
- Download of the certificates and save them on Azure Blob Storage
- Installation of the certificates on Azure App Service Web App or Function App
- Association of the certificates to the Web App or Function App hostname bindings

#### Let's talk technical

The project is written in .NET Core 3.1 (_Porting to .NET 5 is in progress and pending full support by Azure Functions_) and can be hosted on either Azure Functions (Windows) or Azure Functions (Linux).

The deployment can be done:

- Manually, downloading the source files and building/publishing it
- Automatically, via ARM, using the PowerShell script provided
- Automatically, via ARM, using the Azure CLI with the bash script provided
- Automatically, via ARM, using the Azure CLI with the cmd script provided
- Automatically, via ARM, using the Wizard provided

![Deploy](https://dev-to-uploads.s3.amazonaws.com/i/dpulo7bndn3xh2ay865m.png)

### Conclusion

Check out the project's [GitHub repo](https://github.com/n3wt0n/AzureWebAppSSLManager), try it out and let me know what you think!

Remember to __star the repo__ and follow me on GitHub as well.

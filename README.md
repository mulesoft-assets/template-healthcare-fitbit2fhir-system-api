# Template Healthcare Fitbit to FHIR System API

+ [License Agreement](#licenseagreement)
+ [Use Case](#usecase)
+ [Considerations](#considerations)
	* [Cloudhub security considerations](#cloudhubsecurityconsiderations)
	* [APIs security considerations](#apissecurityconsiderations)
+ [Run it!](#runit)
	* [Running on premise](#runonopremise)
	* [Running on Studio](#runonstudio)
	* [Running on Mule ESB stand alone](#runonmuleesbstandalone)
	* [Running on CloudHub](#runoncloudhub)
	* [Deploying your Anypoint Template on CloudHub](#deployingyouranypointtemplateoncloudhub)
	* [Creating externally reachable proxy and applying policies](#proxy)
	* [Properties to be configured (With examples)](#propertiestobeconfigured)

# License Agreement <a name="licenseagreement"/>
Note that using this template is subject to the conditions of this [License Agreement](AnypointTemplateLicense.pdf).
Please review the terms of the license before downloading and using this template. In short, you are allowed to use the template for free with Mule ESB Enterprise Edition, CloudHub, or as a trial in Anypoint Studio.

# Use Case <a name="usecase"/>

As a FitBit user I want a microservice to access data from the FitBit system and transform them to FHIR standard.

Healthcare Fitbit to FHIR System API is part of the Healthcare Templates Solution. This template calls FitBit API to a day to retrieve required data from the FitBit system and transforms them to JSON following the FHIR specification [version 1.0.2 DSTU2](https://www.hl7.org/FHIR/DSTU2/index.html).

# Considerations <a name="considerations"/>

To make this Anypoint Template run, there are certain preconditions that must be considered. **Failling to do so could lead to unexpected behavior of the template.**
Use Anypoint Studio v6.1.0+ and Mule ESB 3.8.1+ to run this template.

### Register your Fitbit Application

Firstly you need to create a new developer app at http://dev.fitbit.com/ as  the OAuth 2.0 Application Type “Server”. Note that you will need to define the Callback URL too. This is important as you would need to already plan your CloudHub domain (assuming you’re using CloudHub as the target platform). The Callback (Redirect) URI should be as following:

	http://your.domain.cloudhub.io/fitbit/callback

Key parameters to note once you’ve registered your app is the OAuth 2.0 Client ID, the Client (Consumer) Secret and the Redirect URI.

### Running the application

Fitbit’s OAuth login has to be initiated from a web-browser.
http://<your-app-domain>.cloudhub.io/Patient/{id}/authorize would get you to the login landing page where you will fill in your email and password. {id} represents Patient ID, which wants to authorize to Fitbit account.

# Run it! <a name="runit"/>
Simple steps to get Healthcare Healthcare Fitbit to FHIR System API running.
See below.

## Running on premise <a name="runonopremise"/>
In this section we detail the way you should run your Anypoint Template on your computer.

### Where to Download Mule Studio and Mule ESB
First thing to know if you are a newcomer to Mule is where to get the tools.

+ You can download Anypoint Studio from this [Location](http://www.mulesoft.com/platform/studio)
+ You can download Mule ESB from this [Location](http://www.mulesoft.com/platform/soa/mule-esb-open-source-esb)

### Importing an Anypoint Template into Studio
Anypoint Studio offers several ways to import a project into the workspace, for instance: 

+ Anypoint Studio generated Deployable Archive (.zip)
+ Anypoint Studio Project from External Location
+ Maven-based Mule Project from pom.xml
+ Mule ESB Configuration XML from External Location

You can find a detailed description on how to do so in this [Documentation Page](https://docs.mulesoft.com/anypoint-studio/v/6/importing-and-exporting-in-studio).

### Running on Studio <a name="runonstudio"/>
Once you have imported you Anypoint Template into Anypoint Studio you need to follow these steps to run it:

+ Generate keystore and set up the truststore (You can find a detailed description on how to do so in this [Documentation Page](https://docs.mulesoft.com/mule-user-guide/v/3.7/tls-configuration#generating-keystores-and-truststores))
+ Locate the properties file `mule.dev.properties`, in src/main/resources
+ Complete all the properties required as per the examples in the section [Properties to be configured](#propertiestobeconfigured)
+ Once that is done, right click on you Anypoint Template project folder 
+ Hover you mouse over `"Run as"`
+ Click on  `"Mule Application"`

### Running on Mule ESB stand alone <a name="runonmuleesbstandalone"/>
Fill in all the properties in one of the property files, for example in [mule.prod.properties](../master/src/main/resources/mule.prod.properties) and run your app with the corresponding environment variable to use it. To follow the example, this will be `mule.env=prod`.

## Running on CloudHub <a name="runoncloudhub"/>
While [creating your application on CloudHub](https://docs.mulesoft.com/runtime-manager/hello-world-on-cloudhub) (Or you can do it later as a next step), you need to go to `"Manage Application"` > `"Properties"` to set all environment variables detailed in **Properties to be configured**.
Follow other steps defined [here](#runonpremise) and once your app is all set and started, there is no need to do anything else.

### Deploying your Anypoint Template on CloudHub <a name="deployingyouranypointtemplateoncloudhub"/>
Anypoint Studio provides you with really easy way to deploy your Template directly to CloudHub, for the specific steps to do so please check this [link](https://docs.mulesoft.com/mule-fundamentals/v/3.8/deploying-mule-applications#deploy-to-the-anypoint-platform)

## Properties to be configured (With examples) <a name="propertiestobeconfigured"/>
In order to use this Mule Anypoint Template you need to configure properties (Credentials, configurations, URLs etc.) either in properties file or in CloudHub as Environment Variables. Detail list with examples:
### Application properties

+ https.port `8081`
+ token.refresh.poll.frequencyMinutes `30`
+ token.refresh.poll.startDelayMinutes `2`

+ fitbit.host `http://your.domain.cloudhub.io`
+ system-api.host `ehr-system-api.cloudhub.io`
+ system-api.basePath `/api`
+ system-api.port `80`
+ keystore.location= `keystore.jks`
+ keystore.password= `mule1234`
+ key.password= `mule1234`
+ key.alias= `1`

+ baseUri= `baseUri.of.your.app/api`

	**Note:** You should encode the redirect URI.
+ fitbit.redirect.uri= `redirect.uri.defined.also.on.fitbit.side`
+ fitbit.client.id= `12345`
+ fitbit.client.secret= `fsd5fd45fs5d4f45sdf5d`

+ api.version `api_version`
+ api.name `api_name`
+ api.id `api_id`

+ anypoint.platform.client_id `anypoint_platform_client_id`
+ anypoint.platform.client_secret `anypoint_platform_client_secret`
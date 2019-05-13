# Template Healthcare Fitbit to FHIR System API

System APIs abstract away the complexity of core systems of record from end user data, while providing downstream insulation from any interface changes or rationalization of those systems. This API provides an implementation best practice to expose fitness data via a set of RESTful FHIR services in RAML, making it easy to consume within an enterprise.

![](https://www.lucidchart.com/publicSegments/view/6c0eab9d-b684-43bd-96c5-61b323fd6399/image.png)

## Accelerator for Healthcare
This FHIR implementation is one of many components included in [Accelerator for Healthcare](/exchange/68ef9520-24e9-4cf2-b2f5-620025690913/catalyst-accelerator-for-healthcare/). This API provides organizations with connectivity assets that accelerate project delivery in healthcare, including pre-built API designs and implementations that support core healthcare business processes. Contact [info@mulesoft.com](mailto:info@mulesoft.com) for more information.

# License Agreement

This template is subject to the conditions of the <a href="https://s3.amazonaws.com/templates-examples/AnypointTemplateLicense.pdf">MuleSoft License Agreement</a>. Review the terms of the license before downloading and using this template. You can use this template for free with the Mule Enterprise Edition, CloudHub, or as a trial in Anypoint Studio. 

# Use Case

As a FitBit user I want a microservice to access data from the FitBit system and transform the data to the FHIR standard.

Healthcare Fitbit to FHIR System API is part of the Healthcare Templates Solution. This template calls FitBit API to retrieve required data from the FitBit system and transforms them to JSON following the FHIR specification [version 3.0.1 STU3](https://www.hl7.org/FHIR/index.html).

# Considerations

To make this Anypoint Template run, there are certain preconditions that must be considered. Failing to do so can lead to unexpected behavior of the template.

Use Anypoint Studio v7.1.4 and later and Mule Runtime 4.1.1 and later to run this template.

### Register your Fitbit Application

Create a new developer app at http://dev.fitbit.com/ with the OAuth 2.0 Application Type “Server”. Note that you need to define the Callback URL too. This is important as you would need to set this URL in property `fitbit.redirect.uri`.

Key parameters to note once you’ve registered your app is the OAuth 2.0 Client ID, the Client (Consumer) Secret, and the Redirect URI.

### Run the Application

Access the Fitbit OAuth login from a web browser at:
 
https://www.fitbit.com/oauth2/authorize?response_type=code&client_id=YOUR_CLIENT_ID&redirect_uri=YOUR_REDIRECT_URI&scope=activity%20profile%20settings%20sleep%20weight&prompt=login.

This gets you to the login landing page where you fill in your email and password. After the successful log in you are redirected to the URL specified in the app at http://dev.fitbit.com/. You can notice the access code in the URL.

To register a patient to this Fitbit account you need to do create the request `GET https://<your-app-domain>.cloudhub.io/Patient/{id}/register?code=<your-access-code>` where {id} represents the Patient ID, who wants to authorize to Fitbit account and access code is the one obtained after login with Fitbit credentials.

# Run it! 

Simple steps to get Healthcare Fitbit to FHIR System API running.

### Where to Download Anypoint Studio and the Mule Runtime

If you are new to Mule, download this software:

- [Download Anypoint Studio](https://www.mulesoft.com/platform/studio)
- [Download Mule runtime](https://www.mulesoft.com/lp/dl/mule-esb-enterprise)

**Note:** Anypoint Studio requires JDK 8.

### Import into Studio

In Studio, click the Exchange X icon in the upper left of the taskbar, log in with your Anypoint Platform credentials, search for the template, and click Open.

### Run in Studio

After you import the Template into Anypoint Studio, to follow these steps to run it:

1. Generate a keystore and set up the truststore (you can find a detailed description on how to do so in [TLS Configuration](https://docs.mulesoft.com/mule-runtime/4.2/tls-configuration#keystores-and-truststores)).
2. Locate the properties file `mule.dev.properties`, in src/main/resources.
3. Complete all the properties required as per the examples in "Properties to Configure".
4. Right click your template project folder.
6. Hover your mouse over Run As.
6. Click Mule Application.

### Run Stand Alone

Fill in all the properties in one of the property files, for example in mule.prod.properties and run your app with the corresponding environment variable to use it. To follow the example, use `mule.env=prod`.

## Run on CloudHub

When creating your application in CloudHub, you need to go to Manage Application > Properties to set all environment variables detailed in the "Properties to Configure" section.

### Deploy on CloudHub

In Studio, right click your project name in Package Explorer and select Anypoint Platform > Deploy on CloudHub.

## Properties to Configure

To use this template you need to configure properties either in a properties file or in CloudHub as Environment Variables. To run the MUnit tests, the configuration file is located in the mule.test.properties.

### Application Properties

- https.port `8082`
- token.refresh.poll.frequencyMinutes `30`
- token.refresh.poll.startDelayMinutes `2`

- keystore.location `keystore.jks`
- keystore.password `password1234`
- key.password `password1234`
- key.alias `alias`

- baseUri `baseUri.of.your.app/api/`

	**Note:** You should encode the fitbit.redirect.uri
	
- api.fitbit.host `api.fitbit.com`
- fitbit.redirect.uri `redirect.uri.defined.also.on.fitbit.side`
- fitbit.client.id `12345`
- fitbit.client.secret `fsd5fd45fs5d4f45sdf5d`

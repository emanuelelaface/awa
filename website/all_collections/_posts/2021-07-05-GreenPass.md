---

layout: post
title: Green Pass
subtitle: COVID-19 Digital Green Pass for iPhone and Apple Watch
date: 2020-10-31
tag: covid-19 green pass
categories: ["category", "subcategory"]
---

Since the beginning of July 2021 European Union adopted a Digital Green Pass to facilitate the movement of people within the Union during the pandemia. However many countries are issuing the Pass as PDF to print, and even who is using a dedicated app does not provide any Apple Watch companion to display the code from the wrist.

Because the standard of the Green Pass is open, I decided to write an app to handle it.

# Digital Green Pass

The European Union releases the Digital Green Pass as QR Code that contains mainly 3 information:

- The date of validity of the pass;
- The basic data of the owner of the pass;
- A description of the kind of pass.

This last information can go under 3 categories: the pass can be generated after a vaccine, after a recovery or after a test, the test can be the rapid or the PCR. These data are packed in a CBOR structure (that is like JSON but binary), gzip compressed and then encoded with Base45. The final result is a string that is converted in a QR Code.

The structure of the data is described on the [EU Portal](https://ec.europa.eu/health/sites/default/files/ehealth/docs/covid-certificate_json_specification_en.pdf) and expanded in the many examples of the [Git Repository](https://github.com/ehn-dcc-development/hcert-spec/blob/main/README.md) and for the protocol my starting point was the excellent [work of Tobias Girstmair](https://gir.st/blog/greenpass.html) where he also shows a good [link](https://dgc.a-sit.at/ehn/) to generates the different kind of Green Pass. 

Then the app is simply a QR Code scanner that decodes the data, verify the signature and display everything to the user.

The verification of the signature requires the public key of the issuer in order to check if the encryption was done with the proper private key. These keys are available only for the members of the Digital COVID-19 Certificate Gateway that, at the moment, does not have a public access so I cannot access it. Luckily, the Netherland Healthcare Authority has a public API that distributes a subset of the available public keys without restrictions, so I am using that [repository](https://verifier-api.coronacheck.nl/v4/verifier/public_keys). If DCCG will decide to open the API to external people, I will implement it in a future version of the app.

The source code of the app is available [here](https://github.com/emanuelelaface/GreenPass). Since it uses several JSON files to decode the codes of the various item in the pass (like the kind of vaccine, the laboratory of the test the manufacturer of the test etc.) I created a Python script  to collect these different files. The files must be included in the source tree of the app because the conversions are done offline to prevent the app to get stuck if the Internet connection is not available (and to prevent MITM attacks, especially for the file of the keys).

<img src="/assets/img/green-pass-01.png"  width="300"/> <img src="/assets/img/green-pass-02.png"  width="300"/>



<img src="/assets/img/green-pass-03.png"  width="200"/> <img src="/assets/img/green-pass-04.png"  width="200"/> <img src="/assets/img/green-pass-05.png"  width="200"/>



## Privacy

Apple requires a privacy disclaimer to submit applications to their store, so this is the one for Digital Green Pass.

The app saves the data contained in the Green Pass directly on the iPhone or the Apple Watch, it never send any data to anyone, it does not communicate with any server.

No data is shared with anyone for profiling, advertisements, marketing or any other service.

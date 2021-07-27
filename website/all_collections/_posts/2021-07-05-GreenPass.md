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

The structure of the data is described on the [EU Portal](https://ec.europa.eu/health/sites/default/files/ehealth/docs/covid-certificate_json_specification_en.pdf), and for the protocol my starting point was the excellent [work of Tobias Girstmair](https://gir.st/blog/greenpass.html) where he also shows a good [link](https://dgc.a-sit.at/ehn/) to generates the different kind of Green Pass. 

Then the app is simply a QR Code scanner that decodes the data and display them to the user.

![Screenshot Green Pass iPhone 1](/assets/img/green-pass-01.png) ![Screenshot Green Pass iPhone 2](/assets/img/green-pass-02.png)

![Screenshot Green Pass AW 1](/assets/img/green-pass-03.png) ![Screenshot Green Pass AW 2](/assets/img/green-pass-04.png) ![Screenshot Green Pass AW 3](/assets/img/green-pass-05.png)

## Privacy

Apple requires a privacy disclaimer to submit applications to their store, so this is the one for Digital Green Pass.

The app saves the data contained in the Green Pass directly on the iPhone or the Apple Watch, it never send any data to anyone, it does not communicate with any server.

No data is shared with anyone for profiling, advertisements, marketing or any other service.

---
title: aaaHow tooConfigure TLS wederzijdse verificatie voor Web-App
description: Meer informatie over hoe tooconfigure uw web-app toouse clientcertificaat verificatie op TLS.
services: app-service
documentationcenter: 
author: naziml
manager: erikre
editor: jimbe
ms.assetid: cd1d15d3-2d9e-4502-9f11-a306dac4453a
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/08/2016
ms.author: naziml
ms.openlocfilehash: 8aeb9b35058fac50b8b38f6428207ad4a82d8637
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-tls-mutual-authentication-for-web-app"></a>Hoe tooConfigure TLS wederzijdse verificatie voor Web-App
## <a name="overview"></a>Overzicht
U kunt access tooyour Azure-web-app beperken door verschillende soorten verificatie voor het inschakelen. Eenzijdige toodo is daarom tooauthenticate met een clientcertificaat als Hallo-aanvraag via TLS/SSL. Dit mechanisme wordt TLS wederzijdse verificatie of verificatie van clientcertificaten genoemd en dit artikel wordt beschreven hoe toosetup uw web-app toouse verificatie van clientcertificaten.

> **Opmerking:** als u toegang uw site via HTTP en niet HTTPS tot, ontvangt u geen een clientcertificaat. Dus als uw toepassing clientcertificaten vereist moet u niet toestaan aanvragen tooyour toepassing via HTTP.
> 
> 

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="configure-web-app-for-client-certificate-authentication"></a>Web-App configureren voor verificatie van clientcertificaten
toosetup uw web-app toorequire clientcertificaten moet u tooadd Hallo clientCertEnabled site instellen voor uw web-app en stel deze tootrue. Deze instelling is momenteel niet beschikbaar via Hallo beheerervaring in Hallo Portal en Hallo REST-API moet tooaccomplish toobe gebruikt dit.

Kunt u Hallo [ARMClient hulpprogramma](https://github.com/projectkudu/ARMClient) toomake het eenvoudig toocraft Hallo REST API-aanroep. Nadat u met Hallo hulpprogramma aanmelden, moet u tooissue Hallo volgende opdracht:

    ARMClient PUT subscriptions/{Subscription Id}/resourcegroups/{Resource Group Name}/providers/Microsoft.Web/sites/{Website Name}?api-version=2015-04-01 @enableclientcert.json -verbose

Alles in {} worden vervangen door de gegevens voor uw web-app en het maken van een bestand met de naam enableclientcert.json Hello volgende JSON-inhoud:

    {
        "location": "My Web App Location",
        "properties": {
            "clientCertEnabled": true
        }
    }

Zorg ervoor dat toochange Hallo-waarde van 'locatie' toowherever die uw web-app is bijvoorbeeld Noordelijk Centraal, VS of West VS enzovoort.

U kunt ook https://resources.azure.com tooflip hello `clientCertEnabled` eigenschap te`true`.

> **Opmerking:** als u ARMClient vanuit Powershell uitvoert, moet u tooescape Hallo @-teken voor JSON-bestand met een back-maatstreepjes Hallo ".
> 
> 

## <a name="accessing-hello-client-certificate-from-your-web-app"></a>Toegang tot Hallo Client certificaat van uw Web-App
Als u gebruik van ASP.NET en configureren van uw app toouse-verificatie van clientcertificaten, Hallo-certificaat is beschikbaar via Hallo **HttpRequest.ClientCertificate** eigenschap. Voor andere stacks toepassing zijn hello client cert beschikbaar in uw app via een base64-gecodeerde waarde in de aanvraagheader van Hallo 'X ARR ClientCert'. Uw toepassing kunt maken van een certificaat via deze waarde en vervolgens worden gebruikt voor verificatie en autorisatie doeleinden in uw toepassing.

## <a name="special-considerations-for-certificate-validation"></a>Speciale overwegingen voor validatie van het servercertificaat
Hallo-clientcertificaat dat wordt verzonden toohello toepassing via niet een validatie door hello Azure Web Apps platform. Dit certificaat wordt gevalideerd, is de verantwoordelijkheid van de Hallo van Hallo web-app. Hier volgt een voorbeeld ASP.NET-code te valideren en eigenschappen voor certificaat voor verificatie.

    using System;
    using System.Collections.Specialized;
    using System.Security.Cryptography.X509Certificates;
    using System.Web;

    namespace ClientCertificateUsageSample
    {
        public partial class cert : System.Web.UI.Page
        {
            public string certHeader = "";
            public string errorString = "";
            private X509Certificate2 certificate = null;
            public string certThumbprint = "";
            public string certSubject = "";
            public string certIssuer = "";
            public string certSignatureAlg = "";
            public string certIssueDate = "";
            public string certExpiryDate = "";
            public bool isValidCert = false;

            //
            // Read hello certificate from hello header into an X509Certificate2 object
            // Display properties of hello certificate on hello page
            //
            protected void Page_Load(object sender, EventArgs e)
            {
                NameValueCollection headers = base.Request.Headers;
                certHeader = headers["X-ARR-ClientCert"];
                if (!String.IsNullOrEmpty(certHeader))
                {
                    try
                    {
                        byte[] clientCertBytes = Convert.FromBase64String(certHeader);
                        certificate = new X509Certificate2(clientCertBytes);
                        certSubject = certificate.Subject;
                        certIssuer = certificate.Issuer;
                        certThumbprint = certificate.Thumbprint;
                        certSignatureAlg = certificate.SignatureAlgorithm.FriendlyName;
                        certIssueDate = certificate.NotBefore.ToShortDateString() + " " + certificate.NotBefore.ToShortTimeString();
                        certExpiryDate = certificate.NotAfter.ToShortDateString() + " " + certificate.NotAfter.ToShortTimeString();
                    }
                    catch (Exception ex)
                    {
                        errorString = ex.ToString();
                    }
                    finally 
                    {
                        isValidCert = IsValidClientCertificate();
                        if (!isValidCert) Response.StatusCode = 403;
                        else Response.StatusCode = 200;
                    }
                }
                else
                {
                    certHeader = "";
                }
            }

            //
            // This is a SAMPLE verification routine. Depending on your application logic and security requirements, 
            // you should modify this method
            //
            private bool IsValidClientCertificate()
            {
                // In this example we will only accept hello certificate as a valid certificate if all hello conditions below are met:
                // 1. hello certificate is not expired and is active for hello current time on server.
                // 2. hello subject name of hello certificate has hello common name nildevecc
                // 3. hello issuer name of hello certificate has hello common name nildevecc and organization name Microsoft Corp
                // 4. hello thumbprint of hello certificate is 30757A2E831977D8BD9C8496E4C99AB26CB9622B
                //
                // This example does NOT test that this certificate is chained tooa Trusted Root Authority (or revoked) on hello server 
                // and it allows for self signed certificates
                //

                if (certificate == null || !String.IsNullOrEmpty(errorString)) return false;

                // 1. Check time validity of certificate
                if (DateTime.Compare(DateTime.Now, certificate.NotBefore) < 0 || DateTime.Compare(DateTime.Now, certificate.NotAfter) > 0) return false;

                // 2. Check subject name of certificate
                bool foundSubject = false;
                string[] certSubjectData = certificate.Subject.Split(new char[] { ',' }, StringSplitOptions.RemoveEmptyEntries);
                foreach (string s in certSubjectData)
                {
                    if (String.Compare(s.Trim(), "CN=nildevecc") == 0)
                    {
                        foundSubject = true;
                        break;
                    }
                }
                if (!foundSubject) return false;

                // 3. Check issuer name of certificate
                bool foundIssuerCN = false, foundIssuerO = false;
                string[] certIssuerData = certificate.Issuer.Split(new char[] { ',' }, StringSplitOptions.RemoveEmptyEntries);
                foreach (string s in certIssuerData)
                {
                    if (String.Compare(s.Trim(), "CN=nildevecc") == 0)
                    {
                        foundIssuerCN = true;
                        if (foundIssuerO) break;
                    }

                    if (String.Compare(s.Trim(), "O=Microsoft Corp") == 0)
                    {
                        foundIssuerO = true;
                        if (foundIssuerCN) break;
                    }
                }

                if (!foundIssuerCN || !foundIssuerO) return false;

                // 4. Check thumprint of certificate
                if (String.Compare(certificate.Thumbprint.Trim().ToUpper(), "30757A2E831977D8BD9C8496E4C99AB26CB9622B") != 0) return false;

                // If you also want tootest if hello certificate chains tooa Trusted Root Authority you can uncomment hello code below
                //
                //X509Chain certChain = new X509Chain();
                //certChain.Build(certificate);
                //bool isValidCertChain = true;
                //foreach (X509ChainElement chElement in certChain.ChainElements)
                //{
                //    if (!chElement.Certificate.Verify())
                //    {
                //        isValidCertChain = false;
                //        break;
                //    }
                //}
                //if (!isValidCertChain) return false;

                return true;
            }
        }
    }

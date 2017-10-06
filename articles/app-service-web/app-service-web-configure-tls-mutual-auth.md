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
# <a name="how-tooconfigure-tls-mutual-authentication-for-web-app"></a><span data-ttu-id="e6201-103">Hoe tooConfigure TLS wederzijdse verificatie voor Web-App</span><span class="sxs-lookup"><span data-stu-id="e6201-103">How tooConfigure TLS Mutual Authentication for Web App</span></span>
## <a name="overview"></a><span data-ttu-id="e6201-104">Overzicht</span><span class="sxs-lookup"><span data-stu-id="e6201-104">Overview</span></span>
<span data-ttu-id="e6201-105">U kunt access tooyour Azure-web-app beperken door verschillende soorten verificatie voor het inschakelen.</span><span class="sxs-lookup"><span data-stu-id="e6201-105">You can restrict access tooyour Azure web app by enabling different types of authentication for it.</span></span> <span data-ttu-id="e6201-106">Eenzijdige toodo is daarom tooauthenticate met een clientcertificaat als Hallo-aanvraag via TLS/SSL.</span><span class="sxs-lookup"><span data-stu-id="e6201-106">One way toodo so is tooauthenticate using a client certificate when hello request is over TLS/SSL.</span></span> <span data-ttu-id="e6201-107">Dit mechanisme wordt TLS wederzijdse verificatie of verificatie van clientcertificaten genoemd en dit artikel wordt beschreven hoe toosetup uw web-app toouse verificatie van clientcertificaten.</span><span class="sxs-lookup"><span data-stu-id="e6201-107">This mechanism is called TLS mutual authentication or client certificate authentication and this article will detail how toosetup your web app toouse client certificate authentication.</span></span>

> <span data-ttu-id="e6201-108">**Opmerking:** als u toegang uw site via HTTP en niet HTTPS tot, ontvangt u geen een clientcertificaat.</span><span class="sxs-lookup"><span data-stu-id="e6201-108">**Note:** If you access your site over HTTP and not HTTPS, you will not receive any client certificate.</span></span> <span data-ttu-id="e6201-109">Dus als uw toepassing clientcertificaten vereist moet u niet toestaan aanvragen tooyour toepassing via HTTP.</span><span class="sxs-lookup"><span data-stu-id="e6201-109">So if your application requires client certificates you should not allow requests tooyour application over HTTP.</span></span>
> 
> 

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="configure-web-app-for-client-certificate-authentication"></a><span data-ttu-id="e6201-110">Web-App configureren voor verificatie van clientcertificaten</span><span class="sxs-lookup"><span data-stu-id="e6201-110">Configure Web App for Client Certificate Authentication</span></span>
<span data-ttu-id="e6201-111">toosetup uw web-app toorequire clientcertificaten moet u tooadd Hallo clientCertEnabled site instellen voor uw web-app en stel deze tootrue.</span><span class="sxs-lookup"><span data-stu-id="e6201-111">toosetup your web app toorequire client certificates you need tooadd hello clientCertEnabled site setting for your web app and set it tootrue.</span></span> <span data-ttu-id="e6201-112">Deze instelling is momenteel niet beschikbaar via Hallo beheerervaring in Hallo Portal en Hallo REST-API moet tooaccomplish toobe gebruikt dit.</span><span class="sxs-lookup"><span data-stu-id="e6201-112">This setting is not currently available through hello management experience in hello Portal, and hello REST API will need toobe used tooaccomplish this.</span></span>

<span data-ttu-id="e6201-113">Kunt u Hallo [ARMClient hulpprogramma](https://github.com/projectkudu/ARMClient) toomake het eenvoudig toocraft Hallo REST API-aanroep.</span><span class="sxs-lookup"><span data-stu-id="e6201-113">You can use hello [ARMClient tool](https://github.com/projectkudu/ARMClient) toomake it easy toocraft hello REST API call.</span></span> <span data-ttu-id="e6201-114">Nadat u met Hallo hulpprogramma aanmelden, moet u tooissue Hallo volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="e6201-114">After you log in with hello tool you will need tooissue hello following command:</span></span>

    ARMClient PUT subscriptions/{Subscription Id}/resourcegroups/{Resource Group Name}/providers/Microsoft.Web/sites/{Website Name}?api-version=2015-04-01 @enableclientcert.json -verbose

<span data-ttu-id="e6201-115">Alles in {} worden vervangen door de gegevens voor uw web-app en het maken van een bestand met de naam enableclientcert.json Hello volgende JSON-inhoud:</span><span class="sxs-lookup"><span data-stu-id="e6201-115">replacing everything in {} with information for your web app and creating a file called enableclientcert.json with hello following JSON content:</span></span>

    {
        "location": "My Web App Location",
        "properties": {
            "clientCertEnabled": true
        }
    }

<span data-ttu-id="e6201-116">Zorg ervoor dat toochange Hallo-waarde van 'locatie' toowherever die uw web-app is bijvoorbeeld Noordelijk Centraal, VS of West VS enzovoort.</span><span class="sxs-lookup"><span data-stu-id="e6201-116">Make sure toochange hello value of "location" toowherever your web app is located e.g. North Central US or West US etc.</span></span>

<span data-ttu-id="e6201-117">U kunt ook https://resources.azure.com tooflip hello `clientCertEnabled` eigenschap te`true`.</span><span class="sxs-lookup"><span data-stu-id="e6201-117">You can also use https://resources.azure.com tooflip hello `clientCertEnabled` property too`true`.</span></span>

> <span data-ttu-id="e6201-118">**Opmerking:** als u ARMClient vanuit Powershell uitvoert, moet u tooescape Hallo @-teken voor JSON-bestand met een back-maatstreepjes Hallo ".</span><span class="sxs-lookup"><span data-stu-id="e6201-118">**Note:** If you run ARMClient from Powershell, you will need tooescape hello @ symbol for hello JSON file with a back tick \`.</span></span>
> 
> 

## <a name="accessing-hello-client-certificate-from-your-web-app"></a><span data-ttu-id="e6201-119">Toegang tot Hallo Client certificaat van uw Web-App</span><span class="sxs-lookup"><span data-stu-id="e6201-119">Accessing hello Client Certificate From Your Web App</span></span>
<span data-ttu-id="e6201-120">Als u gebruik van ASP.NET en configureren van uw app toouse-verificatie van clientcertificaten, Hallo-certificaat is beschikbaar via Hallo **HttpRequest.ClientCertificate** eigenschap.</span><span class="sxs-lookup"><span data-stu-id="e6201-120">If you are using ASP.NET and configure your app toouse client certificate authentication, hello certificate will be available through hello **HttpRequest.ClientCertificate** property.</span></span> <span data-ttu-id="e6201-121">Voor andere stacks toepassing zijn hello client cert beschikbaar in uw app via een base64-gecodeerde waarde in de aanvraagheader van Hallo 'X ARR ClientCert'.</span><span class="sxs-lookup"><span data-stu-id="e6201-121">For other application stacks, hello client cert will be available in your app through a base64 encoded value in hello "X-ARR-ClientCert" request header.</span></span> <span data-ttu-id="e6201-122">Uw toepassing kunt maken van een certificaat via deze waarde en vervolgens worden gebruikt voor verificatie en autorisatie doeleinden in uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="e6201-122">Your application can create a certificate from this value and then use it for authentication and authorization purposes in your application.</span></span>

## <a name="special-considerations-for-certificate-validation"></a><span data-ttu-id="e6201-123">Speciale overwegingen voor validatie van het servercertificaat</span><span class="sxs-lookup"><span data-stu-id="e6201-123">Special Considerations for Certificate Validation</span></span>
<span data-ttu-id="e6201-124">Hallo-clientcertificaat dat wordt verzonden toohello toepassing via niet een validatie door hello Azure Web Apps platform.</span><span class="sxs-lookup"><span data-stu-id="e6201-124">hello client certificate that is sent toohello application does not go through any validation by hello Azure Web Apps platform.</span></span> <span data-ttu-id="e6201-125">Dit certificaat wordt gevalideerd, is de verantwoordelijkheid van de Hallo van Hallo web-app.</span><span class="sxs-lookup"><span data-stu-id="e6201-125">Validating this certificate is hello responsibility of hello web app.</span></span> <span data-ttu-id="e6201-126">Hier volgt een voorbeeld ASP.NET-code te valideren en eigenschappen voor certificaat voor verificatie.</span><span class="sxs-lookup"><span data-stu-id="e6201-126">Here is sample ASP.NET code that validates certificate properties for authentication purposes.</span></span>

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

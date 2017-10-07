---
title: aaaHow toofill specifieke velden voor een toepassing ontwikkelde aangepaste | Microsoft Docs
description: Richtlijnen op hoe toofill uit specifieke als velden u een aangepaste toepassing ontwikkelde registreert met Azure AD
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.openlocfilehash: 7e07bc45c58542edb3863db5aad7c845f1a1772e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toofill-out-specific-fields-for-a-custom-developed-application"></a>Hoe toofill specifieke velden voor een toepassing ontwikkelde aangepaste

In dit artikel geeft u een korte beschrijving van alle Hallo beschikbare velden in Hallo toepassing registratieformulier in Hallo [Azure-portal](https://portal.azure.com).

## <a name="register-a-new-application"></a>Een nieuwe toepassing registreren

-   een nieuwe toepassing tooregister navigeren toohello [Azure-portal](https://portal.azure.com).

-   Hallo navigatiedeelvenster links Klik **Azure Active Directory.**

-   Kies **App registraties** en klik op **toevoegen**.

-   Deze open up registratieformulier Hallo-toepassing.

## <a name="fields-in-hello-application-registration-form"></a>Velden in registratieformulier Hallo-toepassing


| Veld            | Beschrijving                                                                              |
|------------------|------------------------------------------------------------------------------------------|
| Naam             | Hallo-naam van de toepassing hello. Er moet ten minste vier tekens.                |
| Toepassingstype | **Web-app of Web API**: een toepassing die staat voor een webtoepassing, een web-API of beide 
| |**Systeemeigen**: een toepassing die op het apparaat of de computer van een gebruiker kan worden geïnstalleerd           |
| Aanmeldings-URL      | waar gebruikers zich in toouse uw toepassing aanmelden kunnen Hello-URL                                  |

Zodra u Hallo boven velden hebt ingevuld, Hallo toepassing worden geregistreerd in hello Azure-portal en u omgeleid toohello toepassingspagina. Hallo **instellingen** knop op Hallo Toepassingsdeelvenster wordt geopend de instellingenpagina hello, waarvoor meer velden voor u toocustomize uw toepassing. Hallo in de volgende tabel beschrijft alle Hallo velden op de pagina instellingen Hallo. Houd er rekening mee dat u alleen een subset van deze velden ziet, afhankelijk van of u een webtoepassing of een systeemeigen toepassing gemaakt.

| Veld           | Beschrijving                                                                                                                                                                                                                                                                                                     |
|-----------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Toepassings-id  | Wanneer u een toepassing registreert, wijst Azure AD uw toepassing een toepassing. Hallo toepassings-ID kan worden gebruikt toouniquely identificeren in uw toepassing in verificatie aanvragen tooAzure AD, evenals tooaccess resources zoals Hallo Graph API.                                                          |
| App-ID-URI      | Dit moet een unieke URI, meestal van Hallo formulier **https://&lt;tenant\_naam&gt;/&lt;toepassing\_naam&gt;.** Dit wordt gebruikt tijdens het Hallo authorization grant stroom als unieke id toospecify Hallo resource welke Hallo token moet worden verleend voor. Ook wordt het Hallo 'aud' claim in de toegangstoken Hallo uitgegeven. |
| Nieuw logo uploaden | U kunt deze tooupload een logo gebruiken voor uw toepassing. Hallo-logo moet bmp-, JPG of PNG-indeling en Hallo bestandsgrootte moet minder dan 100KB. Hallo-dimensies voor Hallo installatiekopie moet 215 x 215 pixels, met de afmetingen van de centrale afbeelding van 94 x 94 pixels.                                                       |
| URL van de startpagina   | Dit is Hallo aanmeldings-URL opgegeven tijdens de registratie van toepassing.                                                                                                                                                                                                                                              |
| URL voor afmelden      | Deze Hallo één afmelden afmelding URL. Azure AD verzendt een afmelding aanvraag toothis-URL als Hallo gebruiker hun sessie wist met Azure AD met behulp van andere geregistreerde toepassing.                                                                                                                                       |
| Multi-verpachte  | Deze schakeloptie geeft aan of de toepassing hello kan worden gebruikt door meerdere tenants. Dit betekent doorgaans dat uw toepassing in externe organisaties kunnen worden gebruikt door het registreren van deze in de tenant en het verlenen van toegang tootheir organisatie gegevens.                                                                   |
| Antwoord-URL 's      | Hallo antwoord-URL's zijn Hallo eindpunten waarop Azure AD tokens retourneert die door uw toepassing worden aangevraagd.                                                                                                                                                                                                          |
| Omleidings-URI 's   | Dit is waar Hallo gebruiker worden verzonden toofollowing geslaagde autorisatie voor systeemeigen toepassingen. Azure AD-Controleer of de Hallo omleidings-URI die uw toepassing wordt voorzien in Hallo OAuth 2.0 aanvraag overeenkomt met waarden in de portal Hallo Hallo geregistreerd.                                                            |
| Sleutels            | U kunt sleutels tooprogrammatically toegang tot web-API's die zijn beveiligd door Azure AD zonder tussenkomst van de gebruiker maken. Van Hallo \* \*sleutels\* \* pagina, een sleutel beschrijving en Hallo vervaldatum invoeren en toogenerate Hallo sleutel opslaan. Zorg ervoor dat toosave deze ergens beveiligen, zoals tooaccess kunnen niet worden later.             |

## <a name="next-steps"></a>Volgende stappen
[Toepassingen beheren met Azure Active Directory](active-directory-enable-sso-scenario.md)

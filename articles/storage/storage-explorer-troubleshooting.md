---
title: aaaAzure Opslagverkenner probleemoplossingsgids | Microsoft Docs
description: Overzicht van Hallo twee foutopsporingsfunctie van Azure
services: virtual-machines
documentationcenter: 
author: Deland-Han
manager: cshepard
editor: 
ms.assetid: 
ms.service: virtual-machines
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/09/2017
ms.author: delhan
ms.openlocfilehash: 21705629500359222bc566c599f0864ad50036ec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-storage-explorer-troubleshooting-guide"></a>Azure Storage Explorer probleemoplossingsgids

## <a name="introduction"></a>Inleiding

Microsoft Azure Opslagverkenner (Preview) is een zelfstandige app waardoor u tooeasily werken met Azure Storage-gegevens op Windows, Mac OS- en Linux. Hallo-app kunt verbinden toStorage accounts die worden gehost op Azure, soevereine Clouds en Azure-Stack.

Deze handleiding bevat een overzicht van oplossingen voor algemene problemen gezien in Opslagverkenner.

## <a name="sign-in-issues"></a>Problemen met aanmelden

Alleen Azure Active Directory (AAD) accounts worden ondersteund. Als u een AD FS-account gebruikt, is het verwacht dat tooStorage die Explorer niet werkt aanmelden. Voordat u doorgaat, probeer uw toepassing opnieuw te starten en Zie of Hallo problemen kunnen worden opgelost.

### <a name="error-self-signed-certificate-in-certificate-chain"></a>Fout: Zelf-ondertekend certificaat in de certificaatketen

Er zijn diverse redenen waarom u deze fout kan optreden en de meest voorkomende twee redenen Hallo zijn als volgt:

1. Hallo-app is verbonden via een transparante proxy-, wat betekent dat een server (zoals de bedrijfsserver van uw) onderscheppen HTTPS-verkeer, ontsleutelen van deze en vervolgens versleutelen met behulp van een zelfondertekend certificaat.

2. U kunt een toepassing, zoals antivirussoftware, die is injecteren van een zelfondertekend SSL-certificaat in Hallo HTTPS-berichten die u ontvangt worden uitgevoerd.

Wanneer Opslagverkenner Hallo problemen tegenkomt, kan het niet meer te weten of Hallo ontvangen HTTPS-bericht is geknoeid. Als u een kopie van Hallo zelf-ondertekend certificaat hebt, kunt u Opslagverkenner vertrouwen. Als u die is injecteren Hallo certificaat weet, volgt u deze stappen toofind het:

1. Open SSL installeren

    - [Windows](https://slproweb.com/products/Win32OpenSSL.html) (Hallo lichte versies moet voldoende)

    - Mac- en Linux: moet worden opgenomen met het besturingssysteem

2. Open SSL uitvoeren

    - Windows: Hallo-installatiemap openen, klikt u op **/bin/**, en dubbelklik vervolgens op **openssl.exe**.
    - Mac- en Linux: Voer **openssl** van een definitieve.

3. Uitvoeren van s_client - showcerts-microsoft.com:443 verbinding

4. Zoek naar de zelfondertekende certificaten. Als u welke zijn zelf-ondertekend weet, zoek overal Hallo onderwerp ('s:') en verlener ('i') zijn dezelfde Hallo.

5. Wanneer u zelfondertekende certificaten hebt gevonden, voor elk adres kopieert en plakt u alles uit en inclusief **---BEGIN CERTIFICATE---** te**---EINDCERTIFICAAT---** tooa nieuwe cer-bestand.

6. Open Opslagverkenner, klik op **bewerken** > **SSL-certificaten** > **certificaten importeren**, en vervolgens gebruik Hallo bestand objectkiezer toofind, selecteert, en open Hallo cer-bestanden die u hebt gemaakt.

Als u geen zelfondertekende certificaten met behulp van Hallo bovenstaande stappen niet kunt vinden, contact met ons opnemen via Hallo feedbackprogramma voor meer informatie.

### <a name="unable-tooretrieve-subscriptions"></a>Kan geen tooretrieve abonnementen

Als u tooretrieve uw abonnementen na het aanmelden, volg deze stappen tootroubleshoot dit probleem:

- Controleer of uw account toegang toohello abonnementen door aanmeldt bij hello Azure-portal.

- Zorg ervoor dat u bent aangemeld met behulp van de juiste omgeving hello (Azure, Azure China, Duitse Azure, Azure US Government of aangepaste omgeving/Azure Stack).

- Als u zich achter een proxy, zorg er dan voor dat Hallo Opslagverkenner proxy correct geconfigureerd.

- Verwijder en readding Hallo-account.

- Verwijder Hallo volgende bestanden uit de hoofddirectory (dat wil zeggen, C:\Users\ContosoUser) en vervolgens opnieuw toe te voegen Hallo-account:

    - .adalcache

    - .devaccounts

    - .extaccounts

- Console voor controle Hallo developer's (door op F12 te drukken) wanneer u zich aanmeldt voor eventuele foutberichten:

![Hulpprogramma's voor ontwikkelaars](./media/storage-explorer-troubleshooting/4022501_en_2.png)

### <a name="unable-toosee-hello-authentication-page"></a>Kan geen toosee Hallo verificatiepagina

Als u pagina kan niet toosee Hallo-verificatie, volg deze stappen tootroubleshoot dit probleem:

- Afhankelijk van Hallo snelheid van uw verbinding, kan het Hallo-aanmeldingspagina tooload even duren voordat, wacht ten minste één minuut voordat het dialoogvenster verificatie hello wordt gesloten.

- Als u zich achter een proxy, zorg er dan voor dat Hallo Opslagverkenner proxy correct geconfigureerd.

- Weergave Hallo developer-console door Hallo F12-toets te drukken. Hallo-antwoorden van Hallo developer-console te bekijken en zien of voor u een aanwijzing Waarom vindt verificatie werkt niet.

### <a name="cannot-remove-account"></a>Kan account niet verwijderen

Volg deze stappen tootroubleshoot dit probleem als u tooremove een account of Hallo opnieuw verifiëren koppeling heeft geen invloed:

- Verwijder Hallo volgende bestanden uit de hoofddirectory en vervolgens readding Hallo-account:

    - .adalcache

    - .devaccounts

    - .extaccounts

- Als u tooremove SAS Storage-resources die zijn gekoppeld wilt, verwijder Hallo volgende bestanden:

    - De map %AppData%/StorageExplorer voor Windows

    - /Gebruikers/ < Uw_naam >/Library/Applicaiton ondersteuning/StorageExplorer voor Mac

    - ~/.config/StorageExplorer voor Linux

> [!NOTE]
>  U hebt tooreenter alle uw referenties als u deze bestanden verwijdert.

## <a name="proxy-issues"></a>Proxy-problemen

Controleer eerst of die Hallo volgende informatie die u hebt ingevoerd juist zijn:

- proxy-URL en poort Hallo getal

- Gebruikersnaam en wachtwoord, indien vereist door het Hallo-proxy

### <a name="common-solutions"></a>Algemene oplossingen

Als u steeds problemen ondervindt nog, volgt u deze stappen tootroubleshoot ze:

- Als u verbinding van toohello Internet maken kunt zonder gebruik van uw proxyserver, moet u controleren of Opslagverkenner zonder proxyinstellingen zijn ingeschakeld werkt. Als dit Hallo geval is, is er mogelijk een probleem met uw proxy-instellingen. Werken met uw proxy-beheerder tooidentify Hallo problemen.

- Controleer of andere toepassingen die gebruikmaken van de proxyserver Hallo werken zoals verwacht.

- Controleer of u kunt verbinding maken toohello Microsoft Azure-portal met behulp van uw webbrowser

- Controleer of u kunt reacties van uw service-eindpunten te ontvangen. Voer een van de eindpunt-URL's in uw browser. Als u verbinding maken kunt, ontvangt u een InvalidQueryParameterValue of een vergelijkbare XML-antwoord.

- Als iemand anders Opslagverkenner ook met de proxyserver gebruikt, controleert u of dat ze verbinding kunnen maken. Als ze verbinding maken kunnen, hebt u mogelijk toocontact uw proxy-server-beheerder.

### <a name="tools-for-diagnosing-issues"></a>Hulpprogramma's voor het oplossen van problemen

Als u beschikt over hulpprogramma's voor netwerken, zoals Fiddler voor Windows, hebt u mogelijk kunnen toodiagnose Hallo problemen als volgt:

- Als u toowork via de proxy hebt, hebben uw netwerken hulpprogramma tooconnect via proxy Hallo tooconfigure.

- Controleer Hallo poortnummer dat wordt gebruikt door uw netwerken hulpprogramma.

- Hallo lokale host-URL en de netwerken van het hulpprogramma poortnummer als proxy-instellingen in Opslagverkenner Hallo invoeren. Als dit correct is uitgevoerd, start u uw netwerken hulpprogramma logboekregistratie netwerkaanvragen door Opslagverkenner toomanagement en service-eindpunten. Voer bijvoorbeeld https://cawablobgrs.blob.core.windows.net/ voor het eindpunt van de blob in een browser en ontvangt u een antwoord lijkt op de volgende hello, die wordt voorgesteld Hallo resource bestaat, hoewel u geen toegang toe heeft.

![Voorbeeld van code](./media/storage-explorer-troubleshooting/4022502_en_2.png)

### <a name="contact-proxy-server-admin"></a>Neem contact op met de serverbeheerder proxy

Als de proxy-instellingen correct zijn, hebt u mogelijk toocontact uw proxy-server-beheerder en

- Zorg ervoor dat de proxy worden niet geblokkeerd verkeer tooAzure management of resource-eindpunten.

- Controleer of Hallo authenticatieprotocol dat wordt gebruikt door de proxyserver. Opslagverkenner biedt momenteel geen ondersteuning voor NTLM-proxy's.

## <a name="unable-tooretrieve-children-error-message"></a>Het foutbericht 'Kan geen tooRetrieve kinderen'

Als u verbonden tooAzure via een proxy bent, moet u controleren of de proxyinstellingen juist zijn. Als u toegang tooa resource zijn verleend van Hallo eigenaar van het Hallo-abonnement of account, Controleer of u hebt gelezen of lijst met machtigingen voor die bron.

### <a name="issues-with-sas-url"></a>Problemen met SAS-URL
Als u verbinding tooa service met behulp van een SAS-URL en deze fout optreedt maakt:

- Controleer of dat Hallo URL de benodigde machtigingen Hallo tooread of lijst met resources biedt.

- Controleer of deze Hallo die URL niet is verlopen.

- Als Hallo SAS-URL is gebaseerd op een toegangsbeleid, controleert u of Hallo-beleid niet is ingetrokken.

## <a name="next-steps"></a>Volgende stappen

Als geen van de oplossingen Hallo werkt, Geef uw probleem via Hallo feedback hulpprogramma met uw e-mailadres en zoveel mogelijk details over Hallo probleem opgenomen als u kunnen, zodat we kunnen contact met u voor het oplossen van Hallo probleem.

toodo, klikt u op **Help** menu en klik vervolgens op **Feedback verzenden**.

![Feedback](./media/storage-explorer-troubleshooting/4022503_en_1.png)

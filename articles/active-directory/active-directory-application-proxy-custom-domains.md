---
title: aaaCustom domeinen in Azure AD-toepassingsproxy | Microsoft Docs
description: Aangepaste domeinen in Azure AD-toepassingsproxy beheren zodat die Hallo-URL voor Hallo app is dezelfde Hallo ongeacht waar uw gebruikers toegang toe.
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 2fe9f895-f641-4362-8b27-7a5d08f8600f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/01/2017
ms.author: kgremban
ms.reviewer: harshja
ms.custom: it-pro
ms.openlocfilehash: 7a433c411976077210a2435c3c087991c7430755
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="working-with-custom-domains-in-azure-ad-application-proxy"></a>Werken met aangepaste domeinen in Azure AD-toepassingsproxy

Wanneer u een toepassing via Azure Active Directory-toepassingsproxy publiceert, maakt u een externe URL voor uw gebruikers toogo toowhen die ze extern werken. Deze URL opgehaald Hallo standaarddomein *yourtenant.msappproxy.net*. Bijvoorbeeld, als u gepubliceerd een app met de naam uitgaven en uw tenant is met de naam Contoso en vervolgens de externe URL Hallo https://expenses-contoso.msappproxy.net zou zijn. Als u toouse op uw eigen domeinnaam wilt, kunt u een aangepast domein voor uw toepassing configureren. 

Het is raadzaam dat u instelt aangepaste domeinen voor uw toepassingen indien mogelijk. Hallo voordelen van aangepaste domeinen onder andere:

- Uw gebruikers toegang krijgen tot de toepassing toohello met dezelfde URL Hallo of ze binnen of buiten uw netwerk werken.
- Als al uw toepassingen hebben dezelfde interne en externe URL hello, blijven toowork zelfs buiten het bedrijfsnetwerk Hallo met koppelingen in één toepassing die tooanother verwijzen. 
- U uw huisstijl beheren en Hallo-URL's die u wilt maken. 


## <a name="configure-a-custom-domain"></a>Een aangepast domein configureren

### <a name="prerequisites"></a>Vereisten

Voordat u een aangepast domein configureren, zorg ervoor dat er Hallo volgens de vereisten die zijn voorbereid: 
- Een [geverifieerd domein toegevoegd tooAzure Active Directory](active-directory-domains-add-azure-portal.md).
- Een aangepaste certificaat voor Hallo-domein in Hallo vorm van een PFX-bestand. 
- Een lokale app [gepubliceerd via toepassingsproxy](application-proxy-publish-azure-portal.md).

### <a name="configure-your-custom-domain"></a>Uw aangepaste domein configureren

Wanneer u deze drie vereisten gereed hebt, volgt u deze stappen tooset van uw aangepaste domein:

1. Meld u aan toohello [Azure-portal](https://portal.azure.com).
2. Navigeer te**Azure Active Directory** > **bedrijfstoepassingen** > **alle toepassingen** en kies Hallo app gewenste toomanage.
3. Selecteer **toepassingsproxy**. 
4. Gebruik in het veld van de externe URL hello, Hallo dropdown lijst tooselect uw aangepaste domein. Als u uw domein in de lijst Hallo niet ziet, nog niet klikt u vervolgens deze geverifieerd nog. 
5. Selecteer **opslaan**
5. Hallo **certificaat** veld dat is uitgeschakeld, wordt ingeschakeld. Selecteer dit veld. 

   ![Klik op tooupload een certificaat](./media/active-directory-application-proxy-custom-domains/certificate.png)

   Als u al een certificaat voor dit domein hebt geüpload, wordt in het certificaatveld Hallo geeft Hallo-certificaatinformatie weer. 

6. Hallo PFX-certificaat uploaden en Hallo wachtwoord invoeren voor Hallo certificaat. 
7. Selecteer **opslaan** toosave uw wijzigingen. 
8. Voeg een [DNS-record](../dns/dns-operations-recordsets-portal.md) dat omleidingen Hallo nieuwe externe URL toohello msappproxy.net-domein. 

>[!TIP] 
>U hoeft slechts één certificaat tooupload per aangepast domein. Wanneer u een certificaat uploaden, kunt u aangepast domein Hallo wanneer u een nieuwe app publiceert en geen aanvullende configuratie toodo, met uitzondering van Hallo DNS-record. 

## <a name="manage-certificates"></a>Certificaten beheren

### <a name="certificate-format"></a>De indeling van certificaat
Er is geen beperking op Hallo certificaat handtekening methoden. Alle worden Elliptic Curve Cryptography (ECC), SAN Subject Alternative Name () en andere algemene typen certificaten ondersteund. 

U kunt een jokertekencertificaat, zolang Hallo jokertekens overeenkomt met de externe URL Hallo gewenst. 

U kunt zelf-ondertekende certificaten, evenals gebruiken. Als u een persoonlijke certificeringsinstantie, moet Hallo CDP (certificaat intrekken point-distributiepunt) voor Hallo certificaat openbaar zijn.

### <a name="changing-hello-domain"></a>Hallo domein wijzigen
Alle geverifieerde domeinen weergegeven in de vervolgkeuzelijst van Hallo externe URL voor uw toepassing. toochange Hallo-domein alleen update die voor de toepassing hello veld. Als Hallo domein u wilt niet in de lijst Hallo [toevoegen als een geverifieerde domeinnaam](active-directory-domains-add-azure-portal.md). Als u een domein dat een bijbehorend certificaat nog geen selecteert, volgt u stap 5-7 tooadd Hallo certificaat. Controleer vervolgens of dat u Hallo DNS-record tooredirect van nieuwe externe URL Hallo bijwerken. 

### <a name="certificate-management"></a>Certificaatbeheer
U kunt hetzelfde voor meerdere toepassingen certificaat tenzij Hallo toepassingen een externe host delen hello gebruiken. 

Ontvangt u een waarschuwing wanneer een certificaat is verlopen, dat u tooupload een ander certificaat via Hallo-portal. Als het Hallo-certificaat is ingetrokken, kunnen uw gebruikers een beveiligingswaarschuwing zien bij het openen van de toepassing hello. We uitvoeren geen intrekkingscontroles voor certificaten.  tooupdate hello certificaat voor een bepaalde toepassing toohello toepassing navigeren en volg de stappen 5 tot en met 7 voor het configureren van aangepaste domeinen op gepubliceerde toepassingen tooupload een nieuw certificaat. Als het oude certificaat Hallo niet door andere toepassingen wordt gebruikt, wordt deze automatisch verwijderd. 

Alle Certificaatbeheer is momenteel door afzonderlijke toepassing pagina's er daarom toomanage certificaten in de context Hallo van relevante Hallo-toepassingen. 

## <a name="next-steps"></a>Volgende stappen
* [Eenmalige aanmelding inschakelen](active-directory-application-proxy-sso-using-kcd.md) tooyour gepubliceerde apps met Azure AD-verificatie.
* [Inschakelen van voorwaardelijke toegang](active-directory-application-proxy-conditional-access.md) tooyour gepubliceerde apps.
* [Uw aangepaste domein naam tooAzure AD toevoegen](active-directory-domains-add-azure-portal.md)



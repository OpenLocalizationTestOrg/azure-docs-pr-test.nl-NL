---
title: aaaHow toocreate een cloudverzameling van Azure RemoteApp | Microsoft Docs
description: Meer informatie over hoe een implementatie van Azure RemoteApp die slaat gegevens op in toocreate hello Azure-cloud.
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
editor: 
ms.assetid: 4d7c6956-7e4a-4a41-b7f2-7e5832bf01e3
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: a072ad19d8293016382831d48d0af8e0f5e0d458
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-a-cloud-collection-of-azure-remoteapp"></a>Hoe toocreate een cloudverzameling van Azure RemoteApp
> [!IMPORTANT]
> Azure RemoteApp wordt op 31 augustus 2017 buiten gebruik gesteld. Lees Hallo [aankondiging](https://go.microsoft.com/fwlink/?linkid=821148) voor meer informatie.
> 
> 

Er zijn twee soorten [Azure RemoteApp verzamelingen](remoteapp-collections.md): 

* Cloud: bevindt zich volledig in Azure. U kunt toosave alle gegevens in de cloud hello (dus een verzameling alleen in de cloud) of tooconnect uw verzameling tooa VNET en er gegevens op te slaan.   
* Hybride: bevat een virtueel netwerk voor toegang tot lokale - hiervoor Hallo gebruik van Azure AD en een on-premises Active Directory-omgeving.

Deze zelfstudie wordt u begeleid Hallo-proces voor het maken van een cloudverzameling. Er zijn vier stappen: 

1. Maak een Azure RemoteApp-verzameling.
2. Eventueel adreslijstsynchronisatie configureren. Als u van Azure AD gebruikmaakt + Active Directory, hebt u toosynchronize gebruikers, contactpersonen en wachtwoorden van uw lokale Active Directory tooyour Azure AD-tenant.
3. Apps publiceren.
4. De gebruikerstoegang configureren.

**Voordat u begint**

U moet toodo Hallo volgende voordat het Hallo-verzameling maken:

* [Aanmelden](https://azure.microsoft.com/services/remoteapp/) voor Azure RemoteApp. 
* Informatie over het Hallo-gebruikers die u toegang tot toogrant wilt verzamelen. Dit kan zijn Microsoft-accountgegevens of Active Directory work accountgegevens voor gebruikers.
* Deze procedure wordt ervan uitgegaan dat u beide gaat toouse een van de sjablooninstallatiekopieën Hallo geleverd als onderdeel van uw abonnement of dat u al hebt geüpload Hallo-sjablooninstallatiekopie die u wilt dat toouse. Als u de installatiekopie van een andere sjabloon tooupload moet, kunt u dat doen via Hallo Sjablooninstallatiekopieën pagina. Klik op **upload de sjablooninstallatiekopie van een** en volg de stappen Hallo in Hallo-wizard. 
* Wilt u toouse Hallo Office 365 ProPlus-installatiekopie? Raadpleeg informatie over [hier](remoteapp-officesubscription.md).
* Wilt u LOB-programma of tooprovide aangepaste apps? Maak een nieuwe [installatiekopie](remoteapp-imageoptions.md) en deze gebruiken in uw cloudverzameling.
* Bereken noodzaak tooconnect tooa VNET. Als u tooconnect tooa VNET kiest, zorg ervoor dat het voldoet aan Hallo [sizing richtlijnen](remoteapp-vnetsizing.md) en dat deze [verbinding kunnen maken van tooRemoteApp](remoteapp-vnet.md). Bekijk Hallo [VNET planning artikel ](remoteapp-planvnet.md)voor meer informatie.
* Als u een VNET, moet u beslissen of u wilt dat toojoin het tooyour lokale Active Directory-domein.

## <a name="step-1-create-a-cloud-collection---with-or-without-a-vnet"></a>Stap 1: Een cloudverzameling - maken met of zonder een VNET
Gebruik Hallo volgende stappen te**maakt u een verzameling cloudconfiguratie**:

1. In de beheerportal Hallo toohello RemoteApp pagina te gaan.
2. Klik op **Nieuw > Snelle invoer**.
3. Voer een naam voor uw verzameling en selecteer de regio.
4. Kies Hallo-abonnement dat u wilt dat toouse - standaard of basic.
5. Kies Hallo sjabloon toouse voor deze verzameling. 
   
    **Tip:** uw RemoteApp-abonnement wordt geleverd met [sjablooninstallatiekopieën](remoteapp-images.md) met Office 365 of Office 2013 (als proefversie) programma's, sommige gepubliceerd (zoals Word) en anderen toopublish gereed. U kunt ook maken een nieuwe [installatiekopie](remoteapp-imageoptions.md) en deze gebruiken in uw cloudverzameling.
6. Klik op **RemoteApp-verzameling maken**.
   
    **Belangrijk:** kan duren too30 minuten tooprovision uw verzameling.

Nadat u uw Azure RemoteApp-collectie is gemaakt, dubbelklikt u op Hallo-naam van Hallo-verzameling. Die verschijnt nu Hallo **Quick Start** pagina - dit is wanneer u klaar bent met het Hallo-verzameling configureren.

Gebruik Hallo volgende stappen uit toocreate een **cloud + VNET verzameling**:

1. In de beheerportal Hallo toohello Azure RemoteApp pagina te gaan.
2. Klik op **nieuwe** > **maken met VNET**.
3. Voer een naam voor uw verzameling.
4. Kies Hallo-abonnement dat u wilt dat toouse - standaard of basic.
5. Kies Hallo VNET dat u al hebt gemaakt. Niet weet hoe toodo die? Op dit moment zijn Hallo stappen in Hallo [hybride](remoteapp-create-hybrid-deployment.md) onderwerp.
6. Beslissen of u toojoin uw verzameling tooyour-domein wilt. Zo ja, moet u toouse AD Connect toointegrate Azure AD en uw Active Directory-omgeving. Die hieronder wordt beschreven in **stap 2**.
7. Klik op **RemoteApp-verzameling maken**.

## <a name="step-2-configure-active-directory-directory-synchronization-optional"></a>Stap 2: (Optioneel) Active Directory directory-synchronisatie configureren
Als u toouse Active Directory wilt, wordt in Azure RemoteApp mapsynchronisatie tussen Azure Active Directory en uw on-premises Active Directory toosynchronize gebruikers, contactpersonen en wachtwoorden tooyour Azure Active Directory-tenant vereist. Zie [Active Directory configureren voor Azure RemoteApp](remoteapp-ad.md) voor informatie over de planning. U kunt ook gaan rechtstreeks te[AD Connect](https://blogs.technet.microsoft.com/enterprisemobility/2014/08/04/connecting-ad-and-azure-ad-only-4-clicks-with-azure-ad-connect/) voor meer informatie.

## <a name="step-3-publish-apps"></a>Stap 3: Apps publiceren
Een Azure RemoteApp-app is Hallo app of het programma dat u tooyour gebruikers bieden. Deze bevindt zich in het Hallo-sjablooninstallatiekopie die u hebt geüpload voor Hallo-verzameling. Wanneer een gebruiker toegang krijgt tot een app, Hallo app toorun in hun lokale omgeving weergegeven, maar deze daadwerkelijk wordt uitgevoerd in een virtuele machine in Azure. 

Voordat u uw gebruikers hebben toegang tot apps, moet u toopublish ze – publiceren van apps kiest, kunnen uw gebruikers toegang Hallo apps via tot extern bureaublad-client Hallo.

U kunt meerdere apps tooyour Azure RemoteApp-verzameling publiceren. Klik op de pagina voor Hallo publishing **publiceren** tooadd een programma. U kunt ofwel publiceren van Hallo **Start** menu van Hallo-sjablooninstallatiekopie of door op te geven Hallo pad op de installatiekopie van het Hallo-sjabloon voor Hallo-app. Als u tooadd uit Hallo **Start** menu Hallo app toopublish kiezen. Als u tooprovide Hallo pad toohello app, geeft u een naam voor het Hallo-app en Hallo pad toowhere die deze is geïnstalleerd op het Hallo-sjablooninstallatiekopie.

## <a name="step-4-configure-user-access"></a>Stap 4: Configureer de gebruikerstoegang
Nu u uw verzameling hebt gemaakt, moet u tooadd Hallo gebruikers dat u kunnen toouse toobe uw externe bronnen wilt. Als u van Active Directory gebruikmaakt, Hallo gebruikers op te geven toegang tooneed tooexist in Active Directory-tenant Hallo die is gekoppeld aan Hallo-abonnement dat u gebruikt toocreate deze verzameling.

1. Klik op de pagina Quick Start Hallo **gebruikerstoegang configureren**. 
2. Hallo werkaccount (van Active Directory) of Microsoft-account die u wilt dat toegang voor toogrant invoeren.
   
   **Opmerkingen:** 
   
   Zorg ervoor dat u Hallo  *user@domain.com*  indeling.
   
   Als u van Office 365 ProPlus in uw verzameling gebruikmaakt, moet u Hallo Active Directory-identiteit voor uw gebruikers. Dit helpt valideren Licentieverlening. 
3. Nadat het Hallo-gebruikers zijn geverifieerd, klikt u op **opslaan**.

## <a name="next-steps"></a>Volgende stappen
Dat is alles: u hebt gemaakt en geïmplementeerd van uw Azure RemoteApp-cloudverzameling. de volgende stap Hallo is toohave uw gebruikers downloaden en installeren van Hallo extern bureaublad-client. U vindt Hallo-URL voor Hallo-client op Hallo Azure RemoteApp-snel starten-pagina. Vervolgens hebben gebruikers zich aanmelden in Hallo-client en de toegang tot Hallo-apps die u hebt gepubliceerd.

### <a name="help-us-help-you"></a>Help ons u te helpen
Wist u dat in de toevoeging toorating in dit artikel en het toevoegen van opmerkingen omlaag hieronder, kunt u wijzigingen toohello artikel zelf? Ontbreekt er iets? Is er iets niet juist? Heb ik iets geschreven dat niet duidelijk is? Blader omhoog en klik op **Edit on GitHub** toomake wijzigingen - deze worden eerst nagekeken toous, en vervolgens wanneer uitgeschakeld op deze, ziet u uw wijzigingen en verbeteringen hier.


---
title: aaaHow toocreate een hybride verzameling voor Azure RemoteApp | Microsoft Docs
description: Meer informatie over hoe een implementatie van RemoteApp die verbinding het interne netwerk tooyour maakt toocreate.
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
editor: 
ms.assetid: 08ea0ce3-3a2c-4ddf-9394-6d75c8030cb1
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: 3fba29acc676e0af48e995da406f889c532c44c3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-a-hybrid-collection-for-azure-remoteapp"></a>Hoe toocreate een hybride verzameling voor Azure RemoteApp
> [!IMPORTANT]
> Azure RemoteApp wordt op 31 augustus 2017 buiten gebruik gesteld. Lees Hallo [aankondiging](https://go.microsoft.com/fwlink/?linkid=821148) voor meer informatie.
> 
> 

Er zijn twee soorten Azure RemoteApp-verzamelingen:

* Cloud: bevindt zich volledig in Azure. U kunt toosave alle gegevens in de cloud hello (dus een verzameling alleen in de cloud) of tooconnect uw verzameling tooa VNET en er gegevens op te slaan.   
* Hybride: bevat een virtueel netwerk voor toegang tot lokale - hiervoor Hallo gebruik van Azure AD en een on-premises Active Directory-omgeving.

Weet u niet dat u nodig? Bekijk [welk type verzameling hebt u nodig voor Azure RemoteApp](remoteapp-collections.md).

Deze zelfstudie wordt u begeleid Hallo-proces voor het maken van een hybride verzameling. Er zijn acht stappen:

1. Bepalen wat [installatiekopie](remoteapp-imageoptions.md) toouse voor uw verzameling. U kunt een aangepaste installatiekopie maken of gebruik een van de installatiekopieën van het Microsoft hello inbegrepen bij uw abonnement.
2. Stel het virtuele netwerk. Bekijk Hallo [VNET plannen](remoteapp-planvnet.md) en [sizing](remoteapp-vnetsizing.md) informatie.
3. Een verzameling maken.
4. Voeg uw verzameling tooyour lokale domein.
5. Een sjabloon installatiekopie tooyour verzameling toevoegen.
6. Adreslijstsynchronisatie configureren. Azure RemoteApp is vereist dat u integreert met Azure Active Directory door beide 1) configureren Azure Active Directory-synchronisatie met Hallo optie Wachtwoordsynchronisatie of 2) configureren Azure Active Directory-synchronisatie zonder Hallo Wachtwoordsynchronisatie optie maar met behulp van een domein dat federatieve tooAD FS. Bekijk Hallo [informatie over de configuratie voor Active Directory met RemoteApp](remoteapp-ad.md).
7. RemoteApp-apps publiceren.
8. De gebruikerstoegang configureren.

**Voordat u begint**

U moet toodo Hallo volgende voordat het Hallo-verzameling maken:

* [Aanmelden](https://azure.microsoft.com/services/remoteapp/) voor Azure RemoteApp.
* Maak een gebruikersaccount in Active Directory-toouse als hello Azure RemoteApp-serviceaccount. Hallo-machtigingen voor dit account beperken zodat deze alleen worden toegevoegd aan machines toohello domein.
* Informatie verzamelen over uw on-premises netwerk: IP-adres informatie en details van VPN-apparaat.
* Hallo installeren [Azure PowerShell](/powershell/azure/overview) module.
* Informatie over het Hallo-gebruikers die u toegang tot toogrant wilt verzamelen. U moet hello Azure Active Directory UPN-naam (bijvoorbeeld name@contoso.com) voor elke gebruiker. Zorg ervoor dat Hallo UPN overeenkomt met tussen Azure AD en Active Directory.
* Kies uw sjablooninstallatiekopie. Een Azure RemoteApp-sjablooninstallatiekopie bevat Hallo apps en programma's wilt u toopublish voor uw gebruikers. Zie [opties voor Azure RemoteApp-installatiekopie](remoteapp-imageoptions.md) voor meer informatie.
* Wilt u toouse Hallo Office 365 ProPlus-installatiekopie? Raadpleeg informatie over [hier](remoteapp-officesubscription.md).
* [Active Directory configureren voor RemoteApp](remoteapp-ad.md).

## <a name="step-1-set-up-your-virtual-network"></a>Stap 1: Uw virtueel netwerk instellen
U kunt een hybride verzameling die gebruikmaakt van een bestaand virtueel netwerk van Azure implementeren of u kunt een nieuw virtueel netwerk maken. Een virtueel netwerk kunt uw gebruikers toegang tot gegevens op uw lokale netwerk via RemoteApp externe bronnen. Uw tooother verzameling netwerk met directe toegang tot Azure-services met een Azure-netwerk hebt en virtuele machines geïmplementeerd toothat virtueel netwerk.

Zorg ervoor dat u bekijkt hello [VNET plannen](remoteapp-planvnet.md) en [VNET grootte](remoteapp-vnetsizing.md) informatie voordat u uw VNET maken.

### <a name="create-an-azure-vnet-and-join-it-tooyour-active-directory-deployment"></a>Een Azure vnet en deel hieraan tooyour Active Directory-implementatie
Eerst maakt u een [virtueel netwerk](../virtual-network/virtual-networks-create-vnet-arm-pportal.md). Dit gebeurt op Hallo **netwerk** tabblad in hello Azure-portal. U moet uw virtuele netwerk toohello Active Directory-implementatie is de Azure Active Directory-tenant gesynchroniseerde tooyour tooconnect.

Zie [een virtueel netwerk maken met Azure-portal Hallo](../virtual-network/virtual-networks-create-vnet-arm-pportal.md) voor meer informatie.

### <a name="make-sure-your-virtual-network-is-ready-for-azure-remoteapp"></a>Zorg ervoor dat het virtuele netwerk is gereed voor Azure RemoteApp
Zorg ervoor dat uw nieuw virtueel netwerk gereed is voordat u uw verzameling maakt. U kunt dit controleren door Hallo volgende te doen:

1. Maak een virtuele machine van Azure binnen Hallo subnet Hallo virtuele netwerk die u zojuist hebt gemaakt voor RemoteApp.
2. Extern bureaublad tooconnect toohello virtuele machine gebruiken. (Klik op **verbinding**.)
3. Deelnemen aan het toohello dezelfde Active Directory-implementatie wilt u toouse voor RemoteApp.

Werkte die? Uw virtuele netwerk en het subnet zijn gereed voor Azure RemoteApp.

U vindt meer informatie over het maken van virtuele machines in Azure en toothem verbinding te maken met extern bureaublad [hier](https://msdn.microsoft.com/library/azure/jj156003.aspx).

## <a name="step-2-create-an-azure-remoteapp-collection"></a>Stap 2: Een Azure RemoteApp-verzameling maken
1. In Hallo [Azure-portal](http://manage.windowsazure.com), gaat u toohello Azure RemoteApp-pagina.
2. Klik op **Nieuw > maken met VNET**.
3. Voer een naam voor uw verzameling.
4. Kies Hallo-abonnement dat u wilt dat toouse - standaard of basic.
5. Kies uw VNET in Hallo vervolgkeuzelijst lijst en klik vervolgens op uw subnet.
6. Kies toojoin het tooyour domein.
7. Klik op **RemoteApp-verzameling maken**.

Nadat u uw Azure RemoteApp-collectie is gemaakt, dubbelklikt u op Hallo-naam van Hallo-verzameling. Die verschijnt nu Hallo **Quick Start** pagina - dit is wanneer u klaar bent met het Hallo-verzameling configureren.

Is er iets mis gaan? Bekijk Hallo [hybride verzameling probleemoplossingsinformatie](remoteapp-hybridtrouble.md).

## <a name="step-3-link-your-collection-toohello-local-domain"></a>Stap 3: Uw verzameling toohello lokale domein koppelen
1. Op Hallo **Quick Start** pagina, klikt u op **lid worden van een lokale domein**.
2. Hello Azure RemoteApp-service-account tooyour lokale Active Directory-domein toevoegen. U moet Hallo domeinnaam, organisatie-eenheid, service-account-gebruikersnaam en wachtwoord.
   
    Dit is Hallo-informatie die u hebt verzameld als u Hallo stappen uitgevoerd in [Active Directory configureren voor Azure RemoteApp](remoteapp-ad.md).

## <a name="step-4-link-tooan-azure-remoteapp-image"></a>Stap 4: Koppeling tooan Azure RemoteApp-installatiekopie
Een Azure RemoteApp-sjablooninstallatiekopie bevat Hallo-programma's die u wilt de tooshare met gebruikers. U kunt een nieuwe maken [sjablooninstallatiekopie](remoteapp-imageoptions.md) of koppeling tooan bestaande image (een al geïmporteerd of tooAzure RemoteApp geüpload). U kunt ook een koppeling tooone Hallo Azure RemoteApp [sjablooninstallatiekopieën](remoteapp-images.md) die Office 365 of Office 2013 (als proefversie) programma's bevatten.

Als u de nieuwe installatiekopie Hallo uploadt, moet u tooenter Hallo naam en Hallo locatie voor de installatiekopie van het Hallo te kiezen. Klik op volgende pagina van wizard Hallo Hallo u ziet dat een set van PowerShell-cmdlets, kopiëren en voer deze cmdlets uit vanaf een verhoogde Windows PowerShell-prompt tooupload Hallo opgegeven installatiekopie.

Als u bestaande sjablooninstallatiekopie tooan koppelt, geeft u gewoon Hallo installatiekopie met de naam, de locatie en de bijbehorende Azure-abonnement.

## <a name="step-5-configure-active-directory-directory-synchronization"></a>Stap 5: Active Directory directory-synchronisatie configureren
Azure RemoteApp is vereist dat u integreert met Azure Active Directory door beide 1) configureren Azure Active Directory-synchronisatie met Hallo optie Wachtwoordsynchronisatie of 2) configureren Azure Active Directory-synchronisatie zonder Hallo Wachtwoordsynchronisatie optie maar met behulp van een domein dat federatieve tooAD FS.

Bekijk [AD Connect](https://blogs.technet.microsoft.com/enterprisemobility/2014/08/04/connecting-ad-and-azure-ad-only-4-clicks-with-azure-ad-connect/) - in dit artikel kunt u directory-integratie in 4 stappen instellen.

Zie [routekaart voor adreslijstsynchronisatie](http://msdn.microsoft.com//library/azure/hh967642.aspx) voor het plannen van informatie en gedetailleerde stappen.

## <a name="step-6-publish-apps"></a>Stap 6: Apps publiceren
Een Azure RemoteApp-app is Hallo app of het programma dat u tooyour gebruikers bieden. Deze bevindt zich in het Hallo-sjablooninstallatiekopie die u hebt geüpload voor Hallo-verzameling. Wanneer een gebruiker een app, wordt deze toorun in hun lokale omgeving wordt weergegeven, maar deze daadwerkelijk wordt uitgevoerd in Azure.

Voordat u uw gebruikers hebben toegang tot apps, moet u toopublish ze – Hiermee kunt uw gebruikers toegang Hallo-apps via Extern bureaublad-client Hallo.

U kunt meerdere apps tooyour verzameling publiceren. Klik op de pagina voor Hallo publishing **publiceren** tooadd een app. U kunt ofwel publiceren van Hallo **Start** menu van Hallo-sjablooninstallatiekopie of door op te geven Hallo pad op de installatiekopie van het Hallo-sjabloon voor Hallo-app. Als u tooadd uit Hallo **Start** menu Hallo programma tooadd kiezen. Als u tooprovide Hallo pad toohello app, geeft u een naam voor het Hallo-app en Hallo pad toowhere die deze is geïnstalleerd op het Hallo-sjablooninstallatiekopie.

## <a name="step-7-configure-user-access"></a>Stap 7: Configureer de gebruikerstoegang
Nu u uw verzameling hebt gemaakt, moet u tooadd Hallo gebruikers dat u kunnen toouse toobe uw externe bronnen wilt. Hallo-gebruikers op te geven toegang tooneed tooexist in Active Directory-tenant Hallo die is gekoppeld aan Hallo-abonnement dat u gebruikt toocreate deze Azure RemoteApp-verzameling.

1. Klik op de pagina Quick Start Hallo **gebruikerstoegang configureren**.
2. Hallo werkaccount (van Active Directory) of Microsoft-account die u wilt dat toegang voor toogrant invoeren.
   
   **Opmerkingen:**
   
   Zorg ervoor dat u Hallo  *user@domain.com*  indeling.
   
   Als u van Office 365 ProPlus in uw verzameling gebruikmaakt, moet u Hallo Active Directory-identiteit voor uw gebruikers. Dit helpt valideren Licentieverlening.
3. Zodra gebruikers Hallo worden gevalideerd, klikt u op **opslaan**.

## <a name="next-steps"></a>Volgende stappen
Dat is alles: u hebt gemaakt en geïmplementeerd uw hybride Azure RemoteApp-verzameling. de volgende stap Hallo is toohave uw gebruikers downloaden en installeren van Hallo extern bureaublad-client. U vindt Hallo-URL voor Hallo-client op Hallo Azure RemoteApp-snel starten-pagina. Vervolgens hebben gebruikers zich aanmelden in Hallo-client en de toegang tot Hallo-apps die u hebt gepubliceerd.

### <a name="help-us-help-you"></a>Help ons u te helpen
Wist u dat in de toevoeging toorating in dit artikel en het toevoegen van opmerkingen omlaag hieronder, kunt u wijzigingen toohello artikel zelf? Ontbreekt er iets? Is er iets niet juist? Heb ik iets geschreven dat niet duidelijk is? Blader omhoog en klik op **Edit on GitHub** toomake wijzigingen - deze worden eerst nagekeken toous, en vervolgens wanneer uitgeschakeld op deze, ziet u uw wijzigingen en verbeteringen hier.


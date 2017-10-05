---
title: Het maken van een cloudverzameling van Azure RemoteApp | Microsoft Docs
description: Informatie over het maken van een implementatie van Azure RemoteApp die gegevens worden opgeslagen in de Azure-cloud.
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
ms.openlocfilehash: 52d5a073c0de42a77cd7163bf402ed2cdf598d95
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-create-a-cloud-collection-of-azure-remoteapp"></a>How to create a cloud collection of Azure RemoteApp (Een cloudverzameling maken van Azure RemoteApp)
> [!IMPORTANT]
> Azure RemoteApp wordt op 31 augustus 2017 buiten gebruik gesteld. Lees de [aankondiging](https://go.microsoft.com/fwlink/?linkid=821148) voor meer informatie.
> 
> 

Er zijn twee soorten [Azure RemoteApp verzamelingen](remoteapp-collections.md): 

* Cloud: bevindt zich volledig in Azure. U kunt alle gegevens opslaan in de cloud (dus een verzameling alleen in de cloud) of voor het verbinden van uw verzameling met een VNET en er gegevens opslaan.   
* Hybride: bevat een virtueel netwerk voor toegang tot lokale - hiervoor hebt u het gebruik van Azure AD en een on-premises Active Directory-omgeving.

Deze zelfstudie wordt u door het proces van een cloudverzameling maken. Er zijn vier stappen: 

1. Maak een Azure RemoteApp-verzameling.
2. Eventueel adreslijstsynchronisatie configureren. Als u van Azure AD gebruikmaakt + Active Directory die u hebt om te synchroniseren van gebruikers, contactpersonen en wachtwoorden van uw lokale Active Directory in uw Azure AD-tenant.
3. Apps publiceren.
4. De gebruikerstoegang configureren.

**Voordat u begint**

U moet voordat u de verzameling maakt als volgt:

* [Aanmelden](https://azure.microsoft.com/services/remoteapp/) voor Azure RemoteApp. 
* Verzamel informatie over de gebruikers die u wilt toegang verlenen tot. Dit kan zijn Microsoft-accountgegevens of Active Directory work accountgegevens voor gebruikers.
* Deze procedure wordt ervan uitgegaan dat u beide gaat een van de sjablooninstallatiekopieën die is opgegeven als onderdeel van uw abonnement te gebruiken of dat u al hebt geüpload de installatiekopie van de sjabloon die u wilt gebruiken. Als u de installatiekopie van een andere sjabloon uploaden moet, kunt u dat doen op de pagina Sjablooninstallatiekopieën. Klik op **upload de sjablooninstallatiekopie van een** en volg de stappen in de wizard. 
* Wilt u de installatiekopie van het Office 365 ProPlus gebruiken? Raadpleeg informatie over [hier](remoteapp-officesubscription.md).
* Geef aangepaste apps of LOB-programma's wilt? Maak een nieuwe [installatiekopie](remoteapp-imageoptions.md) en deze gebruiken in uw cloudverzameling.
* Uitzoeken of u moet verbinding maken met een VNET. Als u verbinding maken met een VNET wilt, controleert u of deze voldoet aan de [sizing richtlijnen](remoteapp-vnetsizing.md) en dat deze [verbinding kunnen maken met RemoteApp](remoteapp-vnet.md). Bekijk de [VNET planning artikel ](remoteapp-planvnet.md)voor meer informatie.
* Als u een VNET, moet u beslissen of u wilt toevoegen aan uw lokale Active Directory-domein.

## <a name="step-1-create-a-cloud-collection---with-or-without-a-vnet"></a>Stap 1: Een cloudverzameling - maken met of zonder een VNET
Gebruik de volgende stappen om te **maakt u een verzameling cloudconfiguratie**:

1. Ga naar de RemoteApp-pagina in de beheerportal.
2. Klik op **Nieuw > Snelle invoer**.
3. Voer een naam voor uw verzameling en selecteer de regio.
4. Kies het plan dat u gebruiken wilt-standaard of basic.
5. Kies de sjabloon die u wilt gebruiken voor deze verzameling. 
   
    **Tip:** uw RemoteApp-abonnement wordt geleverd met [sjablooninstallatiekopieën](remoteapp-images.md) die Office 365 of Office 2013 (als proefversie) programma's, sommige gepubliceerde (zoals Word) bevatten en anderen wilt publiceren. U kunt ook maken een nieuwe [installatiekopie](remoteapp-imageoptions.md) en deze gebruiken in uw cloudverzameling.
6. Klik op **RemoteApp-verzameling maken**.
   
    **Belangrijk:** duurt maximaal 30 minuten voor het inrichten van uw verzameling.

Nadat u uw Azure RemoteApp-collectie is gemaakt, dubbelklikt u op de naam van de verzameling. Die verschijnt nu de **Quick Start** pagina - dit is wanneer u klaar bent met het configureren van de verzameling.

Gebruik de volgende stappen voor het maken een **cloud + VNET verzameling**:

1. Ga naar de pagina Azure RemoteApp in de beheerportal.
2. Klik op **nieuwe** > **maken met VNET**.
3. Voer een naam voor uw verzameling.
4. Kies het plan dat u gebruiken wilt-standaard of basic.
5. Kies het VNET dat u al hebt gemaakt. Weet u niet hoe u dat doen? Op dit moment zijn de stappen de [hybride](remoteapp-create-hybrid-deployment.md) onderwerp.
6. Bepaal of u wilt uw verzameling toevoegen aan uw domein. Zo ja, moet u Azure AD integreren met AD Connect en Active Directory-omgeving. Die hieronder wordt beschreven in **stap 2**.
7. Klik op **RemoteApp-verzameling maken**.

## <a name="step-2-configure-active-directory-directory-synchronization-optional"></a>Stap 2: (Optioneel) Active Directory directory-synchronisatie configureren
Als u gebruikmaken van Active Directory wilt, wordt in Azure RemoteApp mapsynchronisatie tussen Azure Active Directory en uw lokale Active Directory te synchroniseren van gebruikers, contactpersonen en wachtwoorden in uw Azure Active Directory-tenant vereist. Zie [Active Directory configureren voor Azure RemoteApp](remoteapp-ad.md) voor informatie over de planning. U kunt ook rechtstreeks naar gaan [AD Connect](https://blogs.technet.microsoft.com/enterprisemobility/2014/08/04/connecting-ad-and-azure-ad-only-4-clicks-with-azure-ad-connect/) voor meer informatie.

## <a name="step-3-publish-apps"></a>Stap 3: Apps publiceren
Een Azure RemoteApp-app is de app of het programma dat u voor uw gebruikers opgeeft. Deze bevindt zich in de installatiekopie van de sjabloon die u hebt geüpload voor de verzameling. Wanneer een gebruiker een app, wordt de app wordt weergegeven in hun lokale omgeving uit te voeren, maar deze daadwerkelijk wordt uitgevoerd in een virtuele machine in Azure. 

Voordat u uw gebruikers hebben toegang tot apps, moet u ze publiceren: voor het publiceren van apps kunt uw gebruikers toegang krijgen tot de apps via de extern bureaublad-client.

U kunt meerdere apps publiceren naar uw Azure RemoteApp-collectie. Klik op de pagina publishing **publiceren** een programma toevoegen. U kunt ofwel publiceren van de **Start** menu van de installatiekopie van de sjabloon of geef het pad op de sjablooninstallatiekopie voor de app. Als u wilt toevoegen op basis van de **Start** menu, kies de app te publiceren. Als u ervoor kiest om het pad naar de app, Geef een naam voor de app en het pad naar het waarop deze is geïnstalleerd op de sjablooninstallatiekopie.

## <a name="step-4-configure-user-access"></a>Stap 4: Configureer de gebruikerstoegang
Nu u uw verzameling hebt gemaakt, moet u de gebruikers die u wilt gebruiken van uw externe resources toe te voegen. Als u van Active Directory gebruikmaakt, de gebruikers die toegang tot het moet aanwezig zijn in de Active Directory-tenant gekoppeld aan het abonnement op te geven u gebruikt om deze verzameling te maken.

1. Klik op de pagina Quick Start **gebruikerstoegang configureren**. 
2. Geef de werkaccount (van Active Directory) of de Microsoft-account dat u toegang wilt verlenen voor.
   
   **Opmerkingen:** 
   
   Zorg ervoor dat u gebruikt de  *user@domain.com*  indeling.
   
   Als u van Office 365 ProPlus in uw verzameling gebruikmaakt, moet u de Active Directory-identiteit voor uw gebruikers. Dit helpt valideren Licentieverlening. 
3. Nadat de gebruikers zijn geverifieerd, klikt u op **opslaan**.

## <a name="next-steps"></a>Volgende stappen
Dat is alles: u hebt gemaakt en geïmplementeerd van uw Azure RemoteApp-cloudverzameling. De volgende stap is dat uw gebruikers downloaden en installeren van de extern bureaublad-client. U vindt de URL voor de client op de pagina snel starten van Azure RemoteApp. Vervolgens hebben gebruikers zich aanmelden bij de client en de toegang tot de apps die u hebt gepubliceerd.

### <a name="help-us-help-you"></a>Help ons u te helpen
Wist u dat u niet alleen dit artikel kunt beoordelen en opmerkingen kunt toevoegen, maar zelfs wijzigingen kunt aanbrengen in het artikel zelf? Ontbreekt er iets? Is er iets niet juist? Heb ik iets geschreven dat niet duidelijk is? Blader omhoog en klik op **Edit on GitHub** als u wijzigingen wilt aanbrengen. Deze worden eerst nagekeken en wanneer ze zijn goedgekeurd, worden uw wijzigingen en verbeteringen hier weergegeven.


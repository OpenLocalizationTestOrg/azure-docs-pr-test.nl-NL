---
title: Het gebruik van uw Office 365-abonnement met Azure RemoteApp | Microsoft Docs
description: Meer informatie over hoe u uw Office 365-abonnement in Azure RemoteApp kunt gebruiken voor het delen van Office-apps.
services: remoteapp
documentationcenter: 
author: piotrci
manager: mbaldwin
ms.assetid: f82b6e23-2b71-47be-846d-fd93f2652f3c
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: e58ee0444517074d6b756652d03fc79c2370e69e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-use-your-office-365-subscription-with-azure-remoteapp"></a>Het gebruik van uw Office 365-abonnement met Azure RemoteApp
> [!IMPORTANT]
> Azure RemoteApp wordt op 31 augustus 2017 buiten gebruik gesteld. Lees de [aankondiging](https://go.microsoft.com/fwlink/?linkid=821148) voor meer informatie.
> 
> 

Wist u dat u uw bestaande Office 365-abonnement in Azure RemoteApp gebruiken kunt voor het delen van Office-apps vanuit de cloud? Lees verder voor meer informatie over uw Office 365 + Azure RemoteApp-opties, maken inclusief koppelingen naar artikelen over Office 365 die u helpen bij het meeste uit uw abonnement.

## <a name="how-do-i-use-office-365-accounts-for-azure-remoteapp"></a>Hoe gebruik ik Office 365-accounts voor Azure RemoteApp?
Nieuw artikel voor alle informatie van Peter uitchecken: [Azure RemoteApp gebruiken met Office 365-gebruikersaccounts](remoteapp-o365user.md)

## <a name="can-i-use-my-office-365-subscription-to-run-office-applications-in-azure-remoteapp"></a>Kan ik mijn Office 365-abonnement gebruiken Office-toepassingen uitvoeren in Azure RemoteApp?
Ja. Het gebruik van uw Office 365-abonnement is in feite de enige manier om uw Office-toepassingen op Azure RemoteApp.

(Opmerking: als uw Azure RemoteApp-implementatie wordt geleverd door een partner hosting, ze mogelijk om te voorzien van Office-licenties op basis van een [Service Provider Licensing Agreement](http://www.microsoft.com/en-us/Licensing/licensing-programs/spla-program.aspx))

Het aardige van uw Office 365-abonnement is Hiermee kunt u de dezelfde gebruikerslicentie op veel verschillende platforms en omgevingen, met inbegrip van de Azure-cloud te gebruiken. Wanneer u een Office-toepassingen in Azure RemoteApp gebruiken moet u geen aanvullende licenties kopen of uw licenties te configureren op een speciale manier. Hoeft u een Office 365-abonnement inclusief [Office 365 ProPlus](https://technet.microsoft.com/library/Gg702619.aspx).

Office 365 ProPlus schakelt [gedeelde computeractivering](https://technet.microsoft.com/library/Dn782860.aspx) - met deze functie kunt u tijdelijk op basis van gebruikers activering voor Office in virtuele en cloudomgevingen zoals Azure RemoteApp (en extern bureaublad-Services).

Welke Office 365-abonnementen Office 365 ProPlus opnemen? Bekijk de [Service-beschikbaarheid binnen elk plan](https://technet.microsoft.com/library/office-365-plan-options.aspx) tabel. Houd er rekening mee dat niet alle abonnementen Office 365 ProPlus (bijvoorbeeld het Office 365 Business schema) bevatten. Als uw plan niet ondersteunt, kunt u een upgrade naar een plan dat (bijvoorbeeld Office 365 Education E3 is).

## <a name="ok-so-how-are-my-office-365-proplus-licenses-used-with-azure-remoteapp"></a>OK hoe worden mijn Office 365 ProPlus licenties die worden gebruikt met Azure RemoteApp?
Elke gebruikerslicentie voor Office 365 ProPlus kunt één gebruiker Office-toepassingen op maximaal 5 computers plus tablets en telefoons activeren. Elke activering is geregistreerd bij de gebruiker totdat ze Office op het apparaat deactiveren. (Gebruikers kunnen hun apparaten beheren in de [Office 365-portal](https://portal.office365.com/).)

Met Azure RemoteApp een enkele gebruiker mogelijk Meld u aan bij verschillende computers op dezelfde dag gerust. Dat komt doordat de service automatisch beheert en schalen van resources in de cloud, terwijl de gebruiker ziet alleen de apps en programma's die u hebt gedeeld. Voor dit scenario Office 365 ProPlus een gedeelde computer activering modus biedt: dit betekent dat deze gebruiker niet moet doen eventuele Licentiebeheer dat voor toegang tot deze bronnen en die de afzonderlijke computers niet meegeteld in de limiet voor het activeren van 5-computer.

Als u (admin) Office 365 ProPlus licenties aan uw gebruikers toewijzen, kunnen ze Office gebruiken op hun persoonlijke apparaten, evenals via uw Azure RemoteApp-collectie.

## <a name="which-office-applications-can-i-use-with-office-365-and-azure-remoteapp"></a>Welke Office-toepassingen kan ik gebruiken met Office 365 en Azure RemoteApp?
U kunt uw Office 365-abonnement gebruiken om te activeren en Office 2013 delen in Azure RemoteApp-implementaties. We ondersteunen momenteel niet het gebruik van andere versies van Office met Azure RemoteApp. Dit omvat Office 2003, Office 2007, Office 2010 en Office 2016.

## <a name="what-about-visio-pro-or-project-pro"></a>Wat over Visio Pro en Project Pro?
De installatiekopie van het Office 365 ProPlus opgenomen in uw RemoteApp-abonnement omvat zowel Visio Pro en Project Pro. Maar u kunt uw Office 365 ProPlus-abonnement niet gebruiken voor het activeren van deze programma's - deze hebben elk een eigen licentie. U kunt deze activeren op de [Office 365-portal](https://portal.office365.com/). 

Er geen licentie voor deze programma's als u niet wilt gebruiken. Alleen de programma's die u wilt gebruiken - en overslaan van de andere activeren. Nog steeds ziet u ze in de installatiekopie, maar u kunt ze niet gebruiken. 

## <a name="how-do-i-get-started-with-office-365-and-azure-remoteapp"></a>Hoe ga ik aan de slag met Office 365 en Azure RemoteApp?
Nu dat u de details kennen van Office 365-licentieverlening, krijgen we u aan de slag met Azure RemoteApp - het is heel eenvoudig:

Wanneer u uw Azure RemoteApp-collectie, gebruiken de **Office 365 ProPlus (abonnement vereist)** installatiekopie.

![Azure RemoteApp-installatiekopie met de Office 365 Pro Plus](./media/remoteapp-officesubscription/remoteapp-officeimage.png)

Deze installatiekopie bevat de meest recente versie van Windows Server en Office 365 ProPlus. Nadat u uw verzameling (inclusief publishing apps), uw gebruikers gewoon configureren Meld u aan bij Azure RemoteApp (met behulp van de RemoteApp-client) en hun Office 365-referenties opgeven voor alle Office-apps. Licenties worden automatisch geleverd zonder een set up of management is vereist.

## <a name="can-i-create-a-custom-image-with-office-365-proplus"></a>Kan ik een aangepaste installatiekopie maken met Office 365 ProPlus?
U kunt een aangepaste installatiekopie maken voor uw verzameling met Office 365 ProPlus. Er zijn 2 keuzes - gebruik van de installatiekopie van het Azure-galerie we bieden of u kunt uw eigen aangepaste installatiekopie maken en er Office 365 ProPlus installeren.

### <a name="use-the-azure-gallery-image"></a>Gebruik de installatiekopie van het Azure-galerie
De eenvoudigste manier Office 365 ProPlus implementeren in een verzameling is [beginnen met een van de Azure-galerie installatiekopieën](remoteapp-image-on-azurevm.md) opgenomen in uw Azure RemoteApp-abonnement. Zorg ervoor dat u ervoor kiezen de **Windows Server Remote Desktop Session Host met Office 365 ProPlus vooraf geïnstalleerde** installatiekopie. Installeer alle andere apps die u wilt dat op die installatiekopie en u bent klaar om te beginnen.

### <a name="use-a-custom-image"></a>Een aangepaste installatiekopie gebruiken
U kunt altijd een aangepaste installatiekopie maken - kunt u een [Azure VM](remoteapp-image-on-azurevm.md) of [maken van de installatiekopie lokaal](remoteapp-create-custom-image.md) en dit uploaden naar Azure. In beide gevallen moet dat u Office 365 ProPlus met het knooppunt voor het activeren van gedeelde computer installeren. Gebruik de [Office Deployment Tool](http://blogs.technet.com/b/odsupport/archive/2014/07/11/using-the-office-deployment-tool.aspx) en volg de [instructies](https://technet.microsoft.com/library/Dn782858.aspx) voor installatie.  

### <a name="disable-automatic-updates-for-office-365-proplus-in-your-custom-image---important"></a>Het uitschakelen van automatische updates voor Office 365 ProPlus in uw aangepaste installatiekopie - belangrijk
Uw aangepaste installatiekopie wordt gebruikt door Azure RemoteApp als een sjabloon voor het toevoegen van aanvullende bronnen als de vraag van uw gebruikers toeneemt. Om te voorkomen dat vertragingen en verbindingsproblemen, automatische updates voor Office niet uitschakelen in de installatiekopie. Als u dit niet doet, wordt klikt u vervolgens elke bron met die sjabloon gemaakt automatisch bijgewerkt wanneer deze wordt gestart. Gebruik in plaats daarvan het standaard Azure RemoteApp-proces voor het bijwerken van uw aangepaste installatiekopie. Op die manier u de Office-toepassingen eenmaal op de installatiekopie van de sjabloon bijwerkt en vervolgens laat u Azure RemoteApp zorgt voor het ophalen van de updates voor uw gebruikers.

Voeg de volgende in het configuratiebestand van de Office Deployment Tool voor het uitschakelen van automatische updates:

        <Updates Enabled="FALSE" />

Het configuratiebestand moet nu deze regels bevatten:

        <Display Level="NONE" AcceptEULA="TRUE" />
        <Property Name="SharedComputerLicensing" Value="1" />
        <Updates Enabled="FALSE" />

## <a name="so-how-can-i-update-an-image-with-office-365-proplus"></a>Hoe kan ik een afbeelding met Office 365 ProPlus bijwerken?
Er zijn diverse redenen voor het bijwerken van de afbeelding in uw verzameling. Hier volgen een paar:

* Download de nieuwste updates voor Windows 
* Download de nieuwste updates voor Office 365 ProPlus-toepassing
* Uw aangepaste app bijwerken
* Andere configuratie-instellingen voor de afbeelding zelf wijzigen

Voor de end-to-end-stappen voor het bijwerken van uw verzameling voor het gebruik van de installatiekopie die u hebt bijgewerkt, gaat u [hier](remoteapp-update.md). Maar voor informatie over het bijwerken van de afbeelding en de Office 365 ProPlus, bekijk de volgende informatie.

U hebt twee opties voor het bijwerken van uw installatiekopie - vervangt de afbeelding met een volledig nieuw of handmatig bijwerken van uw bestaande installatiekopie.

### <a name="replace-your-image-with-the-latest-azure-gallery-image--add-customizations"></a>Uw installatiekopie vervangen door de installatiekopie van het meest recente Azure-galerie + aanpassingen toevoegen
Met deze optie kunt u Microsoft zorgt voor de Windows Server en Office 365 ProPlus-updates. In plaats van uw bestaande installatiekopie wordt bijgewerkt, maakt u een volledig nieuwe installatiekopie op basis van de installatiekopie van het meest recente galerie. Herhaal de stappen die u hebt gedaan voordat de installatiekopie van het aanpassen: aangepaste apps installeren wijzigen van de configuratie van de installatiekopie, enzovoort.

De galerie met installatiekopieën regelmatig worden bijgewerkt, zodat u eenvoudig, kan er weten dat uw Windows Server en Office 365 ProPlus-apps up-to-date zijn. De verhouding is natuurlijk of hebt u uw aanpassingen toepassen telkens wanneer u een nieuwe installatiekopie ophalen. U kunt scripts voor het automatiseren van het instellen van uw aanpassingen maken.

### <a name="manually-update-your-existing-image"></a>Uw bestaande installatiekopie handmatig bijwerken
Met deze optie kunt u standaardprogramma's van Windows-updates toepassen op de installatiekopie. Voor Office 365 ProPlus, gebruikt u de Office Deployment tool downloaden en installeren van de meest recente updates of versies van Office 365 ProPlus.

> [!IMPORTANT]
> Houd er rekening mee - de Office 365 ProPlus automatische updates niet uitschakelen.
> 
> 

Meer informatie over het gebruik van de Office Deployment Tool voor updates nodig?

* [Klik en klaar voor Office 365-producten implementeren met behulp van de Office Deployment Tool](https://technet.microsoft.com/library/JJ219423.aspx)
* [Implementeren en bijwerken Office 365 ProPlus met behulp van de Office Deployment Tool](https://channel9.msdn.com/Events/Ignite/2015/BRK3168) (video)
* [Instellingen voor Office 365 ProPlus-updates configureren](https://technet.microsoft.com/library/dn761708.aspx)


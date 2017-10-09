---
title: aaaMulti-tenant-ondersteuning voor VMware VM replicatie tooAzure (CSP programma) | Microsoft Docs
description: Hierin wordt beschreven hoe toodeploy Azure Site Recovery in een omgeving met meerdere tenants tooorchestrate replicatie, failovers en herstel van on-premises VMware-virtuele machines (VM's) tooAzure via Hallo CSP programma door met behulp van hello Azure-portal
services: site-recovery
documentationcenter: 
author: mayanknayar
manager: rochakm
editor: 
ms.assetid: 
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: manayar
ms.openlocfilehash: 9be555c9a438f66e6d3dfcdc9f507a84763846d6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="multi-tenant-support-in-azure-site-recovery-for-replicating-vmware-virtual-machines-tooazure-through-csp"></a>Ondersteuning voor meerdere tenants in Azure Site Recovery voor het repliceren van VMware-virtuele machines tooAzure via CSP

Azure Site Recovery biedt ondersteuning voor meerdere tenants omgevingen voor abonnementen van de tenant. Het ondersteunt ook multi-tenancymodus voor tenant-abonnementen die zijn gemaakt en beheerd via een programma van Hallo Microsoft Cloud Solution Provider (CSP). Dit artikel wordt uitgelegd Hallo richtlijnen voor de implementatie en beheer van meerdere tenants VMware naar Azure-scenario's. Het omvat tevens maken en beheren van tenant-abonnementen via de CSP.

In deze richtlijnen wordt getekend sterk van bestaande documentatie voor het repliceren van VMware virtuele machines tooAzure Hallo. Zie voor meer informatie [tooAzure voor replicatie van VMware-virtuele machines met Site Recovery](site-recovery-vmware-to-azure.md).

## <a name="multi-tenant-environments"></a>Multitenant-omgevingen
Er zijn drie primaire modellen voor meerdere tenants:

* **Hosting-Services Provider (HSP) gedeeld**: Hallo partner is eigenaar van de fysieke infrastructuur Hallo en maakt gebruik van gedeelde resources (vCenter, datacenters, fysieke opslag, enzovoort) toohost meerdere tenants virtuele machines op dezelfde infrastructuur Hallo. Hallo accountpartner herstel na noodgevallen management als een beheerde service kunt opgeven of Hallo tenant eigenaar kan herstel na noodgevallen als een oplossing voor selfservice.

* **Hosting-Services Provider-specifieke**: Hallo partner eigenaar is van de fysieke infrastructuur Hallo maar maakt gebruik van toegewijde bronnen (meerdere Vcenter, fysieke datastores, enzovoort) toohost elke tenant-VM's op een aparte infrastructuur. Hallo accountpartner herstel na noodgevallen management als een beheerde service kunt opgeven of Hallo tenant kan de eigenaar bent als een selfservice-oplossing.

* **Beheerde Provider (MSP-Services)**: Hallo klant eigenaar van het Hallo fysieke infrastructuur die als Hallo VMs host en Hallo partner biedt inschakelen voor herstel na noodgevallen en beheer.

## <a name="shared-hosting-multi-tenant-guidance"></a>Gedeeld-hosting multitenant richtlijnen
Deze sectie bevat informatie over Hallo gedeeld-hosting scenario beschreven. Hallo andere twee scenario's zijn subsets van Hallo gedeeld-hosting scenario en ze hello gebruiken dezelfde principes. Hallo verschillen worden achter Hallo Hallo gedeeld-hosting richtlijnen beschreven.

Hallo basic vereiste in een multitenant-scenario is tooisolate Hallo van verschillende tenants. Een tenant mag geen kunnen tooobserve wat een andere tenant is gehost. Deze vereiste is niet zo belangrijk als het zich in een omgeving met selfservice, waar dit kan essentieel zijn in een omgeving beheerd door een partner. In deze richtlijnen wordt ervan uitgegaan dat de isolatie van tenants vereist is.

Hallo-architectuur is opgenomen in het volgende diagram Hallo:

![Gedeelde HSP met één vCenter](./media/site-recovery-multi-tenant-support-vmware-using-csp/shared-hosting-scenario.png)  
**Gedeeld-hosting scenario met één vCenter**

Zoals u in het voorgaande diagram hello, heeft elke klant een afzonderlijke beheerserver. Deze configuratie limieten tenant tootenant-specifieke virtuele machines toegang en kunt isolatie van tenants. Een VMware-replicatie voor virtuele machines scenario gebruikt Hallo configuratie server toomanage accounts toodiscover VM's en agents installeren. We Hallo Volg dezelfde principes voor multitenant-omgevingen met Hallo toevoeging van het beperken van de detectie van de virtuele machine via vCenter toegangsbeheer.

Hallo-gegevensisolatie vereiste vereist dat alle infrastructuur gevoelige gegevens (zoals toegangsreferenties) blijven tootenants niet openbaar te maken. Daarom is het raadzaam dat alle onderdelen van de beheerserver Hallo onder Hallo exclusieve controle van Hallo-partner blijven. Hallo management server-onderdelen zijn:
* Configuratieserver (CS)
* De processerver (PS)
* Hoofddoelserver (MT) 

Een scale-out PS is ook onder het beheer van Hallo partner.

### <a name="every-cs-in-hello-multi-tenant-scenario-uses-two-accounts"></a>Elke CS in Hallo multitenant scenario gebruikt twee accounts

- **vCenter toegangsaccount**: Gebruik deze account toodiscover tenant virtuele machines. Hieraan toegangsmachtigingen vCenter tooit (zoals beschreven in de volgende sectie Hallo) toegewezen. toohelp onbedoeld toegang lekken voorkomen, is het raadzaam dat partners deze referenties zelf invoert in het Hallo-configuratieprogramma.

- **Virtuele machine toegangsaccount**: Gebruik deze account tooinstall Hallo mobility-agent op Hallo tenant-VM's via een automatische push. Dit is meestal een domeinaccount dat een tenant tooa partner bieden kan of dat u kunt ook Hallo partner kan rechtstreeks beheren. Als een tenant niet rechtstreeks tooshare Hallo details met de partner hello wilt, hij of zij toegestaan tooenter Hallo referenties via tijdelijke toegang tot toohello CS, of installeer met hulp van de partner Hallo mobility agents handmatig.

### <a name="requirements-for-a-vcenter-access-account"></a>Vereisten voor een vCenter-toegangsaccount

Zoals vermeld in de voorgaande sectie hello, moet u Hallo CS configureren met een account met een tooit speciale rol die is toegewezen. Hallo roltoewijzing moet toohello vCenter toegangsaccount voor elk object vCenter toegepast en niet doorgegeven toohello onderliggende objecten. Deze configuratie zorgt er tenantisolatie, omdat toegang doorgeven in onbedoelde toegang tooother objecten resulteren kan.

![Hallo optie doorgeven tooChild-objecten](./media/site-recovery-multi-tenant-support-vmware-using-csp/assign-permissions-without-propagation.png)

Hallo alternatieve tooassign Hallo-gebruikersaccount en de rol op Hallo datacenter-object is en deze toohello onderliggende objecten kan doorgeven. Vervolgens geeft Hallo account een *geen toegang* rol voor ieder object (zoals andere tenants VM's) die niet toegankelijk tooa bepaalde tenant moet worden. Deze configuratie is omslachtig en beschrijft de onbedoeld toegangscontroles, omdat elke nieuwe onderliggend object is ook automatisch toegang die wordt overgenomen van bovenliggend object Hallo. Daarom raden we aan dat u de eerste benadering Hallo.

Hallo vCenter accounttoegang procedure is als volgt:

1. Een nieuwe rol maken door het klonen van de vooraf gedefinieerde Hallo *alleen-lezen* rol, en geef hieraan een geschikte naam (zoals Azure_Site_Recovery, zoals in dit voorbeeld).

2. Hallo volgende machtigingen toothis rol toewijzen:

    * **Datastore**: toewijzen van ruimte, bladeren gegevensopslag, bestandsbewerkingen op laag niveau, bestand verwijderen, bestanden van de virtuele machine bijwerken

    * **Netwerk**: netwerk toewijzen

    * **Resource**: toewijzen VM tooresource toepassingen migreren virtuele machine uitgeschakeld, ingeschakeld op virtuele machine migreren

    * **Taken**: taak, Update-taak maken

    * **Virtuele machine**: 
        * Configuratie > alle
        * Interactie > beantwoorden van vraag, apparaatverbinding, configureer CD's, diskettes configureren, uitschakelen, inschakelen, VMware-hulpprogramma's installeren
        * Inventaris > maken op basis van bestaande, het maken van nieuwe, het registreren, registratie
        * Inrichting > downloaden van de virtuele machine toestaan, toestaan virtuele machine bestanden uploaden
        * Momentopname maken van beheer > momentopnamen verwijderen

    ![het dialoogvenster Hallo-rol bewerken](./media/site-recovery-multi-tenant-support-vmware-using-csp/edit-role-permissions.png)

3. Toegang niveaus toohello vCenter account toewijzen (gebruikt in Hallo tenant CS) voor verschillende objecten als volgt:

>| Object | Rol | Opmerkingen |
>| --- | --- | --- |
>| vCenter | Alleen-lezen | Alleen tooallow vCenter vereist openen voor het beheren van verschillende objecten. Als er Hallo-account nooit toobe opgegeven tooa tenant of voor alle beheerbewerkingen op Hallo vCenter gebruikt, kunt u deze machtiging verwijderen. |
>| Datacenter | Azure_Site_Recovery |  |
>| Host en hostcluster | Azure_Site_Recovery | Opnieuw zorgt ervoor dat toegang op niveau van Hallo zodat alleen toegankelijk hosts tenant-VM's voor failover- en na failback hebben. |
>| Gegevensopslag en datastore-cluster | Azure_Site_Recovery | Hetzelfde als de voorgaande. |
>| Netwerk | Azure_Site_Recovery |  |
>| Beheerserver | Azure_Site_Recovery | Omvat toegang tooall onderdelen (CS PS en MT) als een buiten Hallo CS-machine. |
>| Tenant-VM 's | Azure_Site_Recovery | Zorgt ervoor dat een nieuwe tenant-VM's van een bepaalde tenant ook deze toegang krijgen, of ze zich niet kunnen worden gedetecteerd via hello Azure-portal. |

Hallo vCenter accounttoegang is nu voltooid. Deze stap wordt voldaan aan Hallo minimale machtigingen vereiste toocomplete failback-bewerkingen. U kunt ook deze machtigingen gebruiken met uw bestaande beleid. Uw bestaande machtigingen tooinclude rolmachtigingen instellen uit stap 2, gedetailleerde eerder alleen wijzigen.

toorestrict herstel na noodgevallen operations tot Hallo failover-status (dat wil zeggen, zonder failback mogelijkheden), volg Hallo voorgaande procedure met een uitzondering: in plaats van het toewijzen van Hallo *Azure_Site_Recovery* rol toohello vCenter toegangsaccount, toewijzen alleen een *alleen-lezen* rol toothat account. Deze machtigingenset kunt VM-replicatie en failover en failback niet mogelijk. Alles in het proces vóór Hallo blijft echter is. tooensure tenantisolatie en VM-detectie wilt beperken, elke machtiging nog steeds op Hallo-objecten niveau alleen en niet doorgegeven toochild is toegewezen.

## <a name="other-multi-tenant-environments"></a>Andere omgevingen met meerdere tenants

Hallo voorgaande sectie wordt beschreven hoe tooset van een multitenant-omgeving voor een gedeelde hosting oplossing. Hallo zijn twee belangrijke ook andere oplossingen toegewezen hosting en beheerde service. Hallo-architectuur voor deze oplossingen wordt beschreven in Hallo uit te voeren.

### <a name="dedicated-hosting-solution"></a>Toegewezen hosting oplossing

Zoals u in het volgende diagram hello, is Hallo architectuur verschil in een speciale hosting oplossing dat elke tenant-infrastructuur is ingesteld voor alleen die tenant. Omdat tenants via afzonderlijke Vcenter geïsoleerd, Hallo hostingprovider moet nog steeds stappen Hallo CSP opgegeven voor het hosten van gedeelde maar hoeft niet tooworry over isolatie van tenants. CSP setup blijft ongewijzigd.

![architectuur-gedeeld hsp](./media/site-recovery-multi-tenant-support-vmware-using-csp/dedicated-hosting-scenario.png)  
**Speciale hosting scenario met meerdere Vcenter**

### <a name="managed-service-solution"></a>Beheerde service-oplossing

Als Hallo weergegeven in is volgende diagram wordt Hallo architectuur verschil in een beheerde service-oplossing dat elke tenant infrastructuur ook fysiek gescheiden is van andere tenants-infrastructuur. Dit scenario bestaat meestal wanneer het Hallo-tenant is eigenaar van Hallo-infrastructuur en wil een oplossing provider toomanage-noodherstel. Nogmaals, omdat tenants fysiek geïsoleerd via een andere infrastructuur, Hallo partner toofollow Hallo CSP stappen voor het hosten van gedeelde moet maar hoeft niet tooworry over isolatie van tenants. CSP inrichting blijft ongewijzigd.

![architectuur-gedeeld hsp](./media/site-recovery-multi-tenant-support-vmware-using-csp/managed-service-scenario.png)  
**Service-scenario met meerdere Vcenter beheerd**

## <a name="csp-program-overview"></a>Overzicht van de CSP-programma
Hallo [CSP programma](https://partner.microsoft.com/en-US/cloud-solution-provider) bevordert beter samen artikelen die worden geboden door partners alle Microsoft-cloudservices, zoals Office 365, Enterprise Mobility Suite en Microsoft Azure. Met de CSP, onze partners Hallo end-to-end-relatie met klanten eigenaar en contactpunt van de primaire relatie Hallo geworden. Partners kunnen Azure-abonnementen voor klanten implementeren en combineren Hallo abonnementen met hun eigen toegevoegde waarde, aangepaste aanbiedingen.

Met Azure Site Recovery beheren partners Hallo volledige herstel na noodgevallen oplossing voor klanten rechtstreeks via de CSP. Of ze kunnen gebruiken CSP tooset Site Recovery-omgevingen en laat klanten hun eigen behoeften voor herstel na noodgevallen op een manier selfservice beheren. In beide gevallen zijn partners Hallo samenwerking tussen de Site Recovery en hun klanten. Partners klantrelatie Hallo-service en facturen voor gebruik van de Site Recovery.

## <a name="create-and-manage-tenant-accounts"></a>Maken en beheren van tenantaccounts

### <a name="step-0-prerequisite-check"></a>Stap 0: Controle van vereisten

Hallo VM vereisten zijn Hallo beschreven in Hallo [documentatie van Azure Site Recovery](site-recovery-vmware-to-azure.md). In de vereisten voor toevoeging toothose, moet u hebben Hallo eerder genoemde toegang controlemechanismen zijn geïmplementeerd voordat u verdergaat met tenant-beheer via de CSP. Voor elke tenant, maakt u een afzonderlijke beheerserver die kan communiceren met Hallo tenant-VM's en vCenter van partners. Alleen Hallo partner heeft toegang tot rechten toothis server.

### <a name="step-1-create-a-tenant-account"></a>Stap 1: Een tenantaccount maken

1. Via [Microsoft Partner Center](https://partnercenter.microsoft.com/), tooyour CSP account aanmelden. 
 
2. Op Hallo **Dashboard** selecteert u **klanten**.

    ![Hallo klanten van Microsoft-Partner Center koppeling](./media/site-recovery-multi-tenant-support-vmware-using-csp/csp-dashboard-display.png)

3. Op de pagina Hallo dat wordt geopend, klikt u op Hallo **klant toevoegen** knop.

    ![knop voor Hallo-klant toevoegen](./media/site-recovery-multi-tenant-support-vmware-using-csp/add-new-customer.png)

4. Op Hallo **nieuwe klant** pagina, vul Hallo accountdetails informatie voor Hallo-tenant en klik op **volgende: abonnementen**.

    ![Hallo accountgegevens pagina](./media/site-recovery-multi-tenant-support-vmware-using-csp/customer-add-filled.png)

5. Selecteer op Hallo abonnementen selectiepagina Hallo **Microsoft Azure** selectievakje. U kunt andere abonnementen nu of op elk gewenst moment toevoegen.

    ![het selectievakje Hallo Microsoft Azure-abonnement](./media/site-recovery-multi-tenant-support-vmware-using-csp/azure-subscription-selection.png)

6. Op Hallo **revisie** pagina, om Hallo tenant details te bevestigen en klik vervolgens op **indienen**.

    ![Hallo-voorbeeldpagina](./media/site-recovery-multi-tenant-support-vmware-using-csp/customer-summary-page.png)  

    Nadat u hebt gemaakt Hallo tenantaccount, verschijnt een bevestigingspagina, met de details van Hallo Hallo standaardaccount en Hallo wachtwoord voor dat abonnement. 

7. Hallo gegevens opslaan en wachtwoord hello later als nodig is via Azure portal-aanmeldingspagina Hallo wijzigen.  
 
    U kunt deze informatie delen met Hallo-tenant is of u kunt maken en delen van een afzonderlijk account indien nodig.

### <a name="step-2-access-hello-tenant-account"></a>Stap 2: Toegang Hallo tenantaccount

U opent Hallo tenantabonnement via Hallo Microsoft Partner Center-Dashboard, zoals beschreven in ' stap 1: een tenantaccount maken. " 

1. Ga toohello **klanten** pagina en klik vervolgens op Hallo-naam van Hallo tenantaccount.

2. Op Hallo **abonnementen** pagina van Hallo tenantaccount, kunt u Hallo bestaande account abonnementen controleren en meer abonnementen zo nodig toevoegen. bewerkingen voor toomanage hello tenant herstel na noodgevallen, selecteer **alle resources (Azure-portal)**.

    ![Alle Resources Hallo-koppeling](./media/site-recovery-multi-tenant-support-vmware-using-csp/all-resources-select.png)  
    
    Te klikken op **alle resources** verleent u toegang tot Azure-abonnementen toohello-tenant. U kunt toegang controleren door te klikken op Hallo hello Azure Active Directory-koppeling top rechts van hello Azure-portal.

    ![Azure Active Directory-koppeling](./media/site-recovery-multi-tenant-support-vmware-using-csp/aad-admin-display.png)

U kunt nu alle siteherstel bewerkingen voor de tenant Hallo via hello Azure-portal en Hallo herstel na noodgevallen bewerkingen beheren. tooaccess hello tenantabonnement via CSP voor beheerde noodherstel, volg Hallo proces eerder beschreven.

### <a name="step-3-deploy-resources-toohello-tenant-subscription"></a>Stap 3: Resources toohello tenantabonnement implementeren
1. Een resourcegroep maken op Hallo Azure-portal, en vervolgens implementeert u een Recovery Services-kluis per Hallo normale proces. 
 
2. Hallo kluisregistratiesleutel downloaden.

3. Hallo CS voor Hallo tenant registreren met behulp van Hallo kluisregistratiesleutel.

4. Hallo referenties invoeren voor Hallo twee toegangsaccounts: toegang tot account toegangsaccount vCenter en de VM.

    ![Accounts van server configuration Manager](./media/site-recovery-multi-tenant-support-vmware-using-csp/config-server-account-display.png)

### <a name="step-4-register-site-recovery-infrastructure-toohello-recovery-services-vault"></a>Stap 4: Register Site Recovery-infrastructuur toohello Recovery Services-kluis
1. In hello Azure-portal op Hallo kluis die u eerder hebt gemaakt, registreert u Hallo vCenter server toohello CS die u hebt geregistreerd in ' stap 3: implementeren resources toohello tenantabonnement. " Hallo vCenter access account gebruiken voor dit doel.
2. Eindigen Hallo 'Infrastructuur voorbereiden' proces voor siteherstel per Hallo normale proces.
3. Hallo VM's zijn nu gereed toobe gerepliceerd. Zorg dat alleen hello van tenant-VM's worden weergegeven op Hallo **virtuele machines selecteren** blade onder Hallo **repliceren** optie.

    ![Lijst met virtuele machines op Hallo Selecteer virtuele machines blade voor de tenantsleutel](./media/site-recovery-multi-tenant-support-vmware-using-csp/tenant-vm-display.png)

### <a name="step-5-assign-tenant-access-toohello-subscription"></a>Stap 5: Toewijzen tenant toegang toohello abonnement

Voor self-service noodherstel toohello tenant Hallo accountgegevens opgeven, zoals vermeld in stap 6 van Hallo ' stap 1: Maak een tenantaccount ' sectie. Deze actie niet uitvoeren wanneer Hallo partner Hallo herstel na noodgevallen infrastructuur ingesteld. Of Hallo herstel na noodgevallen type beheerde of selfservice, partners toegang moeten hebben tot tenant abonnementen via Hallo CSP-portal. Ze Hallo partner eigendom kluis instellen en infrastructuur toohello tenant abonnementen te registreren.

Partners kunnen ook een nieuwe gebruiker toohello tenantabonnement via Hallo CSP portal toevoegen door Hallo volgende te doen:

1. Ga toohello-tenant CSP abonnementpagina en selecteer vervolgens Hallo **gebruikers en licenties** optie.

    ![Hallo pagina van de tenant CSP-abonnement](./media/site-recovery-multi-tenant-support-vmware-using-csp/users-and-licences.png)

    U kunt nu een nieuwe gebruiker maken door te voeren Hallo relevante gegevens en machtigingen te selecteren of door het Hallo-lijst met gebruikers in een CSV-bestand uploaden.

2. Nadat u een nieuwe gebruiker hebt gemaakt, gaat u terug toohello Azure portal, en klik vervolgens op Hallo **abonnement** blade, selecteer Hallo relevante abonnement.

3. Selecteer op de blade Hallo die wordt geopend, **Access Control (IAM)**, en klik vervolgens op **toevoegen** tooadd een gebruiker met relevante Hallo-toegangsniveau.      
    Hallo-gebruikers die zijn gemaakt via Hallo CSP portal worden automatisch weergegeven op het Hallo-blade die wordt geopend nadat u een toegangsniveau op.

    ![Een gebruiker toevoegen](./media/site-recovery-multi-tenant-support-vmware-using-csp/add-user-subscription.png)

    Voor de meeste management bewerkingen Hallo *Inzender* rol is voldoende. Gebruikers met dit toegangsniveau kunnen doen alles op een abonnement, behalve toegangsniveaus wijzigen (waarvoor *eigenaar*-toegang is vereist). U kunt verder verfijnen Hallo toegangsniveaus zoals vereist.

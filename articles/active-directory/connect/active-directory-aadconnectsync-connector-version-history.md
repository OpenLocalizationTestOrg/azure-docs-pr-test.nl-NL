---
title: Connector versiegeschiedenis van Release | Microsoft Docs
description: In dit onderwerp geeft een lijst van alle versies van de Connectors voor Forefront Identity Manager (FIM) en Microsoft Identity Manager (MIM)
services: active-directory
documentationcenter: 
author: fimguy
manager: femila
editor: 
ms.assetid: 6a0c66ab-55df-4669-a0c7-1fe1a091a7f9
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 08/24/2017
ms.author: fimguy
ms.openlocfilehash: 313145f4d8e5faa91fb3504cb0fd0ba87ca2e379
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="connector-version-release-history"></a><span data-ttu-id="9a87b-103">Releasegeschiedenis van connectorversie</span><span class="sxs-lookup"><span data-stu-id="9a87b-103">Connector Version Release History</span></span>
<span data-ttu-id="9a87b-104">De Connectors voor Forefront Identity Manager (FIM) en Microsoft Identity Manager (MIM) worden regelmatig bijgewerkt.</span><span class="sxs-lookup"><span data-stu-id="9a87b-104">The Connectors for Forefront Identity Manager (FIM) and Microsoft Identity Manager (MIM) are updated frequently.</span></span>

> [!NOTE]
> <span data-ttu-id="9a87b-105">In dit onderwerp is alleen van FIM en MIM.</span><span class="sxs-lookup"><span data-stu-id="9a87b-105">This topic is on FIM and MIM only.</span></span> <span data-ttu-id="9a87b-106">Deze Connectors worden niet ondersteund voor installatie op Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="9a87b-106">These Connectors are not supported for install on Azure AD Connect.</span></span> <span data-ttu-id="9a87b-107">Uitgebrachte Connectors zijn vooraf geïnstalleerd op AADConnect wanneer een upgrade naar Build opgegeven.</span><span class="sxs-lookup"><span data-stu-id="9a87b-107">Released Connectors are preinstalled on AADConnect when upgrading to specified Build.</span></span>

<span data-ttu-id="9a87b-108">In dit onderwerp lijst van alle versies van de Connectors die zijn uitgebracht.</span><span class="sxs-lookup"><span data-stu-id="9a87b-108">This topic list all versions of the Connectors that have been released.</span></span>

<span data-ttu-id="9a87b-109">Verwante koppelingen:</span><span class="sxs-lookup"><span data-stu-id="9a87b-109">Related links:</span></span>

* [<span data-ttu-id="9a87b-110">Download de meest recente Connectors</span><span class="sxs-lookup"><span data-stu-id="9a87b-110">Download Latest Connectors</span></span>](http://go.microsoft.com/fwlink/?LinkId=717495)
* <span data-ttu-id="9a87b-111">[Algemene LDAP-Connector](active-directory-aadconnectsync-connector-genericldap.md) documentatie verwijst naar</span><span class="sxs-lookup"><span data-stu-id="9a87b-111">[Generic LDAP Connector](active-directory-aadconnectsync-connector-genericldap.md) reference documentation</span></span>
* <span data-ttu-id="9a87b-112">[Algemene SQL-Connector](active-directory-aadconnectsync-connector-genericsql.md) documentatie verwijst naar</span><span class="sxs-lookup"><span data-stu-id="9a87b-112">[Generic SQL Connector](active-directory-aadconnectsync-connector-genericsql.md) reference documentation</span></span>
* <span data-ttu-id="9a87b-113">[Web-Services-Connector](http://go.microsoft.com/fwlink/?LinkID=226245) documentatie verwijst naar</span><span class="sxs-lookup"><span data-stu-id="9a87b-113">[Web Services Connector](http://go.microsoft.com/fwlink/?LinkID=226245) reference documentation</span></span>
* <span data-ttu-id="9a87b-114">[PowerShell Connector](active-directory-aadconnectsync-connector-powershell.md) documentatie verwijst naar</span><span class="sxs-lookup"><span data-stu-id="9a87b-114">[PowerShell Connector](active-directory-aadconnectsync-connector-powershell.md) reference documentation</span></span>
* <span data-ttu-id="9a87b-115">[Lotus Domino-Connector](active-directory-aadconnectsync-connector-domino.md) documentatie verwijst naar</span><span class="sxs-lookup"><span data-stu-id="9a87b-115">[Lotus Domino Connector](active-directory-aadconnectsync-connector-domino.md) reference documentation</span></span>


## <a name="116040-aadconnect-pending-release"></a><span data-ttu-id="9a87b-116">1.1.604.0 (AADConnect in behandeling zijnde Release)</span><span class="sxs-lookup"><span data-stu-id="9a87b-116">1.1.604.0 (AADConnect Pending Release)</span></span>


### <a name="fixed-issues"></a><span data-ttu-id="9a87b-117">Opgeloste problemen:</span><span class="sxs-lookup"><span data-stu-id="9a87b-117">Fixed issues:</span></span>

* <span data-ttu-id="9a87b-118">Algemene webservices:</span><span class="sxs-lookup"><span data-stu-id="9a87b-118">Generic Web Services:</span></span>
  * <span data-ttu-id="9a87b-119">Een probleem dat verhindert dat er een SOAP-project wordt gemaakt wanneer er twee of meer eindpunten zijn opgelost.</span><span class="sxs-lookup"><span data-stu-id="9a87b-119">Fixed an issue preventing a SOAP project from being created when there were two or more endpoints.</span></span>
* <span data-ttu-id="9a87b-120">Algemene SQL:</span><span class="sxs-lookup"><span data-stu-id="9a87b-120">Generic SQL:</span></span>
  * <span data-ttu-id="9a87b-121">In de werking van het importeren is de GSQL niet converteren van tijd correct wanneer opgeslagen naar het connectorgebied overgebracht.</span><span class="sxs-lookup"><span data-stu-id="9a87b-121">In the operation of import the GSQL was not converting time correctly, when saved to connector space.</span></span> <span data-ttu-id="9a87b-122">De standaardnotatie voor datum en tijd voor connectorgebied overgebracht van de GSQL is gewijzigd van 'jjjj-MM-dd: ssZ' in 'jjjj-MM-dd: ssZ'.</span><span class="sxs-lookup"><span data-stu-id="9a87b-122">The default date and time format for connector space of the GSQL was changed from 'yyyy-MM-dd hh:mm:ssZ' to 'yyyy-MM-dd HH:mm:ssZ'.</span></span>

## <a name="115510-aadconnect-115530"></a><span data-ttu-id="9a87b-123">1.1.551.0 (AADConnect 1.1.553.0)</span><span class="sxs-lookup"><span data-stu-id="9a87b-123">1.1.551.0 (AADConnect 1.1.553.0)</span></span>

### <a name="fixed-issues"></a><span data-ttu-id="9a87b-124">Opgeloste problemen:</span><span class="sxs-lookup"><span data-stu-id="9a87b-124">Fixed issues:</span></span>

* <span data-ttu-id="9a87b-125">Algemene webservices:</span><span class="sxs-lookup"><span data-stu-id="9a87b-125">Generic Web Services:</span></span>
  * <span data-ttu-id="9a87b-126">Het hulpprogramma Wsconfig is niet juist geconverteerd de Json-matrix van 'voorbeeldaanvraag' voor de methode voor de REST.</span><span class="sxs-lookup"><span data-stu-id="9a87b-126">The Wsconfig tool did not convert correctly the Json array from "sample request" for the REST service method.</span></span> <span data-ttu-id="9a87b-127">Dit veroorzaakt problemen met serialisatie deze Json-matrix voor de REST-aanvraag.</span><span class="sxs-lookup"><span data-stu-id="9a87b-127">This caused problems with serialization this Json array for the REST request.</span></span>
  * <span data-ttu-id="9a87b-128">Web Service-Connector Configuration Tool biedt geen ondersteuning voor informatie over het gebruik van symbolen ruimte in JSON-kenmerknamen</span><span class="sxs-lookup"><span data-stu-id="9a87b-128">Web Service Connector Configuration Tool does not support usage of space symbols in JSON attribute names</span></span> 
    * <span data-ttu-id="9a87b-129">Het patroon van een vervanging kan handmatig worden toegevoegd aan het bestand WSConfigTool.exe.config bijvoorbeeld```<appSettings> <add key=”JSONSpaceNamePattern” value="__" /> </appSettings>```</span><span class="sxs-lookup"><span data-stu-id="9a87b-129">A Substitution pattern can be added manually to the WSConfigTool.exe.config file, e.g. ```<appSettings> <add key=”JSONSpaceNamePattern” value="__" /> </appSettings>```</span></span>

* <span data-ttu-id="9a87b-130">Lotus Notes:</span><span class="sxs-lookup"><span data-stu-id="9a87b-130">Lotus Notes:</span></span>
  * <span data-ttu-id="9a87b-131">Wanneer de optie **aangepaste certifiers toestaan voor organisatie/organisatorische eenheden** is uitgeschakeld en vervolgens de connector is mislukt tijdens het exporteren (Update) na de export-stroom alle kenmerken worden geëxporteerd naar Domino maar op het moment van exporteren een KeyNotFoundException wordt geretourneerd om te synchroniseren.</span><span class="sxs-lookup"><span data-stu-id="9a87b-131">When the option **Allow custom certifiers for Organization/Organizational Units** is disabled then the connector fails during export (Update) After the export flow all attributes are exported to Domino but at the time of export a KeyNotFoundException is returned to Sync.</span></span> 
    * <span data-ttu-id="9a87b-132">Dit gebeurt omdat de naamswijziging mislukt als er wordt geprobeerd DN-naam (kenmerk UserName) wijzigen door het wijzigen van een van de volgende kenmerken:</span><span class="sxs-lookup"><span data-stu-id="9a87b-132">This happens because the rename operation fails when it tries to change DN (UserName attribute) by changing one of the attributes below:</span></span>  
      - <span data-ttu-id="9a87b-133">Achternaam</span><span class="sxs-lookup"><span data-stu-id="9a87b-133">LastName</span></span>
      - <span data-ttu-id="9a87b-134">Voornaam</span><span class="sxs-lookup"><span data-stu-id="9a87b-134">FirstName</span></span>
      - <span data-ttu-id="9a87b-135">MiddleInitial</span><span class="sxs-lookup"><span data-stu-id="9a87b-135">MiddleInitial</span></span>
      - <span data-ttu-id="9a87b-136">AltFullName</span><span class="sxs-lookup"><span data-stu-id="9a87b-136">AltFullName</span></span>
      - <span data-ttu-id="9a87b-137">AltFullNameLanguage</span><span class="sxs-lookup"><span data-stu-id="9a87b-137">AltFullNameLanguage</span></span>
      - <span data-ttu-id="9a87b-138">organisatie-eenheid</span><span class="sxs-lookup"><span data-stu-id="9a87b-138">ou</span></span>
      - <span data-ttu-id="9a87b-139">altcommonname</span><span class="sxs-lookup"><span data-stu-id="9a87b-139">altcommonname</span></span>

  * <span data-ttu-id="9a87b-140">Wanneer **aangepaste certifiers toestaan voor organisatie/organisatorische eenheden** optie is ingeschakeld, maar vereist certifiers zijn nog steeds leeg vervolgens KeyNotFoundException optreedt.</span><span class="sxs-lookup"><span data-stu-id="9a87b-140">When **Allow custom certifiers for Organization/Organizational Units** option is enabled, but required certifiers are still empty, then KeyNotFoundException occurs.</span></span>

### <a name="enhancements"></a><span data-ttu-id="9a87b-141">Verbeteringen:</span><span class="sxs-lookup"><span data-stu-id="9a87b-141">Enhancements:</span></span>

* <span data-ttu-id="9a87b-142">Algemene SQL:</span><span class="sxs-lookup"><span data-stu-id="9a87b-142">Generic SQL:</span></span>
  * <span data-ttu-id="9a87b-143">**Scenario: aangepast geïmplementeerd:** ' * ' functie</span><span class="sxs-lookup"><span data-stu-id="9a87b-143">**Scenario: redesigned Implemented:** "*" feature</span></span>
  * <span data-ttu-id="9a87b-144">**Beschrijving van oplossing:** gewijzigd benadering voor [met meerdere waarden verwijzing kenmerken verwerking](active-directory-aadconnectsync-connector-genericsql.md).</span><span class="sxs-lookup"><span data-stu-id="9a87b-144">**Solution description:** Changed approach for [multi-valued reference attributes handling](active-directory-aadconnectsync-connector-genericsql.md).</span></span>


### <a name="fixed-issues"></a><span data-ttu-id="9a87b-145">Opgeloste problemen:</span><span class="sxs-lookup"><span data-stu-id="9a87b-145">Fixed issues:</span></span>

* <span data-ttu-id="9a87b-146">Algemene webservices:</span><span class="sxs-lookup"><span data-stu-id="9a87b-146">Generic Web Services:</span></span>
  * <span data-ttu-id="9a87b-147">Serverconfiguratie kan niet worden geïmporteerd als WebService Connector aanwezig is</span><span class="sxs-lookup"><span data-stu-id="9a87b-147">Can’t import Server configuration if WebService Connector is present</span></span>
  * <span data-ttu-id="9a87b-148">WebService-Connector werkt niet met meerdere Web-Services</span><span class="sxs-lookup"><span data-stu-id="9a87b-148">WebService Connector is not working with multiple  Web Services</span></span>

* <span data-ttu-id="9a87b-149">Algemene SQL:</span><span class="sxs-lookup"><span data-stu-id="9a87b-149">Generic SQL:</span></span>
  * <span data-ttu-id="9a87b-150">Er is geen objecttypen worden vermeld voor één waarde waarnaar wordt verwezen kenmerk</span><span class="sxs-lookup"><span data-stu-id="9a87b-150">No object types are listed for single value referenced attribute</span></span>
  * <span data-ttu-id="9a87b-151">Delta-import voor wijzigingen bijhouden strategie verwijderingen object wanneer de waarde wordt verwijderd uit de tabel met meerdere waarden</span><span class="sxs-lookup"><span data-stu-id="9a87b-151">Delta import on Change Tracking strategy deletes object when value is removed from multi-value table</span></span>
  * <span data-ttu-id="9a87b-152">OverflowException in GSQL connector met de DB2 op AS / 400</span><span class="sxs-lookup"><span data-stu-id="9a87b-152">OverflowException in GSQL connector with DB2 on AS/400</span></span>

<span data-ttu-id="9a87b-153">Lotus:</span><span class="sxs-lookup"><span data-stu-id="9a87b-153">Lotus:</span></span>
  * <span data-ttu-id="9a87b-154">Toegevoegde optie om te zoeken naar organisatie-eenheden voor het openen van de pagina GlobalParameters enable\disable</span><span class="sxs-lookup"><span data-stu-id="9a87b-154">Added option to enable\disable searching OUs before opening GlobalParameters page</span></span>

## <a name="114430"></a><span data-ttu-id="9a87b-155">1.1.443.0</span><span class="sxs-lookup"><span data-stu-id="9a87b-155">1.1.443.0</span></span>

<span data-ttu-id="9a87b-156">Uitgebracht: 2017 maart</span><span class="sxs-lookup"><span data-stu-id="9a87b-156">Released: 2017 March</span></span>

### <a name="enhancements"></a><span data-ttu-id="9a87b-157">Verbeteringen</span><span class="sxs-lookup"><span data-stu-id="9a87b-157">Enhancements</span></span>

* <span data-ttu-id="9a87b-158">Algemene SQL:</span><span class="sxs-lookup"><span data-stu-id="9a87b-158">Generic SQL:</span></span></br><span data-ttu-id="9a87b-159">
  **Scenario symptomen:** is een bekende beperking met de SQL-Connector waar we alleen een verwijzing naar een objecttype toestaan en vereisen kruisverwijzingen met leden.</span><span class="sxs-lookup"><span data-stu-id="9a87b-159">
  **Scenario Symptoms:**  It is a well-known limitation with the SQL Connector where we only allow a reference to one object type and require cross reference with members.</span></span> </br><span data-ttu-id="9a87b-160">
**Beschrijving van oplossing:** In de verwerkingsstap voor verwijzingen zijn ' * ' optie kiest, worden alle combinaties van objecttypen terug naar de synchronisatie-engine geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="9a87b-160">
**Solution description:** In the processing step for references were "*" option is chosen, ALL combinations of object types will be returned back to the sync engine.</span></span>

>[!Important]
- <span data-ttu-id="9a87b-161">Hiermee maakt u veel tijdelijke aanduidingen</span><span class="sxs-lookup"><span data-stu-id="9a87b-161">This will create many placeholders</span></span>
- <span data-ttu-id="9a87b-162">Is vereist om ervoor te zorgen dat de naamgeving is kruislings objecttypen die uniek zijn.</span><span class="sxs-lookup"><span data-stu-id="9a87b-162">It is required to make sure the naming is unique cross object types.</span></span>


* <span data-ttu-id="9a87b-163">Algemene LDAP:</span><span class="sxs-lookup"><span data-stu-id="9a87b-163">Generic LDAP:</span></span></br><span data-ttu-id="9a87b-164">
 **Scenario:** wanneer slechts enkele containers in specifieke partitie zijn geselecteerd, klikt u vervolgens de zoekopdracht nog wordt uitgevoerd in hele partitie.</span><span class="sxs-lookup"><span data-stu-id="9a87b-164">
**Scenario:** When only few containers are selected in specific partition, then the search still will be done in whole partition.</span></span> <span data-ttu-id="9a87b-165">Specifieke worden gefilterd door de synchronisatieservice, maar niet door MA wat kan leiden tot verminderde prestaties.</span><span class="sxs-lookup"><span data-stu-id="9a87b-165">Specific will be filtered by Synchronization Service, but not by MA which might cause performance degradation.</span></span> </br>

 <span data-ttu-id="9a87b-166">**Beschrijving van oplossing:** code GLDAP gewijzigd-connector maken het mogelijk Doorloop alle containers en objecten zoeken in elk van deze in plaats van zoeken in de hele partitie.</span><span class="sxs-lookup"><span data-stu-id="9a87b-166">**Solution description:** Changed GLDAP connector's code to make it possible go through all containers and search objects in each of them, instead of searching in the whole partition.</span></span>


* <span data-ttu-id="9a87b-167">Lotus Domino:</span><span class="sxs-lookup"><span data-stu-id="9a87b-167">Lotus Domino:</span></span>

  <span data-ttu-id="9a87b-168">**Scenario:** Domino e-mailondersteuning voor verwijderen van een persoon worden verwijderd tijdens het exporteren van een.</span><span class="sxs-lookup"><span data-stu-id="9a87b-168">**Scenario:** Domino mail deletion support for a person removal during an export.</span></span> </br><span data-ttu-id="9a87b-169">
  **Oplossing:** ondersteuning voor het verwijderen van een persoon worden verwijderd tijdens het exporteren van een configureerbare e.</span><span class="sxs-lookup"><span data-stu-id="9a87b-169">
**Solution:** Configurable mail deletion support for a person removal during an export.</span></span>

### <a name="fixed-issues"></a><span data-ttu-id="9a87b-170">Opgeloste problemen:</span><span class="sxs-lookup"><span data-stu-id="9a87b-170">Fixed issues:</span></span>
* <span data-ttu-id="9a87b-171">Algemene webservices:</span><span class="sxs-lookup"><span data-stu-id="9a87b-171">Generic Web Services:</span></span>
 * <span data-ttu-id="9a87b-172">Bij het wijzigen van de service-URL in standaard via de WebService-configuratieprogramma projecten SAP wsconfig en vervolgens de volgende fout gebeurt: kan een deel van het pad niet vinden</span><span class="sxs-lookup"><span data-stu-id="9a87b-172">When changing the service URL in Default SAP wsconfig projects through WebService Configuration Tool then the following error happens: Could not find a part of the path</span></span>

      ``'C:\Users\cstpopovaz\AppData\Local\Temp\2\e2c9d9b0-0d8a-4409-b059-dceeb900a2b3\b9bedcc0-88ac-454c-8c69-7d6ea1c41d17\cfg.config\cloneconfig.xml'. ``

* <span data-ttu-id="9a87b-173">Algemene LDAP:</span><span class="sxs-lookup"><span data-stu-id="9a87b-173">Generic LDAP:</span></span>
 * <span data-ttu-id="9a87b-174">GLDAP Connector ondersteunt niet alle kenmerken in AD LDS-raadpleegt u</span><span class="sxs-lookup"><span data-stu-id="9a87b-174">GLDAP Connector does not see all attributes in AD LDS</span></span>
 * <span data-ttu-id="9a87b-175">Wizard einden wanneer geen UPN-kenmerken worden gedetecteerd vanuit de LDAP-directory-schema</span><span class="sxs-lookup"><span data-stu-id="9a87b-175">Wizard breaks when no UPN attributes are detected from the LDAP directory schema</span></span>
 * <span data-ttu-id="9a87b-176">Delta-invoer is mislukt met detectie-fouten is niet aanwezig zijn tijdens de volledige import, als 'objectclass'-kenmerk niet is geselecteerd</span><span class="sxs-lookup"><span data-stu-id="9a87b-176">Delta Imports Failing with discovery errors not present during full import, when "objectclass" attribute is not selected</span></span>
 * <span data-ttu-id="9a87b-177">Een pagina van de configuratie 'Partities en hiërarchieën configureren' wordt niet weergegeven van alle objecten welk type gelijk is aan de partitie voor de nieuwe servers in de algemene</span><span class="sxs-lookup"><span data-stu-id="9a87b-177">A "Configure Partitions and Hierarchies” configuration page, doesn’t show any objects which type is equal to the partition for Novel servers in the Generic</span></span>  
<span data-ttu-id="9a87b-178">MA LDAP.</span><span class="sxs-lookup"><span data-stu-id="9a87b-178">LDAP MA.</span></span> <span data-ttu-id="9a87b-179">Ze hebt u geleerd alleen objecten van de RootDSE-partitie.</span><span class="sxs-lookup"><span data-stu-id="9a87b-179">They showed only objects from RootDSE partition.</span></span>


* <span data-ttu-id="9a87b-180">Algemene SQL:</span><span class="sxs-lookup"><span data-stu-id="9a87b-180">Generic SQL:</span></span>
 * <span data-ttu-id="9a87b-181">Herstel voor algemene SQL watermerk bug van Delta-Import-kenmerk met meerdere waarden niet worden geïmporteerd</span><span class="sxs-lookup"><span data-stu-id="9a87b-181">Fix for Generic SQL watermark Delta Import multivalued attribute not imported bug</span></span>
 * <span data-ttu-id="9a87b-182">Bij het exporteren van deleted\added waarden van het kenmerk met meerdere waarden, maar ze zijn geen deleted\added in gegevensbron.</span><span class="sxs-lookup"><span data-stu-id="9a87b-182">When exporting deleted\added values of multivalued attribute, they are not deleted\added in data source.</span></span>  


* <span data-ttu-id="9a87b-183">Lotus Notes:</span><span class="sxs-lookup"><span data-stu-id="9a87b-183">Lotus Notes:</span></span>
 * <span data-ttu-id="9a87b-184">Een bepaald veld 'Volledige naam' wordt weergegeven in de metaverse correct echter bij het exporteren naar de opmerkingen bij de waarde voor het kenmerk Null of leeg is.</span><span class="sxs-lookup"><span data-stu-id="9a87b-184">A specific field "Full Name" is shown in the metaverse correctly however when exporting to Notes the value for the attribute is Null or Empty.</span></span>
 * <span data-ttu-id="9a87b-185">Voor dubbele Certifier fout oplossen</span><span class="sxs-lookup"><span data-stu-id="9a87b-185">Fix for duplicate Certifier error</span></span>
 * <span data-ttu-id="9a87b-186">Als het Object zonder gegevens is ingeschakeld op de Lotus Domino-Connector met andere objecten ontvangt we de Discovery-fout tijdens het uitvoeren van volledige Import.</span><span class="sxs-lookup"><span data-stu-id="9a87b-186">When the Object without any data is selected on the Lotus Domino Connector with other objects then we receive the Discovery error while performing Full-Import.</span></span>
 * <span data-ttu-id="9a87b-187">Wanneer de Delta-Import wordt uitgevoerd op de Lotus Domino-Connector aan het einde van die wordt uitgevoerd, de Microsoft.IdentityManagement.MA.LotusDomino.Service.exe service soms retourneert een toepassingsfout.</span><span class="sxs-lookup"><span data-stu-id="9a87b-187">When Delta Import is being running on the Lotus Domino Connector, at the end of that run, the Microsoft.IdentityManagement.MA.LotusDomino.Service.exe service sometimes returns an Application Error.</span></span>
 * <span data-ttu-id="9a87b-188">Groep lidmaatschap algehele werkt goed samen en wordt onderhouden, behalve wanneer de export proberen te verwijderen van een gebruiker van het lidmaatschap wordt uitgevoerd als succesvol kunnen werken met een update te zien, maar de gebruiker niet daadwerkelijk ophalen verwijderd uit lidmaatschap van Lotus Notes.</span><span class="sxs-lookup"><span data-stu-id="9a87b-188">Group membership overall works fine and is maintained, except when running the export to try to remove a user from membership it shows as successful with an update, but the user doesn’t actually get removed from membership in Lotus Notes.</span></span>
 * <span data-ttu-id="9a87b-189">Een kans om de modus van uitvoer kiezen, zoals 'Append Item onderin' is toegevoegd in de configuratie GUI van Lotus MA nieuwe items onderin tijdens het exporteren voor kenmerken met meerdere waarden toevoegen.</span><span class="sxs-lookup"><span data-stu-id="9a87b-189">An opportunity to choose mode of export as “Append Item at bottom” was added in configuration GUI of Lotus MA to append new items at bottom during the export for multi-valued attributes.</span></span>
 * <span data-ttu-id="9a87b-190">Connector voegt de benodigde logica voor het bestand verwijderen uit de e-mailmap en ID-kluis.</span><span class="sxs-lookup"><span data-stu-id="9a87b-190">Connector will add the needed logic to delete the file from the Mail Folder and ID Vault.</span></span>
 * <span data-ttu-id="9a87b-191">Verwijderen van lidmaatschap voor cross-NAB lid niet werkt.</span><span class="sxs-lookup"><span data-stu-id="9a87b-191">Delete membership not working for cross NAB member.</span></span>
 * <span data-ttu-id="9a87b-192">Waarden moeten worden verwijderd uit een kenmerk met meerdere waarden</span><span class="sxs-lookup"><span data-stu-id="9a87b-192">Values should be successfully deleted from multi-valued attribute</span></span>

## <a name="111170"></a><span data-ttu-id="9a87b-193">1.1.117.0</span><span class="sxs-lookup"><span data-stu-id="9a87b-193">1.1.117.0</span></span>
<span data-ttu-id="9a87b-194">Uitgebracht: 2016 maart</span><span class="sxs-lookup"><span data-stu-id="9a87b-194">Released: 2016 March</span></span>

<span data-ttu-id="9a87b-195">**Nieuwe verbindingslijn**</span><span class="sxs-lookup"><span data-stu-id="9a87b-195">**New Connector**</span></span>  
<span data-ttu-id="9a87b-196">Initiële release van de [algemene SQL-Connector](active-directory-aadconnectsync-connector-genericsql.md).</span><span class="sxs-lookup"><span data-stu-id="9a87b-196">Initial release of the [Generic SQL Connector](active-directory-aadconnectsync-connector-genericsql.md).</span></span>

<span data-ttu-id="9a87b-197">**Nieuwe functies:**</span><span class="sxs-lookup"><span data-stu-id="9a87b-197">**New features:**</span></span>

* <span data-ttu-id="9a87b-198">Algemene LDAP-Connector:</span><span class="sxs-lookup"><span data-stu-id="9a87b-198">Generic LDAP Connector:</span></span>
  * <span data-ttu-id="9a87b-199">Ondersteuning toegevoegd voor de delta-import met Isode.</span><span class="sxs-lookup"><span data-stu-id="9a87b-199">Added support for delta import with Isode.</span></span>
* <span data-ttu-id="9a87b-200">Web Services-Connector:</span><span class="sxs-lookup"><span data-stu-id="9a87b-200">Web Services Connector:</span></span>
  * <span data-ttu-id="9a87b-201">Bijgewerkt in de csEntryChangeResult en setImportErrorCode activiteit om toe te staan fouten object terug naar de synchronisatie-engine wordt geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="9a87b-201">Updated the csEntryChangeResult activity and setImportErrorCode activity to allow object level errors to be returned back to the sync engine.</span></span>
  * <span data-ttu-id="9a87b-202">De SAP6 en SAP6User sjablonen voor het gebruik van de nieuwe functionaliteit van de object-fout op niveau wordt bijgewerkt.</span><span class="sxs-lookup"><span data-stu-id="9a87b-202">Updated the SAP6 and SAP6User templates to use the new object level error functionality.</span></span>
* <span data-ttu-id="9a87b-203">Lotus Domino-Connector:</span><span class="sxs-lookup"><span data-stu-id="9a87b-203">Lotus Domino Connector:</span></span>
  * <span data-ttu-id="9a87b-204">Voor het exporteren moet u één certifier per adresboek.</span><span class="sxs-lookup"><span data-stu-id="9a87b-204">For export, you need one certifier per address book.</span></span> <span data-ttu-id="9a87b-205">U kunt nu voor alle certifiers hetzelfde wachtwoord gebruiken om het beheer te vereenvoudigen.</span><span class="sxs-lookup"><span data-stu-id="9a87b-205">You can now use the same password for all certifiers to make the management easier.</span></span>

<span data-ttu-id="9a87b-206">**Opgeloste problemen:**</span><span class="sxs-lookup"><span data-stu-id="9a87b-206">**Fixed issues:**</span></span>

* <span data-ttu-id="9a87b-207">Algemene LDAP-Connector:</span><span class="sxs-lookup"><span data-stu-id="9a87b-207">Generic LDAP Connector:</span></span>
  * <span data-ttu-id="9a87b-208">Voor IBM Tivoli DS, sommige reference-kenmerken zijn niet correct is gedetecteerd.</span><span class="sxs-lookup"><span data-stu-id="9a87b-208">For IBM Tivoli DS, some reference attributes were not detected correctly.</span></span>
  * <span data-ttu-id="9a87b-209">Voor Open LDAP tijdens een delta-import zijn spaties aan het begin en einde van tekenreeksen afgekapt.</span><span class="sxs-lookup"><span data-stu-id="9a87b-209">For Open LDAP during a delta import, whitespaces at the beginning and end of strings were truncated.</span></span>
  * <span data-ttu-id="9a87b-210">Voor Novell en NetIQ hernoemd exporteren van een die een object tussen de organisatie-eenheden/containers en tegelijkertijd verplaatst het object is mislukt.</span><span class="sxs-lookup"><span data-stu-id="9a87b-210">For Novell and NetIQ, an export that moved an object between OUs/containers and at the same time renamed the object failed.</span></span>
* <span data-ttu-id="9a87b-211">Web Services-Connector:</span><span class="sxs-lookup"><span data-stu-id="9a87b-211">Web Services Connector:</span></span>
  * <span data-ttu-id="9a87b-212">Als de web-service meerdere eindpunten voor dezelfde binding heeft, is klikt u vervolgens de Connector niet correct detecteren deze eindpunten.</span><span class="sxs-lookup"><span data-stu-id="9a87b-212">If the web service had multiple end-points for same binding, then the Connector did not correctly discover these end-points.</span></span>
* <span data-ttu-id="9a87b-213">Lotus Domino-Connector:</span><span class="sxs-lookup"><span data-stu-id="9a87b-213">Lotus Domino Connector:</span></span>
  * <span data-ttu-id="9a87b-214">Exporteren van een van de volledige naam-kenmerk met een database mail in werkt niet.</span><span class="sxs-lookup"><span data-stu-id="9a87b-214">An export of the fullName attribute to a mail-in database did not work.</span></span>
  * <span data-ttu-id="9a87b-215">Exporteren van een die zowel toegevoegd en verwijderd lid uit een groep alleen de toegevoegde leden geëxporteerd.</span><span class="sxs-lookup"><span data-stu-id="9a87b-215">An export which both added and removed member from a group only exported the added members.</span></span>
  * <span data-ttu-id="9a87b-216">Als een Notes-Document is ongeldig (het kenmerk isValid ingesteld op false), is mislukt voor de Connector.</span><span class="sxs-lookup"><span data-stu-id="9a87b-216">If a Notes Document is invalid (the attribute isValid set to false), then the Connector fails.</span></span>

## <a name="older-releases"></a><span data-ttu-id="9a87b-217">Oudere versies</span><span class="sxs-lookup"><span data-stu-id="9a87b-217">Older releases</span></span>
<span data-ttu-id="9a87b-218">De Connectors zijn vóór maart 2016 uitgebracht als ondersteuning onderwerpen.</span><span class="sxs-lookup"><span data-stu-id="9a87b-218">Before March 2016, the Connectors were released as support topics.</span></span>

<span data-ttu-id="9a87b-219">**Algemene LDAP**</span><span class="sxs-lookup"><span data-stu-id="9a87b-219">**Generic LDAP**</span></span>

* <span data-ttu-id="9a87b-220">[KB3078617](https://support.microsoft.com/kb/3078617) -1.0.0597, September 2015</span><span class="sxs-lookup"><span data-stu-id="9a87b-220">[KB3078617](https://support.microsoft.com/kb/3078617) - 1.0.0597, 2015 September</span></span>
* <span data-ttu-id="9a87b-221">[KB3044896](https://support.microsoft.com/kb/3044896) -1.0.0549, van maart 2015</span><span class="sxs-lookup"><span data-stu-id="9a87b-221">[KB3044896](https://support.microsoft.com/kb/3044896) - 1.0.0549, 2015 March</span></span>
* <span data-ttu-id="9a87b-222">[KB3031009](https://support.microsoft.com/kb/3031009) -1.0.0534, januari 2015</span><span class="sxs-lookup"><span data-stu-id="9a87b-222">[KB3031009](https://support.microsoft.com/kb/3031009) - 1.0.0534, 2015 January</span></span>
* <span data-ttu-id="9a87b-223">[KB3008177](https://support.microsoft.com/kb/3008177) -1.0.0419, September 2014</span><span class="sxs-lookup"><span data-stu-id="9a87b-223">[KB3008177](https://support.microsoft.com/kb/3008177) - 1.0.0419, 2014 September</span></span>
* <span data-ttu-id="9a87b-224">[KB2936070](https://support.microsoft.com/kb/2936070) -4.3.1082, 2014 maart</span><span class="sxs-lookup"><span data-stu-id="9a87b-224">[KB2936070](https://support.microsoft.com/kb/2936070) - 4.3.1082, 2014 March</span></span>

<span data-ttu-id="9a87b-225">**WebServices**</span><span class="sxs-lookup"><span data-stu-id="9a87b-225">**WebServices**</span></span>

* <span data-ttu-id="9a87b-226">[KB3008178](https://support.microsoft.com/kb/3008178) -1.0.0419, September 2014</span><span class="sxs-lookup"><span data-stu-id="9a87b-226">[KB3008178](https://support.microsoft.com/kb/3008178) - 1.0.0419, 2014 September</span></span>

<span data-ttu-id="9a87b-227">**PowerShell**</span><span class="sxs-lookup"><span data-stu-id="9a87b-227">**PowerShell**</span></span>

* <span data-ttu-id="9a87b-228">[KB3008179](https://support.microsoft.com/kb/3008179) -1.0.0419, September 2014</span><span class="sxs-lookup"><span data-stu-id="9a87b-228">[KB3008179](https://support.microsoft.com/kb/3008179) - 1.0.0419, 2014 September</span></span>

<span data-ttu-id="9a87b-229">**Lotus Domino**</span><span class="sxs-lookup"><span data-stu-id="9a87b-229">**Lotus Domino**</span></span>

* <span data-ttu-id="9a87b-230">[KB3096533](https://support.microsoft.com/kb/3096533) -1.0.0597, September 2015</span><span class="sxs-lookup"><span data-stu-id="9a87b-230">[KB3096533](https://support.microsoft.com/kb/3096533) - 1.0.0597, 2015 September</span></span>
* <span data-ttu-id="9a87b-231">[KB3044895](https://support.microsoft.com/kb/3044895) -1.0.0549, van maart 2015</span><span class="sxs-lookup"><span data-stu-id="9a87b-231">[KB3044895](https://support.microsoft.com/kb/3044895) - 1.0.0549, 2015 March</span></span>
* <span data-ttu-id="9a87b-232">[KB2977286](https://support.microsoft.com/kb/2977286) -5.3.0712, 2014-augustus</span><span class="sxs-lookup"><span data-stu-id="9a87b-232">[KB2977286](https://support.microsoft.com/kb/2977286) - 5.3.0712, 2014 August</span></span>
* <span data-ttu-id="9a87b-233">[KB2932635](https://support.microsoft.com/kb/2932635) -5.3.1003, februari 2014</span><span class="sxs-lookup"><span data-stu-id="9a87b-233">[KB2932635](https://support.microsoft.com/kb/2932635) - 5.3.1003, 2014 February</span></span>  
* <span data-ttu-id="9a87b-234">[KB2899874](https://support.microsoft.com/kb/2899874) -5.3.0721, oktober 2013</span><span class="sxs-lookup"><span data-stu-id="9a87b-234">[KB2899874](https://support.microsoft.com/kb/2899874) - 5.3.0721, 2013 October</span></span>
* <span data-ttu-id="9a87b-235">[KB2875551](https://support.microsoft.com/kb/2875551) -5.3.0534, 2013-augustus</span><span class="sxs-lookup"><span data-stu-id="9a87b-235">[KB2875551](https://support.microsoft.com/kb/2875551) - 5.3.0534, 2013 August</span></span>

## <a name="next-steps"></a><span data-ttu-id="9a87b-236">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="9a87b-236">Next steps</span></span>
<span data-ttu-id="9a87b-237">Meer informatie over de [Azure AD Connect-synchronisatie](active-directory-aadconnectsync-whatis.md) configuratie.</span><span class="sxs-lookup"><span data-stu-id="9a87b-237">Learn more about the [Azure AD Connect sync](active-directory-aadconnectsync-whatis.md) configuration.</span></span>

<span data-ttu-id="9a87b-238">Lees meer over het [integreren van uw on-premises identiteiten met Azure Active Directory ](active-directory-aadconnect.md).</span><span class="sxs-lookup"><span data-stu-id="9a87b-238">Learn more about [Integrating your on-premises identities with Azure Active Directory](active-directory-aadconnect.md).</span></span>

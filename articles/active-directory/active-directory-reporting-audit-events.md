---
title: Active Directory-controlerapportgebeurtenissen aaaAzure | Microsoft Docs
description: Gebeurtenissen die beschikbaar zijn voor het weergeven en downloaden van uw Azure Active Directory controleren
services: active-directory
documentationcenter: 
author: dhanyahk
manager: femila
editor: 
ms.assetid: 307eedf7-05bc-448d-a84d-bead5a4c5770
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 06/16/2017
ms.author: dhanyahk;markvi
ms.openlocfilehash: 4a84cce2be56bde006164abf10ad1e72ca6e99bf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-audit-report-events"></a>Auditrapport gebeurtenissen Azure Active Directory
*Deze documentatie maakt deel uit van Hallo [Azure Active Directory Reporting Guide](active-directory-reporting-guide.md).*

Hello Azure Active Directory-controlerapport helpt klanten bevoorrechte acties die is opgetreden in Azure Active Directory identificeren. Bevoegdheden omvatten wijzigingen van de uitbreiding van bevoegdheden (bijvoorbeeld het maken of opnieuw instellen van wachtwoorden), het wijzigen van beleidsconfiguraties (bijvoorbeeld wachtwoordbeleid) of wijzigingen toodirectory configuratie (bijvoorbeeld wijzigingen toodomain federation instellingen). Hallo-rapporten geven Hallo controlerecord voor gebeurtenisnaam hello, Hallo actor die Hallo actie, Hallo doelbron beïnvloed door wijziging van de Hallo en Hallo datum en tijd (in UTC) heeft uitgevoerd. Klanten kunnen tooretrieve Hallo lijst van de controlegebeurtenissen voor Azure Active Directory via Hallo zijn [Azure Portal](https://portal.azure.com/), zoals beschreven in [uw logboeken Audit](active-directory-reporting-azure-portal.md).

## <a name="list-of-audit-report-events"></a>Lijst met Controlerapportgebeurtenissen
<!--- audit event descriptions should be in hello past tense --->

| Gebeurtenissen | Beschrijving van gebeurtenis |
| --- | --- |
| **Gebeurtenissen van gebruikers** | |
| Gebruiker toevoegen |Een gebruiker toohello directory toegevoegd. |
| Gebruiker verwijderen |Een gebruiker verwijderd uit Hallo directory. |
| Licentie-eigenschappen instellen |Hallo licentie-eigenschappen ingesteld voor een gebruiker in Hallo directory. |
| Gebruiker-wachtwoord opnieuw instellen |Wachtwoord voor een gebruiker in de directory Hallo Hallo opnieuw instellen. |
| Gebruiker-wachtwoord wijzigen |Wachtwoord voor een gebruiker in de directory Hallo Hallo gewijzigd. |
| De gebruikerslicentie wijzigen |Hallo-licentie toegewezen tooa Hallo-directory-gebruiker gewijzigd. welke licenties zijn bijgewerkt, zoekt u naar op Hallo toosee [Update gebruiker](#update-user-attributes) onderstaande eigenschappen |
| Gebruiker bijwerken |Een gebruiker in Hallo directory bijgewerkt. [Zie hieronder](#update-user-attributes) voor kenmerken die kunnen worden bijgewerkt. |
| Force wijziging gebruiker-wachtwoord instellen |Hallo-eigenschap dat ervoor zorgt een gebruiker toochange dat hun wachtwoord aanmelden instellen. |
| Gebruikersreferenties updaten |Wachtwoord van gebruiker gewijzigde Hallo |
| **Gebeurtenissen groeperen** | |
| Groep toevoegen |Een groep in Hallo directory gemaakt. |
| Groep bijwerken |Een groep in Hallo directory bijgewerkt. welke eigenschappen zijn bijgewerkt, toosee te verwijzen[groep eigenschappen gecontroleerd](#update-group-attributes) in onderstaande Hallo-sectie |
| Groep verwijderen |Een groep verwijderd uit Hallo directory. |
| CreateGroupSettings |Gemaakte groepsinstellingen |
| UpdateGroupSettings |Groepsbeleidsinstellingen bijgewerkt. welke instellingen zijn bijgewerkt, toosee te verwijzen[groep eigenschappen gecontroleerd](#update-group-attributes) in onderstaande Hallo-sectie |
| DeleteGroupSettings |Instellingen van de verwijderde groep |
| SetGroupLicense |Groepslicentie ingesteld. |
| SetGroupManagedBy |Groep toobe beheerd door de gebruiker instellen |
| AddGroupMember |Toogroup lid is toegevoegd |
| RemoveGroupMember |Lid verwijderen uit groep |
| AddGroupOwner |De eigenaar van de toegevoegde toogroup |
| RemoveGroupOwner |Verwijderde eigenaar van groep |
| **Toepassingsgebeurtenissen** | |
| Service-principal toevoegen |Een service-principal toohello directory toegevoegd. |
| Service-principal verwijderen |Een service-principal verwijderd van Hallo directory. |
| Service-principal referenties toevoegen |Toegevoegde referenties tooa service-principal. |
| Service-principal referenties verwijderen |De referenties van een service-principal is verwijderd. |
| Overdracht vermelding toevoegen |Gemaakt een [OAuth2PermissionGrant](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/entity-and-complex-type-reference#oauth2permissiongrant-entity) in Hallo-directory. |
| Set delegering vermelding |Bijgewerkt een [OAuth2PermissionGrant](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/entity-and-complex-type-reference#oauth2permissiongrant-entity) in Hallo-directory. |
| Verwijder de vermelding overdracht |Verwijderde een [OAuth2PermissionGrant](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/entity-and-complex-type-reference#oauth2permissiongrant-entity) in Hallo-directory. |
| **Gebeurtenissen van de rol** | |
| Rol lid tooRole toevoegen |Een gebruikersrol voor tooa directory toegevoegd. |
| Rollid verwijderen uit rol |Een gebruiker verwijderd vanuit een functie directory. |
| AddRoleDefinition |Toegevoegde roldefinitie. |
| UpdateRoleDefinition |Roldefinitie bijgewerkt. welke rolinstellingen zijn bijgewerkt, toosee te verwijzen[rol definitie eigenschappen gecontroleerd](#update-role-definition-attributes) in onderstaande Hallo-sectie |
| DeleteRoleDefinition |Roldefinitie verwijderd. |
| AddRoleAssignmentToRoleDefinition |Roldefinitie toewijzing toorole toegevoegd. |
| RemoveRoleAssignmentFromRoleDefinition |De roltoewijzing is verwijderd van de roldefinitie. |
| AddRoleFromTemplate |De rol van sjabloon is toegevoegd. |
| UpdateRole |Bijgewerkte rol. |
| AddRoleScopeMemberToRole |Bereik van lid toorole toegevoegd. |
| RemoveRoleScopedMemberFromRole |Bereik van lid verwijderd van de rol. |
| **Apparaatgebeurtenissen (alle nieuwe gebeurtenissen)** | |
| AddDevice |Toegevoegd apparaat. |
| UpdateDevice |Bijgewerkte apparaten. de eigenschappen van welke apparaten zijn bijgewerkt, toosee te verwijzen[apparaateigenschappen Audited](#update-device-attributes) in onderstaande Hallo-sectie |
| DeleteDevice |Het apparaat verwijderd. |
| AddDeviceConfiguration |Configuratie van het apparaat. |
| UpdateDeviceConfiguration |Bijgewerkte apparaatconfiguratie. welke configuratie-eigenschappen van het apparaat zijn bijgewerkt, toosee te verwijzen[configuratie apparaateigenschappen Audited](#update-device-configuration-attributes) in onderstaande Hallo-sectie |
| DeleteDeviceConfiguration |Apparaatconfiguratie van het verwijderd. |
| AddRegisteredOwner |Geregistreerde eigenaar toodevice toegevoegd. |
| AddRegisteredUsers |Geregistreerde gebruikers toodevice toegevoegd. |
| RemoveRegisteredOwner |Verwijder geregistreerde eigenaar van apparaat. |
| RemoveRegisteredUsers |Verwijder geregistreerde gebruikers van apparaat. |
| RemoveDeviceCredentials |Apparaat-referenties verwijderen. |
| **B2B-gebeurtenissen** | |
| Batch nodigt geüpload. |Een beheerder is een bestand met uitnodigingen toobe toopartner gebruikers verzonden geüpload. |
| Batch nodigt verwerkt. |Een bestand met uitnodigingen toopartner gebruikers is verwerkt. |
| Externe gebruiker uitnodigen. |Een externe gebruiker is uitgenodigde toohello directory. |
| Externe gebruiker uitnodiging inwisselen. |De uitnodiging toohello directory, een externe gebruiker is gebruikt. |
| Externe gebruiker toogroup toevoegen. |Een externe gebruiker is toegewezen tooa lidmaatschapsgroep in Hallo-directory. |
| Externe gebruiker tooapplication toewijzen. |Een externe gebruiker is directe toegang tooan toepassing toegewezen. |
| Het maken van een tenant. |Een nieuwe tenant is gemaakt in Azure AD door Hallo uitnodiging inwisseling. |
| Het maken van een gebruiker. |Een gebruiker is gemaakt in een bestaande tenant in Azure AD door Hallo uitnodiging inwisseling. |
| **Administratieve eenheden (alle nieuwe gebeurtenissen)** | |
| AddAdministrativeUnit |Administratieve eenheden toevoegen. |
| UpdateAdministrativeUnit |Administratieve eenheid bijwerken. welke eigenschappen administratieve eenheid zijn bijgewerkt, toosee te verwijzen[beheereigenschappen van eenheid, gecontroleerd](#update-administrative-unit-attributes) in onderstaande Hallo-sectie |
| DeleteAdministrativeUnit |Administratieve eenheden verwijderen. |
| AddMemberToAdministrativeUnit |Lid tooadministrative eenheid toevoegen. |
| RemoveMemberFromAdministrativeUnit |Lid verwijderen uit de administratieve eenheid. |
| **Directory-gebeurtenissen** | |
| Partner toocompany toevoegen |Een partner toohello directory toegevoegd. |
| Partner verwijderen van bedrijf |Een partner verwijderd van Hallo directory. |
| DemotePartner |Partner degraderen. |
| Domein toocompany toevoegen |Een domein toohello directory toegevoegd. |
| Domein verwijderen van bedrijf |Een domein verwijderd uit Hallo directory. |
| Bijwerken van domein |Een domein op Hallo directory bijgewerkt. welke eigenschappen van het domein zijn bijgewerkt, toosee te verwijzen[Domeineigenschappen gecontroleerd](#update-domain-attributes) in onderstaande Hallo-sectie |
| Domein-verificatie instellen |Hallo standaard domeininstelling voor Hallo bedrijf gewijzigd. |
| Instellen van de contactgegevens van bedrijf |Niveau van het bedrijf contactvoorkeuren ingesteld. Dit omvat de e-mailadressen voor marketing, evenals technische meldingen over de Microsoft Online Services. |
| Instellingen voor het federatieve domein |Bijgewerkte Hallo federation-instellingen voor een domein. |
| Domein verifiëren |Een domein op Hallo directory gecontroleerd. |
| Controleer of de geverifieerde e-maildomein |Een domein op Hallo directory met behulp van e-mailverificatie gecontroleerd. |
| DirSyncEnabled-vlag ingesteld op het bedrijf |Hallo-eigenschap waarmee een map voor Azure AD-synchronisatie instellen. |
| Wachtwoordbeleid instellen |De lengte en teken beperkingen voor wachtwoorden van gebruikers instellen. |
| Bedrijfsgegevens instellen |Bijgewerkte Hallo niveau van het bedrijf informatie. Zie Hallo [Get-MsolCompanyInformation](https://msdn.microsoft.com/library/azure/dn194126.aspx) PowerShell-cmdlet voor meer informatie. |
| SetCompanyAllowedDataLocation |Set bedrijf gegevenslocatie toegestaan. |
| SetCompanyDirSyncEnabled |DirSyncEnabled vlag worden ingesteld. |
| SetCompanyDirSyncFeature |Stel DirSync-functie. |
| SetCompanyInformation |Set-bedrijfsinformatie. |
| SetCompanyMultiNationalEnabled |Stel bedrijf meertalige functie is ingeschakeld. |
| SetDirectoryFeatureOnTenant |Functie van de directory niet instellen op de tenant. |
| SetTenantLicenseProperties |Tenant-licentie-eigenschappen worden ingesteld. |
| CreateCompanySettings |Bedrijfsinstellingen maken |
| UpdateCompanySettings |Werk de instellingen van het bedrijf. welke eigenschappen van het bedrijf zijn bijgewerkt, toosee te verwijzen[bedrijf eigenschappen gecontroleerd](#update-company-attributes) in onderstaande Hallo-sectie |
| DeleteCompanySettings |Bedrijfsinstellingen verwijderen |
| SetAccidentalDeletionThreshold |Drempelwaarde voor onopzettelijk verwijderen ingesteld. |
| SetRightsManagementProperties |Rights management-eigenschappen instellen. |
| PurgeRightsManagementProperties |Opschonen van rights management-eigenschappen. |
| UpdateExternalSecrets |Externe geheimen bijwerken |
| **Beleidsgebeurtenissen (alle nieuwe gebeurtenissen)** | |
| AddPolicy |Beleid toevoegen. |
| UpdatePolicy |Beleid bijwerken. |
| DeletePolicy |Beleid verwijderen. |
| AddDefaultPolicyApplication |Beleid tooapplication toevoegen. |
| AddDefaultPolicyServicePrincipal |Beleid tooservice principal toevoegen. |
| RemoveDefaultPolicyApplication |Beleid van toepassing verwijderen. |
| RemoveDefaultPolicyServicePrincipal |Beleid verwijderen uit de service-principal. |
| RemovePolicyCredentials |Verwijder de beleid-referenties. |

## <a name="audit-report-retention"></a>Audit rapport bewaren

Zie voor meest recente informatie over bewaren Hallo [bewaarbeleid voor Azure Active Directory-rapport](active-directory-reporting-retention.md).


Voor klanten die de bij het opslaan van de controlegebeurtenissen voor langere bewaartermijn, kan hello rapportage-API worden gebruikt tooregularly pull-controlegebeurtenissen in een afzonderlijke gegevensarchief. Zie [rapportage-API aan de slag met Hallo](active-directory-reporting-api-getting-started.md) voor meer informatie.

## <a name="properties-included-with-each-audit-event"></a>Eigenschappen die deel uitmaakt van elke controlegebeurtenis
| Eigenschap | Beschrijving |
| --- | --- |
| Datum en tijd |Hallo-datum en tijd waarop Hallo controlegebeurtenis is opgetreden |
| Actor |Hallo-gebruiker of service-principal die Hallo actie is uitgevoerd |
| Actie |Hallo-actie die is uitgevoerd |
| doel |Hallo-gebruiker of service-principal Hallo actie is uitgevoerd op |

## <a name="update-user-attributes"></a>'Gebruiker bijwerken' kenmerken
Hallo-Update 'gebruiker' controlegebeurtenis bevat aanvullende informatie over welke gebruikerskenmerken zijn bijgewerkt. Voor elk kenmerk beide vorige waarde Hallo en de nieuwe waarde Hallo is opgenomen.

| Kenmerk | Beschrijving |
| --- | --- |
| accountEnabled |Hallo-gebruiker kunt aanmelden. |
| AssignedLicense |Alle licenties die zijn toegewezen aan gebruiker toohello. |
| AssignedPlan |Service-abonnementen die voortvloeien uit Hallo licenties toohello gebruiker toegewezen. |
| LicenseAssignmentDetail |Meer informatie over licenties toohello gebruiker toegewezen. Bijvoorbeeld, als er op basis van een groep-licentieverlening is betrokken, omvat dit Hallo-groep die verleend Hallo licentie. |
| Mobiele telefoon |Hallo van de gebruiker mobiele telefoon. |
| OtherMail |Hallo alternatief e-mailadres van de gebruiker. |
| OtherMobile |Hallo van gebruiker alternatieve mobiele telefoon. |
| StrongAuthenticationMethod |Een lijst met verificatiemethoden die zijn geconfigureerd door de gebruiker Hallo voor meervoudige verificatie, zoals telefoongesprek, SMS of verificatie van de code van een mobiele app. |
| StrongAuthenticationRequirement |Als multi-factor Authentication wordt afgedwongen, ingeschakeld of uitgeschakeld voor deze gebruiker. |
| StrongAuthenticationUserDetails |Hallo van de gebruiker telefoon getal, alternatieve telefoonnummer en e-adres gebruikt voor verificatie met meerdere factoren en verificatie voor wachtwoord opnieuw instellen. |
| StrongAuthenticationPhoneAppDetail |Detail forof phone-apps geregistreerd tooperform 2FA aanmelding |
| telephoneNumber |het telefoonnummer van de gebruiker Hallo. |
| AlternativeSecurityId |Een alternatieve beveiligings-ID voor het Hallo-object. |
| CreationType |Methode voor het maken van Hallo gebruiker (hetzij door een uitnodiging voor een). |
| InviteTicket |Lijst met uitnodiging tickets voor Hallo-gebruiker. |
| InviteReplyUrl |Lijst met URL's tooreply na ontvangst van de uitnodiging. |
| InviteResources |Lijst met resources toowhich Hallo gebruiker heeft uitgenodigd. |
| LastDirSyncTime |Tijd laatste hello object is bijgewerkt vanwege gesynchroniseerd vanaf Hallo gezaghebbende (klant, on-premises) directory. |
| MSExchRemoteRecipientType |Toegewezen tooMSO geadresseerde typen. Raadpleeg te https://msdn.microsoft.com/library/microsoft.office.interop.outlook.recipient.type.aspx voor geadresseerden typen [MSO geadresseerde typen] |
| PreferredDataLocation |Hallo gewenste locatie voor Hallo van de gebruiker, van de groep, van de contactpersoon, openbare map, of gegevens van het apparaat. |
| ProxyAddresses |Hallo-adres waarmee een ontvanger Exchange Server-object in een extern e-mailsysteem wordt herkend. |
| StsRefreshTokensValidFrom |Uitvoert vernieuwen token intrekkingsgegevens - eventuele STS vernieuwen van tokens verleend voordat dit moment worden beschouwd als verlopen. |
| UserPrincipalName |Hallo UPN die is een aanmeldingsnaam voor Internet-stijl voor een gebruiker. |
| UserState |Status van de gebruiker PendingApproval/PendingAcceptance/geaccepteerd/PendingVerification. |
| UserStateChangedOn |De tijdstempel van laatste wijziging tooUserState. Tootrigger lifecycle werkstromen gebruikt. |
| UserType |Type gebruiker. Lid (0), Gast (1), Viral(2). |

## <a name="update-group-attributes"></a>De kenmerken 'Updategroep'
| Kenmerk | Beschrijving |
| --- | --- |
| Classificatie |Hallo-classificatie voor een groep Unified (HBI, MBI, enzovoort). |
| Beschrijving |Leesbare beschrijvende zinnen over Hallo-object. |
| Weergavenaam |Hallo weergavenaam voor een object |
| DirSyncEnabled |Geeft aan of de synchronisatie van een bindende plaatsvindt (klant, on-premises)-directory. |
| GroupLicenseAssignment |De licentietoewijzing van een groep |
| groupType |Type groep, Unified (0) |
| IsMembershipRuleLocked |Geeft aan dat Hallo MembershipRule-eigenschap is ingesteld door Hallo groepsbeheer met Self-Service management-service en kan niet worden gewijzigd door gebruikers. Van toepassing alleen toogroups waarbij GroupType GroupType.DynamicMembership bevat |
| IsPublic |Vlag tooindicate als Hallo groep openbaar/persoonlijk is. |
| LastDirSyncTime |Tijd laatste hello object is bijgewerkt als gevolg van het synchroniseren van Hallo gezaghebbende (on-premises klant) directory. |
| Mail |Primaire e-mailadres |
| MailEnabled |Geeft aan of deze groep e-functionaliteit. |
| mailNickname |Moniker voor een adres adresboek object, doorgaans Hallo-gedeelte van de e-mailnaam voorgaande Hallo ' @ ' symbool. |
| MembershipRule |Een tekenreeks uitdrukken Hallo criteria door Hallo groepsbeheer met Self-Service management service toodetermine welke leden, behoren toothis groep tot moeten gebruikt. Zie ook IsMembershipRuleLocked. Alleen van toepassing toogroups waarbij GroupType GroupType.DynamicMembership bevat. |
| MembershipRuleProcessingState |Een enum-waarde die wordt gedefinieerd door Hallo management-service voor groepsbeheer met Self-service Hallo status van het lidmaatschap verwerking voor deze groep te definiëren. Alleen van toepassing toogroups waarbij GroupType GroupType.DynamicMembership bevat. |
| ProxyAddresses |Hallo-adres waarmee een ontvanger Exchange Server-object in een extern e-mailsysteem wordt herkend. |
| RenewedDateTime |De registratie van de tijdstempel van wanneer een groep voor het laatst is vernieuwd. |
| securityenabled moet |Hiermee wordt aangegeven of lidmaatschap van groep Hallo autorisatiebeslissingen kan beïnvloeden. |
| WellKnownObject |Een Active directory-object, het toewijzen als een van de vooraf gedefinieerde als label. |

## <a name="update-device-attributes"></a>'Apparaat bijwerken' kenmerken
| Kenmerk | Beschrijving |
| --- | --- |
| accountEnabled |Hiermee wordt aangegeven of een beveiligings-principal kan worden geverifieerd. |
| CloudAccountEnabled |Hiermee wordt aangegeven of een beveiligings-principal kan worden geverifieerd. Geschreven door InTune bij het Hallo-apparaat heeft als master on-premises. |
| CloudDeviceOSType |Het type apparaat dat Hallo op basis van Hallo OS bijvoorbeeld Windows RT, iOS. Als de waarde door een cloudservice (zoals Intune), wordt dit kenmerk in de map Hallo gezaghebbende voor DeviceOSType. |
| CloudDeviceOSVersion |Versie van Hallo OS. Als de waarde door een cloudservice (zoals Intune), wordt dit kenmerk in de map Hallo gezaghebbende voor DeviceOSVersion. |
| CloudDisplayName |De waarde van Hallo displayName LDAP-kenmerk. Dit kenmerk wordt als de waarde door een cloudservice (zoals Intune), in de directory Hallo voor displayName gezaghebbende. |
| CloudCreated |Hiermee wordt aangegeven of het Hallo-object is gemaakt met cloudservices. |
| CompliantUntil |Tot welk tijdstip wordt apparaat als compatibel beschouwd. |
| DeviceMetadata |Aangepaste metagegevens voor Hallo-apparaat |
| DeviceObjectVersion |Dit kenmerk is gebruikte tooidentify Hallo schemaversie van Hallo-apparaat. |
| DeviceOSType |Het type apparaat dat Hallo op basis van Hallo OS bijvoorbeeld Windows RT, iOS. Geschreven door hello Registration-Service en de beoogde toobe bijgewerkt door Hallo MDM-management-service of STS licht management-service. |
| DeviceOSVersion |Versie van Hallo OS. Geschreven door hello Registration-Service en de beoogde toobe bijgewerkt door Hallo MDM-management-service of STS licht management-service. |
| DevicePhysicalIds |Kenmerk met meerdere waarden bedoeld toostore-id's van het fysieke apparaat Hallo. Dit kan ook BIOS-id's, TPM vingerafdrukken, hardware-specifieke id's, enzovoort. |
| DirSyncEnabled |Geeft aan of de synchronisatie van een bindende (klant, on-premises plaatsvindt) directory. |
| Weergavenaam |Hallo weergavenaam voor een object |
| IsCompliant |Dit kenmerk is gebruikte toomanage Hallo mobiele apparaat management status van Hallo-apparaat. |
| IsManaged |Dit kenmerk wordt gebruikt tooindicate Hallo apparaat wordt beheerd door een MDM-cloud |
| LastDirSyncTime |Tijd laatste hello object is bijgewerkt vanwege gesynchroniseerd vanaf Hallo gezaghebbende (on-premises klant) directory. |

## <a name="update-device-configuration-attributes"></a>Kenmerken 'Bijwerken apparaatconfiguratie'
| Kenmerk | Beschrijving |
| --- | --- |
| MaximumRegistrationInactivityPeriod |maximum aantal dagen Hallo een apparaat inactief mag zijn voordat deze is verwijderd. |
| RegistrationQuota |Beleid voor toolimit Hallo aantal apparaat registraties toegestaan voor één gebruiker gebruikt. |

## <a name="update-service-principal-configuration-attributes"></a>'De configuratie van de Service-principal bijwerken' kenmerken
| Kenmerk | Beschrijving |
| --- | --- |
| accountEnabled |Hiermee wordt aangegeven of een beveiligings-principal kan worden geverifieerd. |
| AppPrincipalId |Externe, toepassingsspecifieke identiteit voor een beveiligings-principal. |
| Weergavenaam |Hallo weergavenaam voor een object |
| ServicePrincipalName |Een service principal name "naam/authority" waarbij naam geeft u een waarde van de klasse toepassing en de autoriteit bevat ten minste met hostnaam [: poort] of 'name' die een id voor de service-principal Hallo aangeeft. |

## <a name="update-app-attributes"></a>Kenmerken 'App bijwerken'
| Kenmerk | Beschrijving |
| --- | --- |
| AppAddress |Hallo set adressen (Omleidings-URL's) die zijn toegewezen tooa service-principal. |
| AppId |Toepassings-ID van Hallo App |
| AppIdentifierUri |Een toepassing URI, die toepassing hello te identificeren.  Meestal is het Hallo toegangs-URL van toepassing. |
| AppLogoUrl |Hallo-url voor Hallo toepassing logo installatiekopie is opgeslagen in een CDN. |
| AvailableToOtherTenants |True Hallo toepassing is multitenant (dat wil zeggen kunnen worden gebruikt door andere tenants). |
| Weergavenaam |Hallo weergavenaam voor een toepassingsnaam in |
| Recht |Lijst met rechten van de toepassing. |
| ExternalUserAccountDelegationsAllowed |Markering die aangeeft of de resource-toepassing een vertrouwde is en overdrachtvermeldingen voor de externe gebruikersaccounts kunt maken. |
| GroupMembershipClaims |Hallo lidmaatschap claims Groepsbeleid. |
| PublicClient |True als het Hallo-client kan geen geheime houden (d.w.z. niet-vertrouwelijke client in OAuth2.0) |
| RecordConsentConditions |Soorten toestemming voorwaarden, zoals gedefinieerd door Hallo contract voorwaarden: geen (0), SilentConsentForPartnerManagedApp(1). Deze waarde zal worden weergegeven in Hallo Graph API schema en kan alleen worden ingesteld of gewijzigd door tenantbeheerders. |
| RequiredResourceAccess |XML-inhoud van een waarde van Hallo RequiredResourceAccess-eigenschap. |
| De Web-App |Indien waar, geeft aan dat deze toepassing een web-app. |
| WwwHomepage |Hallo primaire webpagina. |

## <a name="update-role-attributes"></a>Kenmerken voor 'Rol bijwerken'
| Kenmerk | Beschrijving |
| --- | --- |
| AppAddress |Hallo set adressen (Omleidings-URL's) die zijn toegewezen tooa service-principal. |
| BelongsToFirstLoginObjectSet |Indien waar, geeft u aan dat dit object toohello set van objecten vereist tooenable aanmelding van de eerste admin Hallo van een nieuwe tenant hoort. |
| Ingebouwd |Hiermee wordt aangegeven of Hallo levensduur van een object is eigendom van Hallo-systeem. |
| Beschrijving |Leesbare beschrijvende zinnen over Hallo-object. |
| Weergavenaam |Hallo weergavenaam voor een object |
| mailNickname |Moniker voor een adres adresboek object, doorgaans Hallo-gedeelte van de e-mailnaam voorgaande Hallo ' @ ' symbool. |
| RoleDisabled |Hiermee wordt aangegeven of Hallo rol ten behoeve van de toegangscontrole moet worden genegeerd. |
| RoleTemplateId |Identiteit van de sjabloon voor Hallo-rol. |
| ServiceInfo |Service-specifieke informatie die kan worden gebruikt door MOAC en/of andere service-exemplaren voor het inrichten (Hallo dezelfde of verschillende typen service). |
| TaskSetScopeReference |Identificeert een TaskSet en een set met bereiken die zijn gekoppeld aan een functie of RoleTemplate. |
| ValidationError |Gegevens die zijn gepubliceerd door een federatieve service met een beschrijving van een tijdelijke, servicespecifieke fout met betrekking tot Hallo eigenschappen of koppeling van een object beheerder actie tooresolve. |
| WellKnownObject |Een Active directory-object, het toewijzen als een van de vooraf gedefinieerde als label. |

## <a name="update-role-definition-attributes"></a>Kenmerken 'Bijwerken roldefinitie'
| Kenmerk | Beschrijving |
| --- | --- |
| AssignableScopes |Verzameling van autorisatie-scopes die bij het toewijzen van deze RoleDefinition tooa beveiligings-principal kan worden verwezen. |
| Weergavenaam |Hallo weergavenaam voor een object |
| GrantedPermissions |Machtigingen verleend door deze RoleDefinition. |

## <a name="update-administrative-unit-attributes"></a>Kenmerken 'Bijwerken administratieve eenheid'
| Kenmerk | Beschrijving |
| --- | --- |
| Beschrijving |Deze eigenschap wordt bijgewerkt wanneer u Hallo beschrijving van een administratieve eenheid wijzigen. |
| Weergavenaam |Deze eigenschap wordt bijgewerkt wanneer u Hallo-naam van een administratieve eenheid wijzigen. |

## <a name="update-company-attributes"></a>De kenmerken 'Bedrijf bijwerken'
| Kenmerk | Beschrijving |
| --- | --- |
| AllowedDataLocation |Een locatie in welke Hallo van bedrijf gebruikers toobe ingericht zijn toegestaan. |
| AuthorizedServiceInstance |Namen van de service-exemplaren toowhich die een plan kan worden geïmplementeerd. |
| DirSyncEnabled |Geeft aan of de synchronisatie van een bindende (klant, on-premises plaatsvindt) directory. |
| DirSyncStatus |Geeft aan of de synchronisatie van adres adresboek objecten in deze context tenant van een bindende (klant, on-premises) plaatsvindt directory; een uitbreiding van Hallo DirSyncEnabled-eigenschap op objecten van de bedrijfsportal. |
| DirSyncFeatures |Bits vlag tookeep bijhouden van set met ingeschakelde als uitgeschakelde dirsync-functies voor Hallo-tenant. |
| DirectoryFeatures |Directoryfuncties voor ingeschakeld/uitgeschakeld. |
| DirSyncConfiguration |Bevat alle DirSync-configuratie specifieke toohello huidige tenant. |
| Weergavenaam |Hallo weergavenaam voor een object |
| IsMnc |Een Booleaanse vlag set iff te 'true' hello bedrijf is Hallo meertalige bedrijf functie ingeschakeld. |
| ObjectSettings |Een verzameling instellingen van toepassing toohello bereik van Hallo-object. |
| PartnerCommerceUrl |URL toohello Partner commercesite. |
| PartnerHelpUrl |URL toohello Partner help-site. |
| PartnerSupportEmail |URL toohello Partner ondersteuning e-mailbericht. |
| PartnerSupportTelephone |URL toohello Partner ondersteuning telefoon. |
| PartnerSupportUrl |URL toohello Partner ondersteuningssite. |
| StrongAuthenticationDetails |Verwante tooStrongAuthentication voor meer informatie. |
| StrongAuthenticationPolicy |Beleid voor sterke verificatie voor Hallo bedrijf. |
| TechnicalNotificationMail |E-mailadres toonotify technische problemen tooa bedrijf die betrekking hebben. |
| telephoneNumber |Telefoonnummers die aan de Hallo ITU aanbeveling E.123 voldoen. |
| TenantType |Hallo-type van een tenant. Als deze waarde niet is opgegeven, is Hallo tenant een bedrijf. Anders wordt de mogelijke waarden zijn: MicrosoftSupport (0), SyndicatePartner (1), (2) BreadthPartner BreadthPartnerDelegatedAdmin (3) ResellerPartnerDelegatedAdmin (4) ValueAddedResellerPartnerDelegatedAdmin (5). |
| VerifiedDomain |Een set van DNS-domeinnamen gebonden tooa bedrijf. |

## <a name="update-domain-attributes"></a>Kenmerken 'Bijwerken domein'
| Kenmerk | Beschrijving |
| --- | --- |
| Functionaliteit |Bits vlaggen beschrijving Hallo-mogelijkheden van Hallo-domein, indien van toepassing. |
| Standaard |Hiermee wordt aangegeven of Hallo domein Hallo-standaardwaarde. bijvoorbeeld, Hallo standaard UserPrincipalName achtervoegsel wanneer een beheerder een nieuwe gebruiker in MOAC maakt. |
| Initiële |Geeft aan of Hallo domein Hallo eerste domein voor Hallo bedrijf, zoals toegewezen door OCP. Hallo eerste domein is een unieke subdomeinnaam van een Microsoft Online-domein. e.g.contoso3.microsoftonline.com. |
| LiveType |Type Hallo corresponderende Windows Live naamruimte, indien van toepassing. |
| Naam |ID voor het Hallo-eindpunt. |
| PasswordNotificationWindowDays |Hallo aantal dagen voordat een wachtwoord Hallo gebruiker verloopt ontvangt een melding. |
| PasswordValidityPeriodDays |Hallo aantal dagen dat een wachtwoord is geschikt voor voordat moet worden gewijzigd. |

Controlerecords zijn vereiste besturingselement voor veel nalevingsvoorschriften. Voor klanten die hello Azure Active Directory controleren rapport toomeet hun nalevingsvoorschriften, is het raadzaam die klant Hallo verzenden van een kopie van dit help-onderwerp met Hallo kopie van de klant Hallo geëxporteerd controlerapport toohelp uitgelegd Hallo-rapport meer informatie. Als Hallo auditor toounderstand Hallo nalevingsreglementen dat Azure momenteel voldoet aan, directe Hallo auditor toohello [naleving pagina](https://azure.microsoft.com/support/trust-center/compliance/) Hallo Microsoft Azure Trust Center.


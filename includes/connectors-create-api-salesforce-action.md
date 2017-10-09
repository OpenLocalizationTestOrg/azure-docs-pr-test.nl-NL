Nu dat u een voorwaarde, de tijd toodo iets interessante met Hallo-gegevens die worden gegenereerd door de trigger Hallo hebt toegevoegd. Volg deze stappen tooadd hello **Salesforce - Get-object** in te grijpen. Deze actie wordt Hallo-gegevens ophalen telkens wanneer die een nieuwe lead wordt gemaakt. U wordt een tweede actie met Hallo gegevens van Hallo Salesforce - Get een object actie toosend ook een e-mailbericht met Hallo Office 365-connector toevoegen.  

tooconfigure Hallo deze actie, moet u tooprovide Hallo informatie te volgen. U ziet dat het eenvoudig toouse gegevens die zijn gegenereerd door de trigger Hallo als invoer voor een aantal eigenschappen voor het nieuwe bestand Hallo Hallo:

| Bestandseigenschap maken | Beschrijving |
| --- | --- |
| Objecttype |Dit is Hallo type object dat u geïnteresseerd bent in Salesforce. Voorbeelden zijn Lead, Account, enzovoort. |
| object-ID |Hiermee wordt een id voor Hallo-object. |

1. Selecteer **een actie toevoegen** koppeling. Dit wordt geopend Hallo zoekvak waarin u naar elke actie u zoeken kunt graag tootake. In dit voorbeeld zijn de Salesforce-acties van belang.      
   ![SalesForce afbeelding 1](./media/connectors-create-api-salesforce/action-1.png)  
2. Voer *salesforce* toosearch voor verwante toosalesforce acties.
3. Selecteer **Salesforce - Get-object** zoals Hallo actie tootake.   **Opmerking**: u na vragen aan gebruiker tooauthorize uw logische app tooaccess uw Salesforce-account maken als u dit eerder niet hebt gedaan worden.    
   ![SalesForce afbeelding 2](./media/connectors-create-api-salesforce/action-2.png)    
4. Hallo **Get object** beheren wordt geopend.  
5. Selecteer *leiden* als Hallo-objecttype.
6. Selecteer Hallo **Object-ID** besturingselement.
7. Selecteer **...**  tooexpand Hallo lijst met tokens die worden gebruikt als invoer voor acties.       
   ![SalesForce afbeelding 3](./media/connectors-create-api-salesforce/action-3.png)    
8. Selecteer **Lead-ID** beheren wordt geopend.   
   ![SalesForce afbeelding 4](./media/connectors-create-api-salesforce/action-4.png)     
9. U ziet dat Hallo Lead-ID-token is nu in Hallo Object-ID-besturingselement, die aangeeft dat Hallo Get object actie zoekt naar een lead met een ID die is gelijk toohello lead-ID van potentiële klanten die deze logische app heeft geactiveerd.  
   ![SalesForce afbeelding 5](./media/connectors-create-api-salesforce/action-5.png)  
10. Sla uw werk op. Dat is alles, u Hallo Get object actie tooyour logische app hebt toegevoegd. Het besturingselement met Get-object ziet er als volgt:    
    ![SalesForce afbeelding 6](./media/connectors-create-api-salesforce/action-6.png)  

Nu dat u een actie tooget een lead hebt toegevoegd, kunt u toodo iets interessante met lead Hallo nieuw gemaakt. U kunt in een onderneming toosend een e-toonotify een distributielijst dat er een nieuwe lead is gemaakt. We gebruiken Hallo Office 365-connector toosend een e-mailbericht met een aantal Hallo relevante informatie uit Hallo nieuwe lead object in Salesforce.  

1. Selecteer **een actie toevoegen** Voer *e* in Hallo zoeken besturingselement. Dit filtert Hallo acties toothose die zijn gerelateerd toosending en ontvangen van e-mail.  
2. Selecteer Hallo **Office 365 Outlook - stuurt u een e-mailadres** item in de lijst. Als u al hebt gemaakt een *verbinding* tooyour Office 365-account, kun je het tooenter vraag uw Office 365 referenties toocreate worden deze nu. Nadat u klaar bent, Hallo **e-mailbericht verzenden** beheren wordt geopend.        
   ![SalesForce afbeelding 7](./media/connectors-create-api-salesforce/action-7.png)  
3. Voer Hallo e-mailadres dat u toosend e tooin hello wilt **naar** besturingselement.
4. In Hallo **onderwerp** beheren, voert u *nieuwe leiden gemaakt* - Selecteer Hallo *bedrijf* token. Dit wordt weergegeven Hallo *bedrijf* veld van de nieuwe lead Hallo gemaakt in Salesforce.  
5. In Hallo **hoofdtekst** beheer, kunt u selecteren van Hallo tokens van Hallo nieuwe lead object en u kunt ook opgeven welke tekst gewenst toodisplay in Hallo hoofdtekst van e-mail Hallo. Hier volgt een voorbeeld:  
   ![SalesForce afbeelding 8](./media/connectors-create-api-salesforce/action-8.png)   
6. Sla uw werkstroom.  

Dat is alles. Uw logische app is nu voltooid.  

U kunt nu uw logische app testen: in Salesforce, maakt u een nieuwe lead dat voldoet aan Hallo-voorwaarde die u hebt gemaakt.  Als u deze procedure volledig hebt gevolgd, moet u net een lead maken met een e-mailadres met *amazon.com* erin. Na een paar seconden uw logische app moet worden gestart en Hallo resultaten zien er mogelijk vergelijkbare toothis:  
![SalesForce afbeelding 9](./media/connectors-create-api-salesforce/action-9.png)  


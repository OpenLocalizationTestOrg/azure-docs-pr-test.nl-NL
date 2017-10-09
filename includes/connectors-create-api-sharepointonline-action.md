Nu dat u hebt een trigger, de tijd toodo iets interessante met Hallo-gegevens die worden gegenereerd door de trigger Hallo toegevoegd. Volg deze stappen tooadd hello **SharePoint Online - bestand maken** in te grijpen. Deze actie wordt een bestand worden maken in SharePoint Online elke keer Hallo nieuwe item trigger wordt geactiveerd. 

tooconfigure Hallo deze actie, moet u tooprovide Hallo informatie te volgen. Als u deze informatie opgeeft, zult u zien dat het is gemakkelijk toouse gegevens die zijn gegenereerd door de trigger Hallo als invoer voor een aantal eigenschappen voor het nieuwe bestand Hallo Hallo:

| Bestandseigenschap maken | Beschrijving |
| --- | --- |
| Site-URL |Dit is de URL Hallo van Hallo SharePoint Online-site waar u toocreate Hallo nieuw bestand. Selecteer Hallo site uit Hallo lijst weergegeven. |
| Pad naar de map |Dit is map (in de URL van de Site is geselecteerd in de vorige stap Hallo Hallo) Hallo waar Hallo nieuw bestand wordt geplaatst. Zoeken naar en selecteer Hallo-map. |
| Bestandsnaam |Dit is de naam Hallo van Hallo-bestand wordt gemaakt. |
| Bestandsinhoud |Hallo-inhoud die toohello bestand worden geschreven. |

1. Selecteer **+ een nieuwe stap** tooadd Hallo actie.  
   ![SharePoint online actie afbeelding 1](./media/connectors-create-api-sharepointonline/action-1.png)  
2. Selecteer Hallo **een actie toevoegen** koppeling. Dit wordt geopend Hallo zoekvak waarin u naar elke actie u zoeken kunt graag tootake. In dit voorbeeld zijn de SharePoint-acties van belang.    
   ![SharePoint online afbeelding 2](./media/connectors-create-api-sharepointonline/action-2.png)    
3. Voer *sharepoint* toosearch voor verwante tooSharePoint acties.
4. Selecteer **SharePoint Online - bestand maken** zoals Hallo actie tootake.   **Opmerking**: u worden na vragen aan gebruiker tooauthorize uw logische app tooaccess uw SharePoint-account als u een verbinding tooSharePoint Online eerder niet hebt gemaakt.    
   ![SharePoint online afbeelding 3](./media/connectors-create-api-sharepointonline/action-3.png)    
5. Hallo **Create file** beheren wordt geopend.   
   ![SharePoint online afbeelding 4](./media/connectors-create-api-sharepointonline/action-4.png)     
6. Selecteer **Site-URL** en bladeren toofind Hallo site waar u toocreate Hallo-bestand wilt.     
   ![SharePoint online afbeelding 5](./media/connectors-create-api-sharepointonline/action-5.png)  
7. Selecteer **mappad** en bladeren toofind Hallo map waar het nieuwe bestand hello wordt geplaatst.  
   ![SharePoint online afbeelding 6](./media/connectors-create-api-sharepointonline/action-6.png)  
8. Selecteer Hallo **bestandsnaam** beheren en voer de naam Hallo Hallo-bestand dat u wilt dat toocreate. Hier kunt u Hallo-bestandsnaam rechtstreeks kunt invoeren of kunt u een van de eigenschappen Hallo van Hallo trigger die u eerder hebt gemaakt. U dit doen door de eigenschappen te selecteren in lijst met Hallo **uitvoer wanneer een nieuw item wordt gemaakt**. Deze lijst wordt alleen weergegeven nadat u hebt geselecteerd Hallo **bestandsnaam** besturingselement. In deze walkthough ik ID (ID van het nieuwe lijstitem Hallo Hallo) geselecteerd als Hallo-naam van het Hallo-bestand wordt gemaakt door Hallo **SharePoint Online - bestand maken** in te grijpen.    
   ![SharePoint online afbeelding 7](./media/connectors-create-api-sharepointonline/action-7.png)  
9. Selecteer Hallo **inhoud bestand** beheren en Voer Hallo-inhoud die wordt geschreven toohello-bestand dat wordt gemaakt. Voor Hallo bestandsinhoud, zoals u ziet waarmee u kunt een van de eigenschappen Hallo van Hallo trigger die u eerder hebt gemaakt. Eenvoudig hello eigenschappen selecteren uit Hallo lijst weergegeven. U kunt ook Hallo invoeren **inhoud bestand** tekst rechtstreeks in Hallo-besturingselement. In dit voorbeeld ik geselecteerde sommige eigenschappen en spaties en een koppelteken tussen elke eigenschap toegevoegd.        
   ![SharePoint online afbeelding 8](./media/connectors-create-api-sharepointonline/action-8.png)  
10. Hallo wijzigingen tooyour werkstroom opslaan  
11. Gefeliciteerd, u hebt nu een volledig functionele logische app die wordt geactiveerd wanneer een nieuw item tooa SharePoint Online-lijst wordt toegevoegd. Hallo-app maakt vervolgens een bestand, gebruikmakend van de eigenschappen van het nieuwe lijstitem Hallo Hallo.  U kunt het nu door het maken van een nieuw item in de SharePoint-lijst Hallo testen. 


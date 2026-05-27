# Microsoft Fabric - Fabric Analyst in a Day - Lab 5

![](../media/Lab-1/main5.jpg)

# Inhoudsopgave

- Inleiding

- Dataflow Gen2

    - Taak 1: Geplande vernieuwing configureren voor Supplier Dataflow

- Pipeline

    - Taak 2: Pipeline aanmaken

    - Taak 3: Eenvoudige Pipeline bouwen

    - Taak 4: Nieuwe Pipeline aanmaken

    - Taak 5: Until-activiteit aanmaken

    - Taak 6: Variabelen aanmaken

    - Taak 7: Until-activiteit configureren

    - Taak 8: Dataflow-activiteit configureren

    - Taak 9: 1<sup>e</sup> Set variable-activiteit configureren

    - Taak 10: 2<sup>e</sup> Set variable-activiteit configureren

    - Taak 11: 3<sup>e</sup> Set variable-activiteit configureren

    - Taak 12: Wait-activiteit configureren

    - Taak 13: Geplande vernieuwing configureren voor Pipeline

- Referenties

# Inleiding

We hebben gegevens uit verschillende gegevensbronnen ingeladen in de Lakehouse. In dit lab stelt u een vernieuwingsschema in voor de gegevensbronnen. Ter herinnering de vereisten:

- **Leveranciersgegevens:** Snowflake wordt elke dag om middernacht / 00:00 bijgewerkt.

- **Medewerkergegevens:** in SharePoint worden elke dag om 09:00 bijgewerkt. Er is echter geconstateerd dat er soms een vertraging van 5 tot 15 minuten optreedt. We moeten een vernieuwingsschema aanmaken dat hier rekening mee houdt.

- **Klantgegevens:** in Dataverse zijn altijd actueel. Voorheen vernieuwden we deze vier keer per dag: om middernacht / 00:00, 06:00, middag / 12:00 en 18:00. Het IT-team heeft inmiddels een koppeling met Dataverse tot stand gebracht om deze gegevens in te laden in een Admin Lakehouse. Ze hebben deze gegevens ook getransformeerd. We hoeven geen vernieuwingsschema in te stellen, omdat we een koppeling gebruiken naar de Lakehouse die door het IT-team beschikbaar is gesteld.

- **Verkoopgegevens:** in ADLS worden elke dag om middag / 12:00 bijgewerkt. We hoeven hiervoor geen vernieuwingsschema in te stellen, omdat we een shortcut hebben aangemaakt. Zodra de gegevens in ADLS worden bijgewerkt, zijn ze direct beschikbaar.

Aan het einde van dit lab heeft u geleerd:

- Hoe u een geplande vernieuwing van Dataflow Gen2 configureert

- Hoe u een Pipeline aanmaakt

- Hoe u een geplande vernieuwing van een Pipeline configureert

# Dataflow Gen2

## Taak 1: Geplande vernieuwing configureren voor Supplier Dataflow

Laten we beginnen met het configureren van een geplande vernieuwing van Supplier Dataflow.

1. Navigeer terug naar de Fabric-werkruimte, **FAIAD_<inject key="Deployment ID" enableCopy="false"/>**, door de werkruimte te selecteren in het linkerdeelvenster.


2. Om het deelvenster met de lijst van artefacten te maximaliseren, selecteert u de dubbele pijl rechtsboven in het deelvenster.

    ![](../media/Lab-5/image6.png)


3. Alle artefacten die u heeft aangemaakt, worden hier weergegeven. Typ aan de rechterkant van het scherm **df** in het **zoekvak**. Hiermee filtert u de artefacten op Dataflows.

    ![](../media/Lab-5/image7.png)


4. Beweeg de muisaanwijzer over de rij **df_Supplier_Snowflake**. Selecteer het **beletselteken (…)**.


5. U ziet opties om de Dataflow te verwijderen, openen en te vernieuwen. Laten we de vernieuwingsgeschiedenis bekijken. Selecteer **Recent Runs**.

    ![](../media/Lab-5/image8.png)

    >**Opmerking:** Er verschijnt een venster/deelvenster aan de rechterkant met een lijst van vernieuwingen.


6. U zult zien dat er één vernieuwing heeft plaatsgevonden toen we in het vorige lab de optie **Save and run** hebben geselecteerd. Het **Type** vernieuwing dat wordt weergegeven is **On Demand**, wat aangeeft dat dit een handmatig uitgevoerde vernieuwing was.

    ![](../media/Lab-5/image9.png)


7. Selecteer de koppeling **Start time**.

    >**Opmerking:** De begintijd zal bij u anders zijn.

    ![](../media/Lab-5/image10.png)

    Het detailscherm wordt geopend. Dit scherm toont de details van de vernieuwing: de begintijd, eindtijd en duur. Ook worden de tabellen/activiteiten vermeld die zijn vernieuwd. Als er een fout is opgetreden, kunt u op de naam van de tabel/activiteit klikken om verder onderzoek te doen.

    ![](../media/Lab-5/image11.png)

8. Sluit dit scherm door op de **X** rechtsboven te klikken. U wordt teruggeleid naar de **werkruimte**.

9. Beweeg de muisaanwijzer over de rij **df_Supplier_Snowflake**. Selecteer het **beletselteken (…)**.

10. Laten we bekijken hoe we een automatische vernieuwing kunnen plannen. Kies de optie **Settings**.

    ![](../media/Lab-5/image12.png)

11. In het geopende **Settings**-deelvenster ziet u drie opties:

    - **About:** Hier kunt u de naam van de Dataflow wijzigen en een beschrijving toevoegen. U kunt ook zien wie de eigenaar van de dataflow is en wanneer deze voor het laatst is gewijzigd.

    - **Endorsement:** Hiermee kunt u opgeven of de dataflow het label **Promoted** of **Certified** krijgt, zodat anderen dit kunnen zien.

    - **Schedule:** Hier kunt u de planning van uw dataflows instellen.

        ![](../media/Lab-5/image13.png)

12. Selecteer de optie **Schedule**.


13. Om een schema te activeren, klikt u eenvoudig op **Add Schedule**.

    ![](../media/Lab-5/image14.png)


14. U kunt nu de frequentie van de vernieuwing opgeven door een optie te kiezen voor de eigenschap **Repeat**. Voor dit scenario kiest u **Daily (1)**.

15. Voor de eigenschap **Time** kunt u **12:00 AM** **(2)** opgeven, omdat we middernacht willen.

    >**Opmerking:** Door op de koppeling Add another time te klikken, kunt u meerdere vernieuwingstijden toevoegen.


16. U kunt ook een **Start date and time (3)** en een **End date and time (4)** opgeven. Kies voor dit scenario de huidige dag als begin- en einddatum.


17. U kunt de gewenste **Time Zone (5)** opgeven. Selecteer tot slot **Save**.

    ![](../media/Lab-5/image15.png)


18. U ziet de geplande vernieuwing en kunt deze bewerken of verwijderen als deze niet langer nodig is, of aanvullende geplande vernieuwingen toevoegen.

    ![](../media/Lab-5/image16.png)

    Zoals eerder vermeld, moeten we aangepaste logica bouwen voor het scenario waarin het medewerkerbestand in SharePoint niet op tijd wordt aangeleverd. Laten we een Pipeline gebruiken om dit op te lossen.

# Pipeline

## Taak 2: Pipeline aanmaken

1. Navigeer terug naar de Fabric-werkruimte, **FAIAD_<inject key="Deployment ID" enableCopy="false"/>**, door de werkruimte te selecteren in het linkerdeelvenster.

2. Selecteer in het bovenste menu **+ New item (1) -> Pipeline (2)**.

    ![](../media/Lab-5/image17.png)

3. Er wordt een dialoogvenster voor een nieuwe pipeline geopend. Geef de pipeline de naam **pl_Refresh_People_SharePoint** en selecteer **Create**.

    ![](../media/Lab-5/image18.png)

    U wordt doorgestuurd naar de **Pipeline-pagina**. Als u eerder met Azure Data Factory heeft gewerkt, zal dit scherm u bekend voorkomen. Laten we een kort overzicht geven van de indeling.

    U bevindt zich op het **Home**-scherm. In het bovenste menu vindt u opties voor het toevoegen van veelgebruikte activiteiten: valideren, een pipeline uitvoeren en de uitvoeringsgeschiedenis bekijken. In het centrale deelvenster vindt u snelle opties om de pipeline te beginnen bouwen.

    ![](../media/Lab-5/image19.png)


4. Selecteer in het bovenste menu **Activities**. In het menu vindt u een lijst met veelgebruikte activiteiten.


5. Selecteer het **beletselteken (…)** aan de rechterkant van het menu om alle overige beschikbare activiteiten te bekijken. We gaan in dit lab een aantal van deze activiteiten gebruiken.

    ![](../media/Lab-5/image20.png)


6. Klik in het bovenste menu op **Run**. U vindt hier opties om de pipeline-uitvoering te starten en in te plannen. U vindt ook de optie om de uitvoeringsgeschiedenis te bekijken via View run history.


7. Selecteer in het bovenste menu **View**. Hier vindt u opties om de code in JSON-formaat te bekijken. U vindt ook opties om de activiteiten automatisch uit te lijnen.

    >**Opmerking:** Als u een JSON-achtergrond heeft, kunt u aan het einde van het lab vrijelijk View JSON code selecteren. U zult merken dat alle orchestratie die u via de ontwerpweergave uitvoert, ook in JSON kan worden geschreven.

    ![](../media/Lab-5/image21.png)

## Taak 3: Eenvoudige Pipeline bouwen

Laten we beginnen met het bouwen van de pipeline. We hebben een activiteit nodig om de Dataflow te vernieuwen. Laten we een geschikte activiteit zoeken.


1. Selecteer in het bovenste menu **Activities -> Dataflow**. De Dataflow-activiteit wordt toegevoegd aan het centrale ontwerpdeelvenster. U ziet dat het onderste deelvenster nu configuratieopties voor de Dataflow-activiteit toont.


2. We gaan de activiteit configureren om verbinding te maken met de dataflow df_People_SharePoint. Selecteer in het **onderste deelvenster** de optie **Settings**.

    >**Opmerking:** Mogelijk moet u het onderste deelvenster omhoog slepen om de instellingen te zien.*

    ![](../media/Lab-5/image22.png)


3. Zorg ervoor dat **Workspace** is ingesteld op uw Fabric-werkruimte, **FAIAD_<inject key="Deployment ID" enableCopy="false"/>**.

4. Selecteer in de **Dataflow-vervolgkeuzelijst** de optie **df_People_SharePoint**. Wanneer deze Dataflow-activiteit wordt uitgevoerd, wordt **df_People_SharePoint** vernieuwd. Eenvoudig, toch?

    In ons scenario worden de medewerkergegevens niet op een vast schema bijgewerkt. Soms treedt er een vertraging op. Laten we bekijken hoe we hier rekening mee kunnen houden.

    ![](../media/Lab-5/image23.png)

5. Selecteer in het **onderste deelvenster** de optie **General**. Laten we de activiteit een naam en beschrijving geven.


6. Voer in het veld **Name** de waarde **dfactivity_People_SharePoint** in.


7. Voer in het veld **Description** de tekst **Dataflow-activiteit voor het vernieuwen van de dataflow df_People_SharePoint** in.


8. U ziet dat er een optie is om een activiteit te deactiveren. Deze functie is handig bij het testen of debuggen. Laat de instelling op **Activated** staan.


9. Er is een optie om **Timeout** in te stellen. Laat de **standaardwaarde** staan, zodat de dataflow voldoende tijd heeft om te vernieuwen.

    >**Opmerking:** Omdat de gegevens niet op een vast schema beschikbaar zijn, stellen we de activiteit in om elke 10 minuten opnieuw te worden uitgevoerd, maximaal drie keer. Als de derde poging ook mislukt, wordt een fout gerapporteerd.


10. Stel **Retry** in op **3**.


11. Vouw de sectie **Advanced** uit.


12. Stel **Retry interval (sec)** in op **600**.


13. Selecteer in het menu **Home -> Save**-pictogram om de pipeline op te slaan.

    ![](../media/Lab-5/image24.png)

    Let op het voordeel van het gebruik van de pipeline ten opzichte van het instellen van een geplande vernieuwing voor de dataflow (zoals we deden voor de eerdere dataflow):

    - De pipeline biedt de mogelijkheid om meerdere keren opnieuw te proberen voordat de vernieuwing als mislukt wordt gemarkeerd.

    - De pipeline biedt de mogelijkheid om naast het vernieuwen van de dataflow ook andere taken uit te voeren.

## Taak 4: Nieuwe Pipeline aanmaken

Laten we ons scenario iets complexer maken. We hebben geconstateerd dat als de gegevens om 09:00 niet beschikbaar zijn, ze doorgaans binnen vijf minuten beschikbaar zijn. Als dit tijdvenster wordt gemist, duurt het 15 minuten voordat het bestand beschikbaar is. We willen de nieuwe pogingen plannen na vijf en 15 minuten. Laten we bekijken hoe dit kan worden gerealiseerd door een nieuwe Pipeline aan te maken.

1. Klik in het linkerdeelvenster op **FAIAD_<inject key="Deployment ID" enableCopy="false"/>** om naar de startpagina van de werkruimte te navigeren.

2. Klik in het bovenste menu op **+ New item (1)** en klik in het pop-upvenster op **Pipeline (2)**.

    ![](../media/Lab-5/image25.png)

3. Het dialoogvenster voor een nieuwe pipeline wordt geopend. **Geef** de pipeline de naam **pl_Refresh_People_SharePoint_Option2 (3)** en selecteer **Create (4)**.

    ![](../media/Lab-5/image26.png)

## Taak 5: Until-activiteit aanmaken

1. U wordt doorgestuurd naar het Pipeline-scherm. Selecteer in het menu **Activities**.

2. Klik op het **beletselteken (…)** aan de rechterkant.

3. Klik in de lijst met activiteiten op **Until**.

    **Until:** is een activiteit die wordt gebruikt om te herhalen totdat aan een voorwaarde is voldaan.

    In ons scenario gaan we de dataflow herhalen en vernieuwen totdat dit succesvol is, of totdat we drie keer hebben geprobeerd.

    ![](../media/Lab-5/image27.png)

## Taak 6: Variabelen aanmaken

1. We moeten variabelen aanmaken die worden gebruikt voor het herhalen en het instellen van de status. Selecteer het **lege gebied** in het pipeline-ontwerpdeelvenster.

2. U ziet dat het menu in het onderste deelvenster verandert. Selecteer **Variables**.

3. Selecteer **+ New** om een nieuwe variabele toe te voegen.

4. Er verschijnt een rij. Voer **varCounter** in het **tekstvak Name** in. We gebruiken deze variabele om drie keer te herhalen.

5. Selecteer in de **vervolgkeuzelijst Type** de optie **Integer**.

6. Voer als **Default value** de waarde **0** in.

    >**Opmerking:** We voegen het voorvoegsel var toe aan variabelenamen, zodat ze eenvoudig te vinden zijn. Dit is tevens een goede praktijk.

    ![](../media/Lab-5/image28.png)

7. Selecteer **+ New** om nog een nieuwe variabele toe te voegen.

8. Er verschijnt een rij. Voer **varTempCounter** in het **tekstvak Name** in. We gebruiken deze variabele om de variabele varCounter te verhogen.

9. Selecteer in de **vervolgkeuzelijst Type** de optie **Integer**.

10. Voer als **Default value** de waarde **0** in.

11. Volg vergelijkbare stappen om nog drie variabelen toe te voegen:

    1. **varIsSuccess** van het type **String** en standaardwaarde **No**. Deze variabele wordt gebruikt om aan te geven of de dataflow-vernieuwing is geslaagd.

    2. **varSuccess** van het type **String** en standaardwaarde **Yes**. Deze variabele wordt gebruikt om de waarde van varIsSuccess in te stellen als de dataflow-vernieuwing is geslaagd.

    3. **varWaitTime** van het type **Integer** en standaardwaarde **60**. Deze variabele wordt gebruikt om de wachttijd in te stellen als de dataflow mislukt. (Ofwel 5 minuten/300 seconden of 15 minuten/900 seconden.)

        >**Opmerking:** Zorg ervoor dat er geen spatie staat voor of na de variabelenaam.

        ![](../media/Lab-5/image29.png)

## Taak 7: Until-activiteit configureren

1. Selecteer de **Until**-activiteit.

2. Selecteer in het **onderste deelvenster** de optie **General**.

3. Voer als **Name** de waarde **Iterator** in.

4. Voer als **Description** de tekst **"Iterator voor het vernieuwen van de dataflow. Er worden maximaal 3 pogingen gedaan"** in.

    ![](../media/Lab-5/image30.png)

5. Selecteer in het onderste deelvenster **Settings (1)**.

6. Selecteer het **tekstvak Expression (2)**. We moeten een expressie invoeren in dit tekstvak die als true of false wordt geëvalueerd. De Until-activiteit blijft herhalen zolang deze expressie als false wordt geëvalueerd. Zodra de expressie als true wordt geëvalueerd, stopt de Until-activiteit met herhalen en gaat verder naar de volgende activiteit.

7. Selecteer de koppeling **Add dynamic content (3)** die onder het tekstvak verschijnt.

    ![](../media/Lab-5/image31.png)

    We moeten een expressie schrijven die wordt uitgevoerd totdat de waarde van **varCounter gelijk is aan 3** of de waarde van **varIsSuccess gelijk is aan Yes**. (varCounter en varIsSuccess zijn de variabelen die we zojuist hebben aangemaakt.)

8. Het dialoogvenster **Pipeline expression builder** wordt geopend. In de onderste helft van het dialoogvenster ziet u een menu:

    1. **Parameters:** Waarden die aan de pipeline worden doorgegeven. Bijvoorbeeld een waarde van de ene pipeline die aan een andere pipeline wordt doorgegeven. Deze waarden kunnen in elke expressie worden gebruikt, maar kunnen niet worden gewijzigd tijdens de pipeline-uitvoering.

    2. **System variables:** Kunnen worden gebruikt in expressies bij het definiëren van entiteiten binnen een van de services. Bijvoorbeeld pipeline-id, pipeline-naam, triggernaam, enzovoort.

    3. **Trigger parameters:** Parameters die de pipeline hebben geactiveerd. Bijvoorbeeld bestandsnaam of mappad.

    4. **Functions:** U kunt functies aanroepen binnen expressies. Functies zijn ingedeeld in de categorieën Collection, Conversion, Date, Logical, Math en String. Zo is concat een String-functie en add een Math-functie.

    5. **Variables:** Pipeline-variabelen zijn waarden die tijdens een pipeline-uitvoering kunnen worden ingesteld en gewijzigd. In tegenstelling tot pipeline-parameters, die op pipeline-niveau worden gedefinieerd en niet kunnen worden gewijzigd tijdens een pipeline-uitvoering, kunnen pipeline-variabelen worden ingesteld en gewijzigd binnen een pipeline via een Set variable-activiteit. We gaan de Set variable-activiteit binnenkort gebruiken.

    6. **Library variables:** Library Variables gebruiken variabelen die zijn gedefinieerd in de **Variable Library Fabric Item**. Deze variabelen bieden een gecentraliseerde manier om configuraties te beheren over werkruimten heen ter ondersteuning van CI/CD-workflows. Ze kunnen worden gebruikt in combinatie met pipelines, notebooks, Lakehouse shortcuts en meer.

        ![](../media/Lab-5/image32.png)

9. Klik op **Functions** in het menu.

10. Selecteer in de sectie **Logical Functions** de functie **or**. U ziet dat **@or()** wordt toegevoegd aan het tekstvak voor de dynamische expressie. De **or**-functie heeft twee parameters nodig; we werken nu aan de eerste parameter.

    ![](../media/Lab-5/image33.png)


11. Plaats de cursor **tussen de haakjes** van de **@or**-functie.


12. Selecteer in de sectie **Logical Functions** de functie **equals**. U ziet dat deze wordt toegevoegd aan het tekstvak voor de dynamische expressie.

    >**Opmerking:** Uw functie zou er als volgt uit moeten zien: **@or(equals())**. De equals-functie heeft ook twee parameters nodig. We controleren of de variabele varCounter gelijk is aan 3.

    ![](../media/Lab-5/image34.png)


13. Plaats nu de cursor **tussen de haakjes** van de **@equals**-functie om de parameters toe te voegen.


14. Selecteer in het onderste menu **Variables**.


15. Selecteer de variabele **varCounter** als eerste parameter.


16. Voer **3** in als tweede parameter van de equals-functie. Zoals in de onderstaande schermafbeelding ziet uw expressie er als volgt uit: **@or(equals(variables('varCounter'),3))**

    ![](../media/Lab-5/image35.png)


17. We moeten de tweede parameter aan de **or**-functie toevoegen. **Voeg een komma toe** tussen de twee afsluitende haakjes. Typ deze keer de functienaam. Begin met typen **equ** en er verschijnt een vervolgkeuzelijst met beschikbare functies (dit heet IntelliSense). Selecteer de functie **equals**.

    ![](../media/Lab-5/image36.png)


18. De eerste parameter van de equals-functie is een variabele. Plaats **de cursor voor de komma**.


19. Begin met typen **variables(**


20. Selecteer met behulp van IntelliSense de optie **variables('varIsSuccess')**


21. Voer na de komma de tweede parameter in. Begin met typen **variables(**


22. Selecteer met behulp van IntelliSense de optie **variables('varSuccess')**. Hier vergelijken we de waarde van varIsSuccess met de waarde van varSuccess. (varSuccess heeft als standaardwaarde Yes.)

    ![](../media/Lab-5/image37.png)


23. Uw expressie zou er als volgt uit moeten zien:

    **@or(equals(variables('varCounter'),3),equals(variables('varIsSuccess'), variables('varSuccess')))**


24. Selecteer **OK**.

    ![](../media/Lab-5/image38.png)

## Taak 8: Dataflow-activiteit configureren


1. U wordt teruggeleid naar het ontwerpscherm. Selecteer de **Until-activiteit** en kies in het **onderste deelvenster** de optie **Activities**. We gaan nu de activiteiten toevoegen die moeten worden uitgevoerd.


2. Selecteer het **bewerkingspictogram** in de eerste rij. U wordt doorgestuurd naar een leeg iterator-ontwerpscherm.

    ![](../media/Lab-5/image39.png)


3. Selecteer in het bovenste menu **Activities -> Dataflow**. De Dataflow-activiteit wordt toegevoegd aan het ontwerpdeelvenster.


4. Selecteer met de **Dataflow-activiteit geselecteerd** in het onderste deelvenster de optie **General**. Laten we de activiteit een naam en beschrijving geven.


5. Voer in het veld **Name** de waarde **dfactivity_People_SharePoint** in.


6. Voer in het veld **Description** de tekst **"Dataflow-activiteit voor het vernieuwen van de dataflow df_People_SharePoint"** in.

    ![](../media/Lab-5/image40.png)


7. Selecteer **Settings** in het onderste deelvenster.


8. Zorg ervoor dat **Workspace** is ingesteld op uw werkruimte, **FAIAD_<inject key="Deployment ID" enableCopy="false"/>**.


9. Selecteer in de **Dataflow-vervolgkeuzelijst** de optie **df_People_SharePoint**.

    ![](../media/Lab-5/image41.png)

## Taak 9: 1<sup>e</sup> Set variable-activiteit configureren

We hebben de Dataflow-activiteit geconfigureerd zoals we eerder in het lab hebben gedaan. Nu voegen we nieuwe logica toe. Als de dataflow-vernieuwing is geslaagd, moeten we de Until-iterator verlaten. Ter herinnering: een van de voorwaarden om de iterator te verlaten is het instellen van de waarde van de variabele varIsSuccess op Yes.

1. Selecteer in het bovenste menu **Activities -> Set variable**. De Set variable-activiteit wordt toegevoegd aan het ontwerpcanvas.

2. Selecteer met de **Set variable-activiteit** geselecteerd in het onderste deelvenster de optie **General**. Laten we de activiteit een naam en beschrijving geven.

3. Voer in het veld **Name** de waarde **set_varIsSuccess** in.

4. Voer in het veld **Description** de tekst **"Variabele varIsSuccess instellen op Yes"** in.

    >**Opmerking:** Beweeg de muisaanwijzer over de **Dataflow-activiteit**. Aan de rechterkant van het activiteitsvak ziet u vier pictogrammen. Deze kunnen worden gebruikt om verbinding te maken met de volgende activiteit op basis van het resultaat van de activiteit:

    1. Het **grijze gebogen pijl**-pictogram wordt gebruikt bij het overslaan van de activiteit.

    2. Het **groene vinkje**-pictogram wordt gebruikt bij het slagen van de activiteit.

    3. Het **rode kruis**-pictogram wordt gebruikt bij het mislukken van de activiteit.

    4. Het **blauwe rechte pijl**-pictogram wordt gebruikt bij de voltooiing van de activiteit.

5. Klik op het **groene vinkje** van de Dataflow-activiteit dfactivity_People_SharePoint en sleep dit naar de nieuwe **Set variable-activiteit set_varIsSuccess**. Zo wordt de Set variable-activiteit uitgevoerd als de dataflow-vernieuwing is geslaagd.

    ![](../media/Lab-5/image42.png)

6. Selecteer met de **Set variable-activiteit** geselecteerd de optie **Settings** in het onderste menu.

7. Zorg ervoor dat in het onderste deelvenster **Variable type** is ingesteld op **Pipeline variable**.

8. Selecteer in het veld **Name** de waarde **varIsSuccess**. Dit is de variabele waarvan we de waarde gaan instellen.

9. Selecteer in het veld **Value** het **tekstvak**. Selecteer de koppeling **Add dynamic content**.

    ![](../media/Lab-5/image43.png)

10. Het dialoogvenster Pipeline expression builder wordt geopend. Selecteer het tekstgebied **Add dynamic content below using any combination of expressions, functions, and system variables (1)**.

11. Klik in het onderste menu op het **beletselteken (...) (2)** en selecteer vervolgens **Variables (3) -> varSuccess (4)**. U ziet dat **@variables('varSuccess')** wordt ingevoerd in het tekstgebied. Ter herinnering: bij het aanmaken van de variabelen hebben we de waarde van de variabele varSuccess vooraf ingesteld op Yes. We kennen dus de waarde Yes toe aan de variabele varIsSuccess.

12. Selecteer **OK**. U wordt teruggeleid naar het **iterator-ontwerpdeelvenster**.

    ![](../media/Lab-5/image44.png)

    Nu moeten we de teller instellen als de dataflow-activiteit mislukt. In een Pipeline kunnen we een variabele niet naar zichzelf verwijzen. Dit betekent dat we de tellervariabele varCounter niet kunnen verhogen door er één bij op te tellen (varCounter = varCounter + 1). Daarom maken we gebruik van de variabele varTempCounter.

## Taak 10: 2<sup>e</sup> Set variable-activiteit configureren

1. Selecteer in het bovenste menu **Activities -> Set variable**. De Set variable-activiteit wordt toegevoegd aan het ontwerpcanvas.

2. Selecteer met de **Set variable-activiteit** geselecteerd in het onderste deelvenster de optie **General**. Laten we de activiteit een naam en beschrijving geven.

3. Voer in het veld **Name** de waarde **set_varTempCounter** in.

4. Voer in het veld **Description** de tekst **"Variabele varTempCounter verhogen"** in.

5. Klik op het **rode kruis** van de Dataflow-activiteit en sleep dit naar de nieuwe Set variable-activiteit. Zo wordt deze Set variable-activiteit uitgevoerd als de dataflow-vernieuwing mislukt.

    ![](../media/Lab-5/image45.png)

6. Selecteer met de **Set variable-activiteit** geselecteerd de optie **Settings** in het onderste menu.

7. Zorg ervoor dat in het onderste deelvenster **Variable type** is ingesteld op **Pipeline variable**.

8. Selecteer in het veld **Name** de waarde **varTempCounter**. Dit is de variabele waarvan we de waarde gaan instellen.

9. Selecteer in het veld **Value** het **tekstvak**. Selecteer de koppeling **Add dynamic content**.

10. Het dialoogvenster Pipeline expression builder wordt geopend. Voer **@add(variables('varCounter'),1)** in.

    >**Opmerking:** U kunt deze expressie vrij typen, via het menu de functies selecteren, of kopiëren en plakken. Deze functie stelt de waarde van de variabele varTempCounter in op de waarde van de variabele varCounter plus één (varTempCounter = varCounter + 1).

    ![](../media/Lab-5/image46.png)

    Nu moeten we de waarde van de variabele varCounter instellen op de waarde van varTempCounter.

## Taak 11: 3<sup>e</sup> Set variable-activiteit configureren

1. Selecteer in het bovenste menu **Activities -> Set variable**. De Set variable-activiteit wordt toegevoegd aan het ontwerpcanvas.

2. Selecteer met de **Set variable-activiteit** geselecteerd in het onderste deelvenster de optie **General**. Laten we de activiteit een naam en beschrijving geven.

3. Voer in het veld **Name** de waarde **set_varCounter** in.

4. Voer in het veld **Description** de tekst **"Variabele varCounter verhogen"** in.

5. Klik op het **groene vinkje** van de Set variable-activiteit set_varTempCounter en sleep dit naar de nieuwe **Set variable-activiteit set_varCounter**.

    ![](../media/Lab-5/image47.png)

6. Selecteer met de **Set variable-activiteit set_varCounter** geselecteerd de optie **Settings** in het onderste menu.

7. Zorg ervoor dat in het onderste deelvenster **Variable type** is ingesteld op **Pipeline variable**.

8. Selecteer in het veld **Name** de waarde **varCounter**. Dit is de variabele waarvan we de waarde gaan instellen.


9. Selecteer in het veld **Value** het **tekstvak**. Selecteer de koppeling **Add dynamic content**.


10. Het dialoogvenster Pipeline expression builder wordt geopend. Voer **@variables('varTempCounter')** in. U kunt deze expressie vrij typen, via het menu de functies selecteren, of kopiëren en plakken.

11. Klik op **OK**.

    ![](../media/Lab-5/image48.png)

    >**Opmerking:** Deze functie stelt de waarde van de variabele varCounter in op de waarde van de variabele varTempCounter (varCounter = varTempCounter). Aan het einde van elke iteratie hebben zowel varCounter als varTempCounter dezelfde waarde.

## Taak 12: Wait-activiteit configureren

Vervolgens moeten we 5 minuten/300 seconden wachten als de dataflow-vernieuwing de eerste keer mislukt voordat we het opnieuw proberen. Als de dataflow-vernieuwing de tweede keer mislukt, moeten we 15 minuten/900 seconden wachten en het opnieuw proberen. We gaan de Wait-activiteit en de variabele varWaitTime gebruiken om de wachttijd in te stellen.


1. Selecteer in het bovenste menu **Activities -> ellipsis (…) -> Wait**. De Wait-activiteit wordt toegevoegd aan het ontwerpcanvas.


2. Selecteer met de **Wait-activiteit** geselecteerd in het onderste deelvenster de optie **General**. Laten we de activiteit een naam en beschrijving geven.


3. Voer in het veld **Name** de waarde **wait_onFailure** in.


4. Voer in het veld **Description** de tekst **"300 seconden wachten bij de 2e poging en 900 seconden bij de 3e poging"** in.


5. Klik op het **groene vinkje** van de Set variable-activiteit set_varCounter en sleep dit naar de nieuwe **Wait-activiteit wait_onFailure**.

    ![](../media/Lab-5/image49.png)


6. Selecteer met de **Wait-activiteit** geselecteerd de optie **Settings** in het onderste menu.


7. Selecteer in het veld **Wait time in seconds** het **tekstvak** en kies de koppeling **Add dynamic content**.


8. Het dialoogvenster Pipeline expression builder wordt geopend. Voer het volgende in:

   ```
   @if(
       greater(variables('varCounter'), 1),
       if(equals(variables('varCounter'), 2),
           mul(variables('varWaitTime'),15 ),
           mul(variables('varWaitTime'), 0)
       ),
       mul(variables('varWaitTime'),5 )
   )
   ```

    U kunt deze expressie vrij typen, via het menu de functies selecteren, of kopiëren en plakken.

    ![](../media/Lab-5/image50.png)

    We gebruiken hier twee nieuwe functies:

    - **greater:** Neemt twee getallen als parameters en vergelijkt welke groter is.

    - **mul:** Dit is een vermenigvuldigingsfunctie die twee parameters neemt om te vermenigvuldigen.

    De expressie is een geneste if-instructie. Er wordt gecontroleerd of de waarde van de variabele varCounter groter is dan 1.

    Als dat het geval is, wordt gecontroleerd of de waarde van de variabele varCounter gelijk is aan 2. Als dat zo is, wordt de wachttijd ingesteld op varWaitTime maal 15. Ter herinnering: de standaardwaarde van varWaitTime is 60. Dat is 60 × 15 = 900 seconden. Als de waarde van de variabele varCounter niet 2 is (dat wil zeggen groter dan 2, wat betekent dat de dataflow-vernieuwing drie keer is mislukt), zijn we klaar met herhalen. We hoeven niet meer te wachten, dus de wachttijd wordt ingesteld op varWaitTime × 0, dus 0. Als de waarde van de variabele varCounter gelijk is aan 1, vermenigvuldigen we varWaitTime × 5. Dat is 60 × 5 = 300 seconden.

9. Selecteer **OK**.

    **Controlepunt:** Uw **Until**-iterator zou er als volgt uit moeten zien als in de onderstaande schermafbeelding.

    ![](../media/Lab-5/image51.png)

10. Selecteer linksboven in het ontwerpcanvas **pl_Refresh_People_Sharepoint_Option2** of **Main Canvas** om de Until-iterator te verlaten.

    ![](../media/Lab-5/image52.png)


11. We zijn klaar met het aanmaken van de pipeline. Selecteer in het bovenste menu **Home -> Save**-pictogram om de pipeline op te slaan.

    ![](../media/Lab-5/image53.png)

## Taak 13: Geplande vernieuwing configureren voor Pipeline

1. We kunnen de pipeline testen door **Home -> Run** te selecteren.
         
    >**Opmerking:** Het kan enkele minuten duren voordat de pipeline een vernieuwing heeft voltooid. Dit is een trainingsomgeving, dus het bestand in SharePoint is altijd beschikbaar. Uw pipeline zal daarom nooit mislukken.

2. We kunnen de pipeline instellen om op een schema te worden uitgevoerd. Selecteer in het bovenste menu **Home -> Schedule**. Het dialoogvenster Schedule wordt geopend.

3. Selecteer de knop **+ Add Schedule** onder **Scheduled run**.

    ![](../media/Lab-5/image54.png)

4. Stel de **vervolgkeuzelijst Repeat** in op **Daily**.

5. Stel **Time** in op **9 AM**.

6. Stel **Start date and time** in op **Vandaag**.

7. Stel **End date and time** in op een **toekomstige datum**.

8. Stel uw **tijdzone** in.

    >**Opmerking:** Omdat dit een labomgeving is, kunt u de tijdzone instellen op uw voorkeurstijdzone. In een werkelijk scenario stelt u de tijdzone in op basis van de locatie van uw gegevensbron.

9. Selecteer **Save**.

10. Selecteer het **X**-teken rechtsboven in het dialoogvenster om het te sluiten.

    ![](../media/Lab-5/image55.png)

11. Selecteer uw Fabric-werkruimte **FAIAD_<inject key="Deployment ID" enableCopy="false"/>** in het linkerdeelvenster om naar de werkruimte te navigeren.

    >**Opmerking:** In het Schedule-scherm is er geen optie om een melding te ontvangen bij slagen of mislukken (zoals bij Dataflow Schedule). Meldingen kunnen worden ingesteld door een activiteit aan de pipeline toe te voegen. We doen dit niet in dit lab, omdat dit een labomgeving is.

    We hebben vernieuwingsschema's ingesteld voor de verschillende gegevensbronnen. In het volgende lab maken we een semantisch model met relaties, metingen en andere modelleringshandelingen.

# Referenties

Fabric Analyst in a Day (FAIAD) introduceert u tot een aantal van de belangrijkste functies die beschikbaar zijn in Microsoft Fabric. In het menu van de service vindt u in de sectie Help (?) koppelingen naar nuttige informatiebronnen.

![](../media/Lab-1/image29.png)

Hier zijn nog enkele aanvullende bronnen die u helpen bij uw volgende stappen met Microsoft Fabric.

- Lees de blogpost voor de volledige aankondiging van [Microsoft Fabric GA](https://aka.ms/Fabric-Hero-Blog-Ignite23)

- Verken Fabric via de [Guided Tour](https://aka.ms/Fabric-GuidedTour)

- Meld u aan voor de [gratis proefversie van Microsoft Fabric](https://aka.ms/try-fabric)

- Bezoek de [Microsoft Fabric-website](https://aka.ms/microsoft-fabric)

- Leer nieuwe vaardigheden door de [Fabric-leermodules](https://aka.ms/learn-fabric) te verkennen

- Raadpleeg de [technische documentatie van Fabric](https://aka.ms/fabric-docs)

- Lees het [gratis e-book over aan de slag gaan met Fabric](https://aka.ms/fabric-get-started-ebook)

- Word lid van de [Fabric-community](https://aka.ms/fabric-community) om vragen te stellen, feedback te delen en van anderen te leren

Lees de uitgebreidere aankondigingsblogs over de Fabric-ervaringen:

- [Data Factory-ervaring in Fabric-blog](https://aka.ms/Fabric-Data-Factory-Blog)

- [Synapse Data Engineering-ervaring in Fabric-blog](https://aka.ms/Fabric-DE-Blog)

- [Synapse Data Science-ervaring in Fabric-blog](https://aka.ms/Fabric-DS-Blog)

- [Synapse Data Warehousing-ervaring in Fabric-blog](https://aka.ms/Fabric-DW-Blog)

- [Synapse Real-Time Analytics-ervaring in Fabric-blog](https://aka.ms/Fabric-RTA-Blog)

- [Power BI-aankondigingsblog](https://aka.ms/Fabric-PBI-Blog)

- [Data Activator-ervaring in Fabric-blog](https://aka.ms/Fabric-DA-Blog)

- [Beheer en governance in Fabric-blog](https://aka.ms/Fabric-Admin-Gov-Blog)

- [OneLake in Fabric-blog](https://aka.ms/Fabric-OneLake-Blog)

- [Dataverse en Microsoft Fabric-integratieblog](https://aka.ms/Dataverse-Fabric-Blog)

© 2026 Microsoft Corporation. Alle rechten voorbehouden.

Door gebruik te maken van deze demo/dit lab, gaat u akkoord met de volgende voorwaarden:

De technologie/functionaliteit die in deze demo/dit lab wordt beschreven, wordt door Microsoft Corporation aangeboden met als doel uw feedback te verzamelen en u een leerervaring te bieden. U mag de demo/het lab uitsluitend gebruiken om dergelijke technologiefuncties en -functionaliteit te evalueren en feedback aan Microsoft te geven. U mag het niet voor enig ander doel gebruiken. U mag deze demo/dit lab of enig deel daarvan niet wijzigen, kopiëren, distribueren, verzenden, weergeven, uitvoeren, reproduceren, publiceren, in licentie geven, er afgeleide werken van maken, overdragen of verkopen.

HET KOPIËREN OF REPRODUCEREN VAN DE DEMO/HET LAB (OF EEN DEEL DAARVAN) NAAR EEN ANDERE SERVER OF LOCATIE TEN BEHOEVE VAN VERDERE REPRODUCTIE OF HERDISTRIBUTIE IS UITDRUKKELIJK VERBODEN.

DEZE DEMO/DIT LAB BEVAT BEPAALDE SOFTWARETECHNOLOGIE-/PRODUCTFUNCTIES EN -FUNCTIONALITEIT, INCLUSIEF MOGELIJK NIEUWE FUNCTIES EN CONCEPTEN, IN EEN GESIMULEERDE OMGEVING ZONDER COMPLEXE INSTALLATIE OF CONFIGURATIE VOOR HET HIERBOVEN BESCHREVEN DOEL. DE TECHNOLOGIE/CONCEPTEN DIE IN DEZE DEMO/DIT LAB WORDEN GEPRESENTEERD, VERTEGENWOORDIGEN MOGELIJK NIET DE VOLLEDIGE FUNCTIEFUNCTIONALITEIT EN WERKEN MOGELIJK NIET ZOALS EEN DEFINITIEVE VERSIE ZOU WERKEN. WE KUNNEN OOK BESLUITEN EEN DEFINITIEVE VERSIE VAN DERGELIJKE FUNCTIES OF CONCEPTEN NIET UIT TE BRENGEN. UW ERVARING MET HET GEBRUIK VAN DERGELIJKE FUNCTIES EN FUNCTIONALITEIT IN EEN FYSIEKE OMGEVING KAN OOK ANDERS ZIJN.

**FEEDBACK**. Als u feedback geeft over de technologiefuncties, functionaliteit en/of concepten die in deze demo/dit lab worden beschreven aan Microsoft, verleent u Microsoft kosteloos het recht om uw feedback op enigerlei wijze en voor elk doel te gebruiken, te delen en te commercialiseren. U verleent ook aan derden, kosteloos, alle octrooirechten die nodig zijn voor hun producten, technologieën en diensten om gebruik te maken van of te koppelen aan specifieke onderdelen van een Microsoft-software of -dienst die de feedback bevat. U zult geen feedback geven die onderworpen is aan een licentie die vereist dat Microsoft zijn software of documentatie in licentie geeft aan derden omdat wij uw feedback daarin opnemen. Deze rechten blijven van kracht na beëindiging van deze overeenkomst.

MICROSOFT CORPORATION WIJST HIERBIJ ALLE GARANTIES EN VOORWAARDEN MET BETREKKING TOT DE DEMO/HET LAB AF, INCLUSIEF ALLE GARANTIES EN VOORWAARDEN VAN VERKOOPBAARHEID, ONGEACHT OF DEZE UITDRUKKELIJK, IMPLICIET OF WETTELIJK ZIJN, GESCHIKTHEID VOOR EEN BEPAALD DOEL, TITEL EN NIET-INBREUK. MICROSOFT GEEFT GEEN GARANTIES OF VERKLARINGEN MET BETREKKING TOT DE NAUWKEURIGHEID VAN DE RESULTATEN, DE UITVOER DIE VOORTVLOEIT UIT HET GEBRUIK VAN DE DEMO/HET LAB, OF DE GESCHIKTHEID VAN DE INFORMATIE IN DE DEMO/HET LAB VOOR ENIG DOEL.

**VRIJWARING**

Deze demo/dit lab bevat slechts een deel van de nieuwe functies en verbeteringen in Microsoft Power BI. Sommige functies kunnen worden gewijzigd in toekomstige versies van het product. In deze demo/dit lab leert u over enkele, maar niet alle, nieuwe functies.

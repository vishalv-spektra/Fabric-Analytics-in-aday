# Microsoft Fabric - Fabric Analyst in a Day - Lab 2

![](../media/Lab-1/main2.jpg)

# Inhoudsopgave

* Introductie

* Fabric-licentie

  * Taak 1: Een Microsoft Fabric-proeflicentie inschakelen

* Fabric-werkruimte

  * Taak 2: Een Fabric-werkruimte maken

  * Taak 3: Een Lakehouse maken

* Overzicht van Fabric-ervaringen

  * Taak 4: Data Factory-ervaring

  * Taak 5: Industry Solutions-ervaring

  * Taak 6: Real-Time Intelligence-ervaring

  * Taak 7: Data Engineering-ervaring

  * Taak 8: Data Science-ervaring

  * Taak 9: Data Warehouse-ervaring

  * Taak 10: Databases-ervaring

* Referenties

# Introductie

Vandaag leert u verschillende belangrijke functies van Microsoft Fabric kennen. Dit is een introductieworkshop die bedoeld is om u kennis te laten maken met de verschillende productervaringen en onderdelen die beschikbaar zijn in Fabric. Aan het einde van deze workshop leert u hoe u Lakehouse, Dataflow Gen2, Pipeline, DirectLake en meer kunt gebruiken.

Aan het einde van dit lab hebt u geleerd:

* Hoe u een Fabric-werkruimte maakt

* Hoe u een Lakehouse maakt

# Fabric-licentie

## Taak 1: Een Microsoft Fabric-proeflicentie inschakelen

1. Selecteer **Power BI Portal** op het bureaublad van de virtuele machine. Mogelijk wordt u gevraagd zich aan te melden.

   ![](../media/Lab-2/image6.png)

   > **Opmerking:** Als u de labomgeving gebruikt, wordt u mogelijk automatisch aangemeld.

   > **Opmerking:** Als Fabric niet wordt geopend, ga dan in de browser naar http://app.fabric.microsoft.com/.

2. Kopieer de gebruikersnaam en plak deze in het veld **E-mail** van het dialoogvenster en selecteer **Verzenden**.

   * **E-mail/Gebruikersnaam:** <inject key="AzureAdUserEmail"></inject>

     ![](../media/Lab-2/image7.png)

3. Op het tabblad **Aanmelden bij Microsoft Azure** ziet u het aanmeldscherm. Voer vervolgens het volgende **E-mailadres/Gebruikersnaam** in en klik op **Volgende**.

   * **E-mail/Gebruikersnaam:** <inject key="AzureAdUserEmail"></inject>

     ![](../media/Lab-1/image9.png)

4. Voer nu de volgende **Tijdelijke toegangscode** in en klik op **Aanmelden**.

   * **Tijdelijke toegangscode:** <inject key="AzureAdUserPassword"></inject>

     ![](../media/Lab-1/image10.png)

5. U wordt doorgestuurd naar de vertrouwde **Power BI Service-startpagina**.

6. We gaan ervan uit dat u bekend bent met de indeling van Power BI Service. Als u vragen heeft, aarzel dan niet om deze aan de instructeur te stellen.

   U bevindt zich momenteel in **Mijn werkruimte**. Om met Fabric-items te werken, hebt u een proeflicentie nodig en een werkruimte waaraan een Fabric-licentie is toegewezen. Laten we dit instellen.

7. Selecteer in de rechterbovenhoek van het scherm het **gebruikerspictogram**.

8. Selecteer **Proefversie starten**.

   ![](../media/Lab-2/image10.png)

9. Het dialoogvenster **Upgraden naar een gratis Microsoft Fabric-proefversie** wordt geopend. Selecteer **Activeren**.

   > **Opmerking:** Wijzig de standaardregio niet. Laat deze ongewijzigd.

   ![](../media/Lab-2/image11.png)

10. Het dialoogvenster **Upgrade naar Microsoft Fabric voltooid** wordt geopend. Selecteer **Fabric-startpagina**.

    ![](../media/Lab-2/image12.png)

11. U wordt doorgestuurd naar de **Microsoft Fabric-startpagina**. Mogelijk wordt het dialoogvenster **“Welkom bij de Fabric-weergave”** geopend. U kunt desgewenst **Rondleiding starten** of **Annuleren** selecteren.

    ![](../media/Lab-2/image13.png)

# Fabric-werkruimte

## Taak 2: Een Fabric-werkruimte maken

1. Laten we nu een werkruimte maken met een Fabric-licentie. Selecteer **Werkruimten (1)** in de linker navigatiebalk. Er wordt een dialoogvenster geopend.

2. Klik op **+ Nieuwe werkruimte (2)** onderaan het uitklapmenu.

   ![](../media/Lab-2/image14.png)

3. Het dialoogvenster **Een werkruimte maken** wordt geopend aan de rechterkant van de browser.

4. Voer in het veld **Naam** het volgende in: **FAIAD_<inject key="Deployment ID" enableCopy="false"/>**

   > **Opmerking:** De naam van de werkruimte moet uniek zijn. Zorg ervoor dat onder het veld Naam een groen vinkje met de melding "Deze naam is beschikbaar" wordt weergegeven.

5. Indien gewenst kunt u een beschrijving voor de werkruimte invoeren. Dit is een optioneel veld.

6. Klik op **Geavanceerd** om de sectie uit te vouwen.

   ![](../media/Lab-2/image15.png)

7. Controleer onder **Licentiemodus** of **Proefversie** is geselecteerd. (Deze optie zou standaard geselecteerd moeten zijn.)

8. Selecteer **Toepassen** om een nieuwe werkruimte te maken.

   ![](../media/Lab-2/image16.png)

   U wordt doorgestuurd naar uw nieuw gemaakte werkruimte. We zullen gegevens uit verschillende gegevensbronnen naar een Lakehouse brengen en deze gegevens uit het Lakehouse gebruiken om ons model op te bouwen en rapportages te maken. De eerste stap is het maken van een Lakehouse. Dit gaan we nu doen.

## Taak 3: Een Lakehouse maken

1. Zoek in de nieuw gemaakte werkruimte **FAIAD_<inject key="Deployment ID" enableCopy="false"/>** naar de knop **+ Nieuw item (1)** in het linkernavigatiepaneel. Hier kunt u nieuwe items in uw werkruimte maken.

2. Typ in het zoekvak **Lakehouse (2)** en selecteer vervolgens in de zoekresultaten de optie **Lakehouse (3)**. Hiermee kunt u een nieuw Lakehouse maken om uw big data op te slaan, op te vragen en te beheren.

   ![](../media/Lab-2/image17.png)

3. Er verschijnt een dialoogvenster voor een nieuw Lakehouse. Voer **lh_FAIAD** in het tekstvak **Naam** in.

   > **Opmerking:** *lh* staat hier voor Lakehouse. We gebruiken het voorvoegsel *lh* zodat het eenvoudiger te herkennen en terug te vinden is.

   > **Opmerking:** Deze functie bevindt zich niet langer in preview, **maar we hoeven deze nog steeds niet in te schakelen**.

4. Zorg ervoor dat **Lakehouse-schema's (2)** niet is aangevinkt.

5. Selecteer vervolgens **Maken (3)** om verder te gaan.

   ![](../media/Lab-2/image18.png)

   > **Opmerking:** **Zorg ervoor dat u de functie Lakehouse-schema's uitschakelt, aangezien deze nu standaard is ingeschakeld.**

   Binnen enkele ogenblikken wordt een Lakehouse gemaakt en wordt u doorgestuurd naar de Lakehouse Explorer-interface. Linksboven, naast de Fabric-naam in de koptekst, ziet u het Lakehouse-pictogram. Het werkruimtepictogram in de linkernavigatie zal weergeven dat deze nu een item bevat.

   In Lakehouse Explorer ziet u de secties **Tabellen** en **Bestanden**. Een Lakehouse kan Azure Data Lake Storage Gen2-bestanden weergeven in de sectie Bestanden, of een dataflow kan gegevens laden naar Lakehouse-tabellen. Er zijn verschillende opties beschikbaar. We zullen enkele van deze mogelijkheden in de volgende labs laten zien.

   ![](../media/Lab-2/image19.png)

# Overzicht van Fabric-ervaringen

## Taak 4: Data Factory-ervaring

1. Selecteer het pictogram **Workloads** aan de linkerkant van uw scherm. Er wordt een dialoogvenster geopend met een lijst van Fabric-ervaringen. De lijst met ervaringen omvat Power BI, Data Factory, Industry Solutions, Real-Time Intelligence, Data Engineering, Data Science en Data Warehouse. Laten we deze verkennen.

   ![](../media/Lab-2/image20.png)

2. Selecteer **Data Factory**.

   ![](../media/Lab-2/image21.png)

3. U wordt doorgestuurd naar de startpagina van Data Factory. Hieronder vindt u een gedetailleerde uitleg van de verschillende onderdelen, ontworpen om u stap voor stap te begeleiden bij het effectief gebruiken van Data Factory. Dataflow Gen2 is de volgende generatie van Dataflow.

    **Wat is Data Factory?**

    Data Factory is een hulpmiddel dat u helpt gegevens uit verschillende bronnen te beheren en te organiseren. Het stelt u in staat gegevens te verzamelen, voor te bereiden en te transformeren, zodat deze effectief kunnen worden gebruikt. Of u nu een beginner of een expert bent, Data Factory biedt hulpmiddelen om gegevensomzetting eenvoudiger en efficiënter te maken.

    **Itemtypen:**

    a. **Dataflow Gen2:** Dataflows zijn vergelijkbaar met recepten voor het transformeren van gegevens. Ze bieden meer dan 300 verschillende transformaties die u op uw gegevens kunt toepassen. Dit betekent dat u uw gegevens op veel verschillende manieren kunt opschonen, combineren en wijzigen om aan uw behoeften te voldoen.

    b. **Pipeline:** Pipelines zijn workflows waarmee u gegevensprocessen kunt automatiseren. Ze stellen u in staat flexibele gegevensworkflows te maken die kunnen worden aangepast aan uw specifieke vereisten. Dit maakt het eenvoudiger om gegevens op een gestructureerde manier te beheren en te verwerken.

    c. **Azure Data Factory:** Azure Data Factory is een cloudgebaseerde gegevensintegratieservice waarmee u gegevensgestuurde workflows kunt maken voor het coördineren en automatiseren van gegevensverplaatsing en gegevenstransformatie.

    d. **Apache Airflow-taak:** Apache Airflow is een opensourceplatform dat wordt gebruikt om workflows programmatisch te maken, plannen en bewaken. Binnen Data Factory kunt u hiermee complexe gegevensworkflows maken, plannen en beheren.

    e. **Kopieertaak:** Een kopieertaak is een functie waarmee u gegevens van de ene bron naar een andere kunt kopiëren. Het biedt een eenvoudige en efficiënte manier om gegevens tussen verschillende gegevensopslagplaatsen te verplaatsen.

    f. **Gespiegelde database:** Een functie voor het maken van gespiegelde versies van databases voor back-up, testen of alleen-lezen toegang.

    g. **Gespiegelde SAP:** Integreer uw bestaande SAP-omgeving naadloos met de rest van uw gegevens in Fabric.

    h. **Gespiegelde Oracle (preview):** Mirroring in Fabric repliceert uw Oracle-databases naar een uniform platform, waardoor bijna realtime analyses met lage latentie mogelijk worden naast andere gegevensbronnen.

    i. **Gespiegelde Google BigQuery (preview):** Met mirroring in Fabric kunt u continu Google BigQuery-gegevens repliceren naar OneLake, waardoor complexe ETL-processen worden geëlimineerd en naadloos gebruik mogelijk wordt voor analyses, AI en gegevensdeling.

    j. **Variabelenbibliotheek:** Bevat een lijst met variabelen en hun standaardwaarden. Het kan ook andere waardesets bevatten met alternatieve waarden.

    k. **dbt-taak (preview):** Hiermee kunt u dbt gebruiken om gegevens met SQL te transformeren in een vertrouwde omgeving.

    **Aan de slag:**

    Om Data Factory te gaan gebruiken, kunt u de volgende stappen volgen:

    a. **Leer Data Factory gebruiken:** Deze sectie helpt u om aan de slag te gaan met Data Factory. U krijgt begeleiding over hoe u de tool effectief kunt gebruiken.

    b. **Maak uw eerste Dataflow:** Hier leert u hoe u uw eerste Dataflow maakt. Dataflows zijn essentieel voor het transformeren van uw gegevens volgens uw behoeften.

    c. **Maak uw eerste Pipeline:** Deze sectie begeleidt u bij het maken van uw eerste Pipeline. Pipelines helpen u om gegevensprocessen efficiënt te automatiseren en beheren.

    d. **Leer Data Factory bewaken:** Bewaking is essentieel om ervoor te zorgen dat uw gegevensprocessen probleemloos verlopen. Deze sectie leert u hoe u uw Data Factory-activiteiten kunt bewaken.

    e. **Leer gegevens transformeren met Dataflows:** Deze sectie helpt u te begrijpen hoe u Dataflows kunt gebruiken om uw gegevens effectief te transformeren.

    f. **Maak uw eerste API voor GraphQL:** Als u geïnteresseerd bent in het gebruik van API's met GraphQL, begeleidt deze sectie u bij de eerste stappen.

    g. **Maak uw eerste gebruikersgegevensfuncties:** Deze sectie helpt u bij het maken van gebruikersgegevensfuncties, die nuttig zijn voor het beheren en transformeren van gebruikersgegevens.

    ![](../media/Lab-2/image23.png)

4. Klik linksboven in het scherm op **Terug naar workloads**. Deze actie brengt u terug naar de hoofdpagina met workloads, waar u andere hulpmiddelen of secties kunt verkennen.

    ![](../media/Lab-2/image24.png)

## Taak 5: Industry Solutions-ervaring

1. Klik op de pagina **Workloads** op **Industry Solutions** om verder te gaan.

   ![](../media/Lab-2/image25.png)

2. U wordt doorgestuurd naar de startpagina van Industry Solutions. Hieronder vindt u een gedetailleerd overzicht van de verschillende onderdelen, ontworpen om u stap voor stap te helpen Industry Solutions effectief te gebruiken.

    **Wat zijn Industry Solutions?**

    Industry Solutions zijn kant-en-klare gegevensoplossingen in Microsoft Fabric die oplossingen en hulpmiddelen bieden voor verschillende sectoren. Industry Solutions helpen u aan de slag te gaan met belangrijke bedrijfsscenario's met behulp van branchegerelateerde gegevensmodellen, connectoren, transformaties, rapporten en andere middelen.

    **Itemtypen:**

    a. **Duurzaamheidsoplossingen:** ondersteunen de opname, standaardisatie en analyse van Environmental, Social, and Governance (ESG)-gegevens.

    b. **Retailoplossingen:** helpen bij het beheren van grote hoeveelheden gegevens, het integreren van gegevens uit verschillende bronnen en het leveren van realtime analyses voor snelle besluitvorming. Retailers kunnen deze oplossingen gebruiken voor voorraadoptimalisatie, klantsegmentatie, verkoopprognoses, dynamische prijsstelling en fraudedetectie.

    c. **Zorgoplossingen:** zijn strategisch ontworpen om de tijd tot waarde voor klanten te versnellen door in te spelen op de kritieke behoefte om zorggegevens efficiënt om te zetten naar een geschikt formaat voor analyse.

    > **Opmerking:** Sommige oplossingen worden mogelijk niet weergegeven.

    **Aan de slag:**

    Volg de onderstaande stappen om Industry Solutions te gebruiken:

    a. **Meer informatie over oplossingen voor zorggegevens:** Klik op de knop **Meer informatie** om meer te lezen over oplossingen voor zorggegevens en te begrijpen hoe deze in uw projecten kunnen worden gebruikt.

    b. **Aan de slag met oplossingen voor zorggegevens:** Begin met het implementeren van oplossingen voor zorggegevens in uw projecten.

    c. **Meer informatie over duurzaamheidsoplossingen:** Klik op de knop **Meer informatie** om meer te lezen over duurzaamheidsoplossingen en te begrijpen hoe deze in uw projecten kunnen worden gebruikt.

    d. **Aan de slag met duurzaamheidsoplossingen:** Begin met het implementeren van duurzaamheidsoplossingen in uw projecten.

    e. **Meer informatie over retailoplossingen:** Klik op de knop **Meer informatie** om meer te lezen over retailoplossingen en te begrijpen hoe deze in uw projecten kunnen worden gebruikt.

    f. **Aan de slag met retailoplossingen:** Begin met het implementeren van retailoplossingen in uw projecten.

    ![](../media/Lab-2/image26.png)

3. Klik linksboven in het scherm op **Terug naar workloads**. Deze actie brengt u terug naar de hoofdpagina met workloads, waar u andere hulpmiddelen of secties kunt verkennen.

   ![](../media/Lab-2/image24.png)

## Taak 6: Real-Time Intelligence-ervaring

1. Klik op de pagina **Workloads** op **Real-Time Intelligence** om verder te gaan.

    ![](../media/Lab-2/image27.png)

2. U wordt doorgestuurd naar de startpagina van Real-Time Intelligence. Hieronder vindt u een gedetailleerd overzicht van de secties om u te helpen Real-Time Intelligence effectief en stap voor stap te gebruiken.

    **Wat is Real-Time Intelligence?**

    Real-Time Intelligence is een hulpmiddel dat u helpt bij het beheren en analyseren van grote hoeveelheden zeer gedetailleerde gegevens uit verschillende bronnen. Hiermee kunt u gegevens in realtime opnemen, analyseren en erop reageren, waardoor uw bedrijfsprocessen worden verbeterd door tijdige besluitvorming en acties.

    **Itemtypen:** 

    a. **Eventhouse:** Wordt gebruikt om een werkruimte te maken met één of meerdere KQL-databases die over verschillende projecten gedeeld kunnen worden.

    b. **KQL Queryset:** Wordt gebruikt om query’s uit te voeren op gegevens om deelbare tabellen en visualisaties te genereren.

    c. **Real-Time Dashboard:** Wordt gebruikt om realtime dashboards binnen enkele seconden na gegevensinvoer te visualiseren.

    d. **Eventstream:** Wordt gebruikt om realtime gebeurtenisstromen vast te leggen, te transformeren en door te sturen.

    e. **Activator:** Wordt gebruikt om datasets, query’s en gebeurtenisstromen te controleren op patronen.

    f. **Event Schema Set (preview):** Helpt bij het organiseren en standaardiseren van gegevensstructuren (schema’s) voor uw realtime analyseworkflows, waardoor streaminggegevens consistenter verwerkt en geanalyseerd kunnen worden.

    g. **Custom Stream Connector (preview):** Hiermee kunt u realtime gebeurtenissen vanuit uw eigen aangepaste eindpunten en aangepaste applicaties naar een eventstream verzenden.

    h. **Anomaly detector (Preview):** Detectie van afwijkingen identificeert automatisch ongebruikelijke patronen en uitschieters in uw Eventhouse-tabellen.

    i. **Operations agent (Preview):** Operationele agents automatiseren de cyclus observeren → analyseren → beslissen → handelen. Ze volgen continu belangrijke statistieken, tonen inzichten en bevelen gerichte acties aan.

    j. **Map (preview):** Brengt geografische inzichten naar Real-Time Intelligence, zodat gebruikers kunnen visualiseren waar gebeurtenissen plaatsvinden, ruimtelijke gegevens kunnen integreren met andere Fabric-mogelijkheden en slimmere, locatiebewuste beslissingen kunnen nemen.

    k. **Digital Twin Builder (Preview):** Digital Twin Builder biedt gebruikers low-code/no-code mogelijkheden om hun bedrijfsconcepten, zoals bedrijfsmiddelen en processen, te bouwen en te modelleren via een ontologie.

    **Aan de slag:** 

    Volg deze stappen om Real-Time Intelligence te gaan gebruiken:

    a. **End-to-End Experiences in Real-Time:** Klik op de knop **"Get started"** om realtime gegevensanalyse met voorbeeldgegevens te verkennen.

    b. **Explore Real-Time Intelligence Sample:** Klik op de knop **"Open"** om realtime gegevensanalyse met een voorbeeld te verkennen.

    c. **Explore an Eventhouse Sample:** Klik op de knop **"Select"** om een voorbeeld te gebruiken en meer te leren over Real-Time Intelligence.

    d. **Introduction to Real-Time Intelligence:** Klik op de knop **"Open"** om een overzicht van Real-Time Intelligence te krijgen en het hulpmiddel effectief te gaan gebruiken.

    e. **Learn KQL with Sample Data:** Klik op de knop **"Open"** om KQL te leren met behulp van voorbeeldgegevens.

    f. **What's a Real-Time Hub:** Klik op de knop **"Open"** om te leren wat een Real-Time Hub is en hoe deze gebruikt kan worden.

    g. **Explore a Sample Activator:** Klik op de knop **"Open"** om een voorbeeld-activator te gebruiken en de functies en mogelijkheden van Real-Time Intelligence te begrijpen.

    h. **Get Started with Activator:** Klik op de knop **"Open"** om kennis te maken met Activator-concepten en het hulpmiddel effectief te gaan gebruiken.

    ![](../media/Lab-2/image28.png)

3. Klik linksboven op het scherm op **Return to workloads**. Deze actie brengt u terug naar de hoofdpagina van Workloads, waar u andere hulpmiddelen of secties kunt verkennen.

    ![](../media/Lab-2/image24.png)

## Taak 7: Data Engineering-ervaring

1. Klik op de pagina **Workloads** op **Data Engineering** om verder te gaan.

   ![](../media/Lab-2/image29.png)

2. U wordt doorgestuurd naar de startpagina van **Data Engineering**. Hieronder vindt u een gedetailleerd overzicht van de verschillende onderdelen, ontworpen om u stap voor stap te helpen **Data Engineering** effectief te gebruiken.

    **Wat is Data Engineering?**

    Data Engineering is een hulpmiddel waarmee u infrastructuren en systemen kunt ontwerpen, bouwen en onderhouden voor het verzamelen, opslaan, verwerken en analyseren van grote hoeveelheden gegevens. Hiermee kunt u een Lakehouse maken en uw workflow operationeel inzetten om uw gegevensomgeving op te bouwen, te transformeren en te delen.

    **Itemtypen:**

    a. **Lakehouse:** Wordt gebruikt om big data op te slaan voor opschoning, query's, rapportage en delen.

    b. **Notebook:** Wordt gebruikt voor gegevensopname, voorbereiding, analyse en andere gegevensgerelateerde taken met behulp van verschillende talen zoals Python en Scala.

    c. **Omgeving:** Wordt gebruikt om gedeelde bibliotheken, Spark-rekeninstellingen en bronnen voor notebooks en Spark-taakdefinities in te stellen.

    d. **Spark-taakdefinitie:** Wordt gebruikt om Apache-taken te definiëren, plannen en beheren.

    e. **Gebruikersgegevensfuncties:** Een platform waarmee u toepassingen in Fabric kunt hosten en uitvoeren.

    f. **API voor GraphQL:** Dit is een API om meerdere gegevensbronnen te raadplegen.

    g. **Snowflake-database:** Hiermee kunnen gebruikers een Snowflake-database spiegelen binnen Fabric.

    **Aan de slag:**

    Volg deze stappen om Data Engineering te gebruiken:

    a. **Een voorbeeld verkennen:** Klik op de knop **Selecteren** om een voorbeeld te gebruiken en meer te leren over Data Engineering.

    b. **Wat is een Lakehouse?:** Klik op de knop **Openen** om meer te leren over Lakehouses en hoe deze kunnen worden gebruikt.

    c. **Gegevenservaring in Lakehouse:** Klik op de knop **Openen** om aan de slag te gaan met Data Engineering met behulp van Lakehouses.

    d. **Aan de slag met Spark-taakdefinities:** Klik op de knop **Openen** om te leren hoe u Spark-taakdefinities kunt gebruiken voor gegevensverwerking.

    e. **Notebooks ontwikkelen en uitvoeren:** Klik op de knop **Openen** om te leren hoe u notebooks kunt ontwikkelen en uitvoeren voor gegevensanalyse.

    f. **NotebookUtils gebruiken:** Klik op de knop **Openen** om te leren hoe u NotebookUtils kunt gebruiken voor verbeterde gegevensanalyse.

    g. **Notebooks gebruiken voor uw Lakehouse:** Klik op de knop **Openen** om te leren hoe u notebooks kunt inzetten voor uw Lakehouse.

    h. **Datasets gebruiken voor uw Lakehouse:** Klik op de knop **Openen** om te leren hoe u datasets kunt inzetten voor uw Lakehouse.

    i. **Uw eerste gebruikersgegevensfuncties maken:** Klik op de knop **Openen** om te leren hoe u gebruikersgegevensfuncties maakt.

    j. **Uw eerste API voor GraphQL maken:** Klik op de knop **Openen** om te leren hoe u een API voor GraphQL maakt.

    ![](../media/Lab-2/image30.png)

3. Klik linksboven in het scherm op **Terug naar workloads**. Deze actie brengt u terug naar de hoofdpagina met workloads, waar u andere hulpmiddelen of secties kunt verkennen.

   ![](../media/Lab-2/image24.png)

## Taak 8: Data Science-ervaring

1. Klik op de pagina **Workloads** op **Data Science** om verder te gaan.

   ![](../media/Lab-2/image31.png)

2. U wordt doorgestuurd naar de startpagina van **Data Science**. Hieronder vindt u een gedetailleerd overzicht van de verschillende onderdelen, ontworpen om u te helpen **Data Science** effectief te gebruiken.

    **Wat is Data Science?**

    Data Science is een hulpmiddel waarmee u krachtige inzichten kunt verkrijgen met behulp van AI- en machinelearningtechnologie. Het biedt AI-hulpmiddelen die zijn ontworpen om u te helpen volledige Data Science-workflows uit te voeren en AI te benutten voor gegevensverrijking en bedrijfsinzichten.

    **Itemtypen:**

    a. **ML-model:** Wordt gebruikt om machinelearningmodellen te maken.

    b. **Experiment:** Wordt gebruikt om de ontwikkeling van meerdere modellen te maken, uit te voeren en te volgen.

    c. **Notebook:** Wordt gebruikt om gegevens te verkennen en machinelearningoplossingen op te bouwen.

    d. **Omgeving:** Wordt gebruikt om gedeelde bibliotheken, Spark-rekeninstellingen en bronnen voor notebooks en Spark-taakdefinities in te stellen.

    e. **Data Agent (preview):** Wordt gebruikt om conversatiegestuurde AI-ervaringen te creëren die vragen beantwoorden over gegevens die zijn opgeslagen in Lakehouses, Warehouses, Power BI-semantische modellen en KQL-databases.

    f. **Python Notebook:** Wordt gebruikt om Python-notebooks vanaf een lokale computer te importeren.

    **Aan de slag:**

    Volg deze stappen om Data Science te gebruiken:

    a. **Een voorbeeld verkennen:** Klik op de knop **Selecteren** om een voorbeeld te gebruiken en meer te leren over Data Science.

    b. **Aan de slag met ML-modellen:** Klik op de knop **Openen** om te leren hoe u aan de slag gaat met machinelearningmodellen.

    c. **Aan de slag met ML-experimenten:** Klik op de knop **Openen** om te leren hoe u machinelearningexperimenten uitvoert.

    d. **Aan de slag met Notebooks:** Klik op de knop **Openen** om te leren hoe u aan de slag gaat met notebooks.

    e. **Notebooks ontwikkelen en uitvoeren:** Klik op de knop **Openen** om te leren hoe u notebooks kunt ontwikkelen en uitvoeren voor gegevensanalyse.

    ![](../media/Lab-2/image32.png)

3. Klik linksboven in het scherm op **Terug naar workloads**. Deze actie brengt u terug naar de hoofdpagina met workloads, waar u andere hulpmiddelen of secties kunt verkennen.

   ![](../media/Lab-2/image24.png)

## Taak 9: Data Warehouse-ervaring

1. Klik op de pagina **Workloads** op **Data Warehouse** om verder te gaan.

   ![](../media/Lab-2/image33.png)

2. U wordt doorgestuurd naar de startpagina van Data Warehouse. Hieronder vindt u een gedetailleerd overzicht van de verschillende onderdelen, ontworpen om u stap voor stap te helpen Data Warehouse effectief te gebruiken.

    **Wat is Data Warehouse?**

    Data Warehouse is een hulpmiddel waarmee u gegevens kunt opslaan en analyseren in een beveiligd SQL-warehouse. Het stelt u in staat uw inzichten op te schalen door gebruik te maken van prestaties van topniveau op petabyteschaal in een open gegevensindeling.

    **Itemtypen:**

    a. **Warehouse:** Wordt gebruikt om een Data Warehouse te maken.

    b. **Voorbeeldwarehouse:** Wordt gebruikt om datawarehousingmogelijkheden te verkennen en te testen met vooraf geconfigureerde datasets en modellen.

    c. **Notebook:** Wordt gebruikt voor het maken en delen van interactieve gegevensanalyse- en visualisatietaken.

    d. **Gespiegelde Azure SQL Database:** Wordt gebruikt om Azure SQL Database te spiegelen.

    e. **Gespiegelde Azure Databricks-catalogus:** Wordt gebruikt om gegevens uit Azure Databricks te spiegelen voor verbeterde integratie en analyses.

    f. **Gespiegelde Snowflake:** Wordt gebruikt om een Snowflake-database te spiegelen.

    g. **Gespiegelde Oracle (preview):** Wordt gebruikt om Oracle te spiegelen.

    h. **Gespiegelde Google BigQuery (preview):** Wordt gebruikt om Google BigQuery te spiegelen.

    i. **Gespiegelde Azure Cosmos DB:** Wordt gebruikt om Azure Cosmos DB te spiegelen.

    j. **Gespiegelde SQL Server:** Wordt gebruikt om SQL Server te spiegelen.

    k. **Gespiegelde Azure Database for PostgreSQL:** Wordt gebruikt om uw bestaande Azure Database for PostgreSQL te spiegelen.

    l. **Gespiegelde Azure SQL Managed Instance:** Wordt gebruikt om Azure SQL Managed Databases te spiegelen voor hoge beschikbaarheid en noodherstel.

    m. **Gespiegelde database:** Wordt gebruikt om databases te repliceren voor hoge beschikbaarheid en noodherstel.

    **Aan de slag:**

    Volg de onderstaande stappen om Data Warehouse te gebruiken:

    a. **Een voorbeeldwarehouse verkennen:** Start een nieuw warehouse waarin voorbeeldgegevens al zijn geladen.

    b. **Aan de slag met Warehouse:** Klik op de knop **Openen** om te leren hoe u een warehouse kunt gebruiken om gegevens te analyseren.

    ![](../media/Lab-2/image34.png)

3. Klik linksboven in het scherm op **Terug naar workloads**. Deze actie brengt u terug naar de hoofdpagina met workloads, waar u andere hulpmiddelen of secties kunt verkennen.

   ![](../media/Lab-2/image24.png)

## Taak 10: Databases-ervaring

1. Klik op de pagina **Workloads** op **Databases** om verder te gaan.

   ![](../media/Lab-2/image35.png)

2. U wordt doorgestuurd naar de startpagina van Databases. Hieronder vindt u een gedetailleerd overzicht van de verschillende onderdelen, ontworpen om u te helpen Databases effectief te gebruiken.

    **Wat is een Fabric-database?**

    SQL Database in Microsoft Fabric is een ontwikkelaarsvriendelijke transactionele database, gebaseerd op Azure SQL Database, waarmee u eenvoudig uw operationele database in Fabric kunt maken. Een SQL Database in Fabric maakt gebruik van dezelfde SQL Database Engine als Azure SQL Database.

    **Itemtypen:**

    a. **SQL Database:** SQL Database in Fabric maakt deel uit van de workload **Database** en de gegevens zijn toegankelijk vanuit andere onderdelen in Fabric. De gegevens van uw SQL Database worden ook up-to-date gehouden in een doorzoekbare indeling binnen OneLake, zodat u verschillende Fabric-services kunt gebruiken, zoals het uitvoeren van analyses met Spark, het uitvoeren van notebooks, Data Engineering, visualisaties via Power BI-rapporten en meer.

    b. **Cosmos DB:** Cosmos DB in Microsoft Fabric is een AI-geoptimaliseerde NoSQL-database met een vereenvoudigde beheerervaring. Als ontwikkelaar kunt u Cosmos DB in Fabric gebruiken om AI-toepassingen te bouwen met minder complexiteit en zonder typische databasebeheertaken uit te voeren.

    **Aan de slag:**

    Volg de onderstaande stappen om Databases te gebruiken:

    a. **Verkennen:** Klik op de knop **Openen** om een voorbeelddatabase te verkennen.

    b. **Databaseconcepten:** Beschrijft veelgebruikte termen en concepten rond transactionele databases, zodat u vertrouwd raakt met het werken met SQL Database.

    c. **Databasesjablonen:** Bekijk een bibliotheek met vooraf gemaakte sjablonen van veelgebruikte databaseontwerpen.

    ![](../media/Lab-2/image36.png)

3. Klik linksboven in het scherm op **Terug naar workloads**. Deze actie brengt u terug naar de hoofdpagina met workloads, waar u andere hulpmiddelen of secties kunt verkennen.

   ![](../media/Lab-2/image24.png)

    In dit lab hebben we de Fabric-interface verkend en een Fabric-werkruimte en een Lakehouse gemaakt. In het volgende lab leren we hoe we snelkoppelingen in Lakehouse kunnen gebruiken om verbinding te maken met ADLS Gen2-gegevens en hoe we deze gegevens kunnen transformeren met behulp van weergaven.

# Referenties

Fabric Analyst in a Day (FAIAD) introduceert u aan enkele van de belangrijkste functies die beschikbaar zijn in Microsoft Fabric. In het menu van de service bevat de sectie **Help (?)** koppelingen naar een aantal waardevolle bronnen.

![](../media/Lab-1/image29.png)

Hieronder vindt u nog enkele aanvullende bronnen die u helpen bij uw volgende stappen met Microsoft Fabric.

* Bekijk het blogbericht om de volledige [Microsoft Fabric GA-aankondiging](https://aka.ms/Fabric-Hero-Blog-Ignite23) te lezen.

* Verken Fabric via de [Rondleiding](https://aka.ms/Fabric-GuidedTour).

* Meld u aan voor de [gratis proefversie van Microsoft Fabric](https://aka.ms/try-fabric).

* Bezoek de [Microsoft Fabric-website](https://aka.ms/microsoft-fabric).

* Leer nieuwe vaardigheden door de [Fabric-leermodules](https://aka.ms/learn-fabric) te verkennen.

* Verken de [technische documentatie van Fabric](https://aka.ms/fabric-docs).

* Lees het [gratis e-book over aan de slag gaan met Fabric](https://aka.ms/fabric-get-started-ebook).

* Neem deel aan de [Fabric-community](https://aka.ms/fabric-community) om vragen te stellen, feedback te delen en van anderen te leren.

Lees de meer uitgebreide aankondigingsblogs over Fabric:

* [Blog over Data Factory-ervaring in Fabric](https://aka.ms/Fabric-Data-Factory-Blog)

* [Blog over Synapse Data Engineering-ervaring in Fabric](https://aka.ms/Fabric-DE-Blog)

* [Blog over Synapse Data Science-ervaring in Fabric](https://aka.ms/Fabric-DS-Blog)

* [Blog over Synapse Data Warehousing-ervaring in Fabric](https://aka.ms/Fabric-DW-Blog)

* [Blog over Synapse Real-Time Analytics-ervaring in Fabric](https://aka.ms/Fabric-RTA-Blog)

* [Power BI-aankondigingsblog](https://aka.ms/Fabric-PBI-Blog)

* [Blog over Data Activator-ervaring in Fabric](https://aka.ms/Fabric-DA-Blog)

* [Blog over beheer en governance in Fabric](https://aka.ms/Fabric-Admin-Gov-Blog)

* [Blog over OneLake in Fabric](https://aka.ms/Fabric-OneLake-Blog)

* [Blog over Dataverse- en Microsoft Fabric-integratie](https://aka.ms/Dataverse-Fabric-Blog)

© 2026 Microsoft Corporation. Alle rechten voorbehouden.

Door deze demo/dit lab te gebruiken, gaat u akkoord met de volgende voorwaarden:

De technologie/functionele mogelijkheden die in deze demo/dit lab worden beschreven, worden door Microsoft Corporation geleverd om uw feedback te verkrijgen en u een leerervaring te bieden. U mag deze demo/dit lab uitsluitend gebruiken om dergelijke technologische functies en mogelijkheden te evalueren en feedback aan Microsoft te geven. U mag deze niet voor andere doeleinden gebruiken. U mag deze demo/dit lab of enig onderdeel daarvan niet wijzigen, kopiëren, distribueren, verzenden, weergeven, uitvoeren, reproduceren, publiceren, licentiëren, afgeleide werken maken, overdragen of verkopen.

HET KOPIËREN OF REPRODUCEREN VAN DE DEMO/HET LAB (OF ENIG DEEL ERVAN) NAAR EEN ANDERE SERVER OF LOCATIE VOOR VERDERE REPRODUCTIE OF HERDISTRIBUTIE IS UITDRUKKELIJK VERBODEN.

DEZE DEMO/HET LAB BIEDT BEPAALDE SOFTWARETECHNOLOGIE-/PRODUCTFUNCTIES EN MOGELIJKHEDEN, INCLUSIEF MOGELIJKE NIEUWE FUNCTIES EN CONCEPTEN, IN EEN GESIMULEERDE OMGEVING ZONDER COMPLEXE INSTALLATIE OF CONFIGURATIE VOOR HET HIERBOVEN BESCHREVEN DOEL. DE TECHNOLOGIE/CONCEPTEN DIE IN DEZE DEMO/HET LAB WORDEN WEERGEGEVEN, VERTEGENWOORDIGEN MOGELIJK NIET DE VOLLEDIGE FUNCTIONALITEIT EN WERKEN MOGELIJK NIET OP DEZELFDE MANIER ALS EEN DEFINITIEVE VERSIE. WIJ KUNNEN OOK BESLUITEN GEEN DEFINITIEVE VERSIE VAN DERGELIJKE FUNCTIES OF CONCEPTEN UIT TE BRENGEN. UW ERVARING BIJ HET GEBRUIK VAN DERGELIJKE FUNCTIES EN MOGELIJKHEDEN IN EEN FYSIEKE OMGEVING KAN OOK AFWIJKEN.

**FEEDBACK**. Als u feedback geeft aan Microsoft over de technologie, functies, mogelijkheden en/of concepten die in deze demo/dit lab worden beschreven, verleent u Microsoft kosteloos het recht om uw feedback op welke manier dan ook en voor welk doel dan ook te gebruiken, delen en commercialiseren. U verleent ook kosteloos aan derden eventuele octrooirechten die nodig zijn voor hun producten, technologieën en diensten om specifieke onderdelen van Microsoft-software of -services waarin uw feedback is opgenomen te gebruiken of ermee te communiceren. U zult geen feedback verstrekken die onder een licentie valt die Microsoft verplicht om haar software of documentatie aan derden in licentie te geven omdat wij uw feedback daarin opnemen. Deze rechten blijven van kracht na beëindiging van deze overeenkomst.

MICROSOFT CORPORATION WIJST HIERBIJ ALLE GARANTIES EN VOORWAARDEN MET BETREKKING TOT DE DEMO/HET LAB AF, INCLUSIEF ALLE GARANTIES EN VOORWAARDEN VAN VERHANDELBAARHEID, HETZIJ UITDRUKKELIJK, IMPLICIET OF WETTELIJK, GESCHIKTHEID VOOR EEN BEPAALD DOEL, EIGENDOMSRECHTEN EN NIET-INBREUK. MICROSOFT GEEFT GEEN GARANTIES OF VERTEGENWOORDIGINGEN MET BETREKKING TOT DE NAUWKEURIGHEID VAN DE RESULTATEN, UITVOER DIE VOORTVLOEIT UIT HET GEBRUIK VAN DE DEMO/HET LAB OF DE GESCHIKTHEID VAN DE INFORMATIE IN DE DEMO/HET LAB VOOR WELK DOEL DAN OOK.

**DISCLAIMER**

Deze demo/dit lab bevat slechts een gedeelte van de nieuwe functies en verbeteringen in Microsoft Power BI. Sommige functies kunnen in toekomstige versies van het product worden gewijzigd. In deze demo/dit lab leert u enkele, maar niet alle, nieuwe functies kennen.

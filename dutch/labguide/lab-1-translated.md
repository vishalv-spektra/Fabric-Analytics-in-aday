# Microsoft Fabric - Fabric Analyst in a Day - Lab 1

![](../media/Lab-1/main1.jpg)

# Inhoudsopgave

- Documentstructuur

- Scenario / Probleemstelling

- Overzicht van het Power BI Desktop-rapport

    - Taak 1: Power BI Desktop instellen in de labomgeving

    - Taak 2: Het Power BI Desktop-rapport analyseren

    - Taak 3: Power Queries bekijken

- Referenties

# Documentstructuur

Het lab bevat stappen die de gebruiker kan volgen, met bijbehorende schermafbeeldingen als visuele ondersteuning. In elke schermafbeelding zijn secties gemarkeerd met oranje kaders om de gebieden aan te geven waarop de gebruiker zich moet richten.

>**Opmerking:** Sommige schermafbeeldingen kunnen verouderd zijn vanwege doorlopende productupdates.

# Scenario / Probleemstelling

Fabrikam, Inc. is een groothandelaar in nieuwheidsartikelen. Als groothandelaar zijn Fabrikams klanten voornamelijk bedrijven die doorverkopen aan particulieren. Fabrikam verkoopt aan retailklanten in de gehele Verenigde Staten, waaronder speciaalzaken, supermarkten, computerwinkels en souvenirwinkels bij toeristische attracties. Fabrikam verkoopt ook aan andere groothandelaren via een netwerk van agenten die de producten namens Fabrikam promoten. Hoewel alle klanten van Fabrikam momenteel gevestigd zijn in de Verenigde Staten, is het bedrijf van plan om uit te breiden naar andere landen en regio's.

U bent een Data Analyst in het verkoopteam. U verzamelt, reinigt en interpreteert datasets om zakelijke problemen op te lossen. U stelt ook visualisaties samen zoals grafieken en diagrammen, schrijft rapporten en presenteert deze aan de besluitvormers binnen de organisatie.

Om waardevolle inzichten uit de data te halen, haalt u data op uit meerdere systemen, reinigt u deze en combineert u deze. U haalt data op uit de volgende bronnen:

- **Verkoopdata:** afkomstig uit het ERP-systeem; de data wordt opgeslagen in een ADLS Gen2-database. Deze wordt elke dag om 12:00 uur 's middags bijgewerkt.

- **Leveranciersdata:** afkomstig van verschillende leveranciers; de data wordt opgeslagen in een Snowflake-database. Deze wordt elke dag om 12:00 uur 's nachts bijgewerkt.

- **Klantdata:** afkomstig uit Customer Insights; de data wordt opgeslagen in Dataverse. De data is altijd actueel.

- **Medewerkerdata:** afkomstig uit het HR-systeem; deze wordt opgeslagen als exportbestand in een SharePoint-map. De data wordt elke ochtend om 09:00 uur bijgewerkt.

![](../media/Lab-1/image6.png)

U bouwt momenteel een semantisch model in Power BI Premium dat data ophaalt uit de bovenstaande bronsystemen om te voldoen aan uw rapportagebehoeften en om eindgebruikers de mogelijkheid te bieden om zelfstandig analyses uit te voeren. U gebruikt Power Query om uw model bij te werken.

**U wordt geconfronteerd met de volgende uitdagingen:**

- U moet uw dataset minimaal drie keer per dag vernieuwen om tegemoet te komen aan de verschillende updatetijden van de verschillende databronnen.

- Uw vernieuwingen duren lang omdat u elke keer een volledige vernieuwing moet uitvoeren om eventuele wijzigingen in de bronsystemen te verwerken.

- Fouten in een van de databronnen waaruit u data ophaalt, leiden ertoe dat uw datasetvernieuwing mislukt. Het medewerkerbestand wordt vaak niet op tijd geüpload, waardoor uw datasetvernieuwing mislukt.

- Het kost veel tijd om wijzigingen aan uw datamodel aan te brengen, omdat Power Query er lang over doet om uw voorbeeldweergaven te vernieuwen, vanwege de grote datavolumes en complexe transformaties.

- U heeft een Windows-pc nodig om Power BI Desktop te gebruiken, terwijl de bedrijfsstandaard Mac is.

U heeft gehoord over Microsoft Fabric en besloten dit uit te proberen om te zien of het uw uitdagingen kan oplossen.

# Overzicht van het Power BI Desktop-rapport

Voordat we beginnen met Fabric, bekijken we het huidige rapport in Power BI Desktop om de transformaties en het model te begrijpen.

## Taak 1: Power BI Desktop instellen in de labomgeving

1. Open het bestand **FAIAD.pbix** in de map **Reports** op het **bureaublad** van uw labomgeving. Het bestand wordt geopend in Power BI Desktop.

    ![](../media/Lab-1/image7.png)

   >### **Opmerking:** Als Power BI Desktop niet meer reageert op het scherm **"Voer uw e-mailadres in"** en u niet kunt typen, beweeg dan uw cursor over het Power BI-pictogram op de taakbalk (1). Sluit vervolgens het extra lege (witte) venster door op **X** te klikken (2). Hierdoor reageert het hoofdvenster van Power BI weer.

    ![](../media/Lab-1/powerbidesktop-note.png)

3. Wanneer het dialoogvenster "Voer uw e-mailadres in" verschijnt, kopieert u de **Gebruikersnaam** en plakt u deze in het veld **E-mail** van het dialoogvenster. Selecteer vervolgens **Doorgaan**.

    - E-mail/Gebruikersnaam: <inject key="AzureAdUserEmail"></inject>

        ![](../media/Lab-1/image8.png)


4. Op het tabblad Aanmelden bij Microsoft Azure ziet u het aanmeldscherm. Voer de volgende e-mail/gebruikersnaam in en klik op **Volgende**.

    - E-mail/Gebruikersnaam: <inject key="AzureAdUserEmail"></inject>

        ![](../media/Lab-1/image9.png)


5. Voer nu de volgende **Tijdelijke toegangscode** in en klik op **Aanmelden**.

    - Tijdelijke toegangscode: <inject key="AzureAdUserPassword"></inject>

        ![](../media/Lab-1/image10.png)


6. Het dialoogvenster **Aangemeld blijven bij al uw apps** wordt geopend. Selecteer **OK**.

    ![](../media/Lab-1/image11.png)


7. Het dialoogvenster **U bent helemaal klaar!** wordt geopend. Selecteer **Gereed**.

    Power BI Desktop wordt nu geopend.

## Taak 2: Het Power BI Desktop-rapport analyseren

Het onderstaande rapport analyseert de verkoop voor Fabrikam. KPI's worden linksboven op de pagina weergegeven. De overige visuals lichten de verkoop toe over de tijd, per regio, productgroep en resellersbedrijf.

![](../media/Lab-1/image12.png)

>**Opmerking:** In deze training richten we ons op gegevensverzameling, -transformatie en -modellering met behulp van de beschikbare tools in Fabric. We richten ons niet op rapportontwikkeling of -navigatie. Neem een paar minuten de tijd om het rapport te bekijken en ga daarna verder naar de volgende stappen.


1. Laten we de data analyseren per verkoopgebied. Selecteer **New England in de visual Sales Territory** (spreidingsdiagram). U ziet dat uit de verkoop over de tijd blijkt dat reseller Tailspin Toys meer verkopen heeft dan Wingtip Toys in New England. Als u naar het kolomdiagram Sales YoY% kijkt, ziet u dat de verkoopgroei van Wingtip Toys laag is geweest en kwartaal na kwartaal is gedaald in het afgelopen jaar. Na een kleine opleving in Q3 daalde de verkoop opnieuw in Q4.

    ![](../media/Lab-1/image13.png)


2. Laten we dit vergelijken met het gebied Rocky Mountain. Selecteer **Rocky Mountain in de visual Sales Territory** (spreidingsdiagram). U ziet in het kolomdiagram Sales YoY% dat de verkoop van Wingtip Toys in Q4 van 2023 sterk is gestegen, na twee kwartalen van lage verkoop.

    ![](../media/Lab-1/image14.png)


3. Selecteer **Rocky Mountain in de visual Sales Territory** om het filter te verwijderen.


4. Selecteer in de visual Spreidingsdiagram onderaan het midden van het scherm (Sales Orders by Sales) de uitbijter rechtsboven (4<sup>e</sup> kwadrant). U ziet dat de marge % 52% is, wat boven het gemiddelde van 50% ligt. Ook is de Sales YoY% de laatste twee kwartalen van 2023 gestegen.

    ![](../media/Lab-1/image15.png)


5. Selecteer de uitbijter-reseller in de visual Spreidingsdiagram om **het filter te verwijderen**.


6. Laten we de productdetails bekijken per productgroep en reseller. Klik in de staafdiagramvisual Sales by Product Group and Reseller Company met de **rechtermuisknop op de balk Packaging Materials voor Tailspin Toys** en selecteer in het dialoogvenster **Drillthrough -> Product Detail**.

    ![](../media/Lab-1/image16.png)


7. U wordt doorgestuurd naar de pagina met productdetails. U ziet dat er ook toekomstige orders zijn geplaatst.


8. Wanneer u klaar bent met het bekijken van deze pagina, selecteert u de **Ctrl+pijl-terug** linksboven op de pagina om terug te keren naar het verkooprapport.

    ![](../media/Lab-1/image17.png)


9. U kunt het rapport verder analyseren. Wanneer u klaar bent, bekijken we de modelweergave. Selecteer in het linkerdeelvenster het **pictogram Modelweergave**.
         
    ![](../media/Lab-1/image18.png)

10. U ziet dat er twee feitentabellen zijn: Sales en PO.

    1. De granulariteit van de verkoopdata is op datum, reseller, product en medewerker. Datum, reseller, product en medewerker zijn gekoppeld aan Sales.

    2. De granulariteit van de PO-data is op datum, product en medewerker. Datum, product en medewerker zijn gekoppeld aan PO.

    3. We hebben leveranciersdata per product. Leverancier is gekoppeld aan Product.

    4. We hebben locatiedata van resellers per regio. Geo is gekoppeld aan Reseller.

    5. We hebben klantinformatie per reseller. Klant is gekoppeld aan Reseller.

## Taak 3: Power Queries bekijken

1. Laten we Power Query bekijken om de databronnen te begrijpen. Selecteer in het lint **Start -> Gegevens transformeren**.
    
    ![](../media/Lab-1/image19.png)

2. Het Power Query-venster wordt geopend. Selecteer in het lint **Start -> Instellingen voor gegevensbron**. Het dialoogvenster Instellingen voor gegevensbron wordt geopend. Terwijl u door de lijst scrolt, ziet u dat er vier databronnen zijn zoals vermeld in de probleemstelling:

    - Snowflake

    - SharePoint

    - ADLS Gen2

    - Dataverse


3. Selecteer **Sluiten** om het dialoogvenster Instellingen voor gegevensbron te sluiten.

    ![](../media/Lab-1/image20.png)


4. In het linkerdeelvenster Queries ziet u dat de queries zijn gegroepeerd per databron.


5. U ziet dat de map **DataverseData** klantdata bevat die beschikbaar is in vier verschillende queries: BabyBoomer, GenX, GenY en GenZ. Deze vier queries worden samengevoegd om de query Customer te maken.


6. Klik op de query Customer in het venster Queries. Als u deze query selecteert, moet u uw Dataverse-referenties opnieuw invoeren. Klik op **Referenties bewerken**.

    ![](../media/Lab-1/image21.png)


7. Klik op **Aanmelden** om u aan te melden bij uw account.
    
    ![](../media/Lab-1/image22.png)

8. U kunt de referenties voor de Dataverse-gegevensbron invoeren door de **Gebruikersnaam** en het **Wachtwoord** in te geven. De referenties worden hieronder verstrekt. Selecteer **Verbinding maken** wanneer u klaar bent.

    - E-mail/Gebruikersnaam: <inject key="AzureAdUserEmail"></inject>

    - Wachtwoord: <inject key="AzureAdUserPassword"></inject>

9. Klik op de query **ADLS Base Folder** in het venster Queries. Als u deze query selecteert, zijn referenties vereist. Klik op **Referenties bewerken**.
         
    ![](../media/Lab-1/image23.png)

10. Kies voor de ADLS-gegevensbron de optie **Shared access signature (SAS)** en voer het onderstaande **SAS token** in. Selecteer vervolgens **Verbinding maken**.

    - **SAS token:** <inject key="Sas token"></inject>

        ![](../media/Lab-1/image24.png)

11. U ziet dat de map **ADLSData** meerdere dimensies bevat: Geo, Product, Reseller en Date. Deze bevat ook verkoopfeiten.

    - De **dimensie Geo** wordt gemaakt door data samen te voegen uit de queries Cities, Countries en States.

    - De **dimensie Product** wordt gemaakt door data samen te voegen uit de queries Product Groups en Product Item Group.

    - De **dimensie Reseller** wordt gefilterd met behulp van de query BuyingGroup.

    - Het **feit Sales** wordt gemaakt door InvoiceLineItems samen te voegen met de query Invoice.

12. Selecteer voor de Snowflake-gegevensbron de query **SupplierCategories** in het venster Queries. Als u deze query selecteert, wordt u om referenties gevraagd. Klik op **Referenties bewerken**.
         
    ![](../media/Lab-1/image25.png)


13. Voer de onderstaande **Snowflake-gebruikersnaam** en het **Snowflake-wachtwoord** in. Gebruik deze referenties om alle tabellen onder Snowflake te verbinden met Snowflake en selecteer vervolgens **Verbinding maken**.

    * **Snowflake-gebruikersnaam:** <inject key="SnowFlake Username" enableCopy="false" />

    * **Snowflake-wachtwoord:** <inject key="SnowFlake Password" enableCopy="false" />

      >**Opmerking:** Als u problemen ondervindt bij het verbinding maken met Snowflake met de bovenstaande referenties, gebruik dan de onderstaande reservereferenties.

    - **Snowflake-gebruikersnaam:** SNOWFLAKE_BACKUP

    - **Snowflake-wachtwoord:** 8UpfRpExVDXv2AC1

14. U ziet dat de map **SnowflakeData** de dimensie Supplier en het feit PO (Order/Besteding) bevat.

    - De **dimensie Supplier** wordt gemaakt door de query Suppliers samen te voegen met de query SupplierCategories.

    - Het **feit PO** wordt gemaakt door PO samen te voegen met de query PO Line Items.


15. Selecteer voor de SharePoint-gegevensbron de query **People** in het venster Queries. Als u deze query selecteert, wordt u om referenties gevraagd. Klik op **Referenties bewerken**.

    ![](../media/Lab-1/image26.png)

16. Selecteer de optie **Microsoft-account** en klik vervolgens op **Aanmelden**. Voer de onderstaande gebruikersnaam en het wachtwoord in en selecteer vervolgens **Verbinding maken**.

    - **E-mail/Gebruikersnaam:** <inject key="AzureAdUserEmail"></inject>

    - **Wachtwoord:** <inject key="AzureAdUserPassword"></inject>

        ![](../media/Lab-1/image27.png)


17. U ziet dat de map **SharepointData** de dimensie People bevat.

    ![](../media/Lab-1/image28.png)

    Nu weten we waarmee we te maken hebben. In de volgende labs maken we een vergelijkbare Power Query met Dataflow Gen2 en voeren we modellering uit met behulp van een Lakehouse.

# Referenties

Fabric Analyst in a Day (FAIAD) introduceert u aan een aantal van de belangrijkste functies die beschikbaar zijn in Microsoft Fabric. In het menu van de service vindt u in de sectie Help (?) koppelingen naar uitstekende bronnen.

![](../media/Lab-1/image29.png)

Hier zijn nog enkele aanvullende bronnen die u helpen bij uw volgende stappen met Microsoft Fabric.

- Lees de blogpost voor de volledige [aankondiging van Microsoft Fabric GA](https://aka.ms/Fabric-Hero-Blog-Ignite23)

- Verken Fabric via de [Begeleide rondleiding](https://aka.ms/Fabric-GuidedTour)

- Meld u aan voor de [gratis proefversie van Microsoft Fabric](https://aka.ms/try-fabric)

- Bezoek de [Microsoft Fabric-website](https://aka.ms/microsoft-fabric)

- Leer nieuwe vaardigheden door de [Fabric-leermodules](https://aka.ms/learn-fabric) te verkennen

- Verken de [technische documentatie van Fabric](https://aka.ms/fabric-docs)

- Lees het [gratis e-book over aan de slag gaan met Fabric](https://aka.ms/fabric-get-started-ebook)

- Word lid van de [Fabric-community](https://aka.ms/fabric-community) om uw vragen te stellen, feedback te delen en van anderen te leren

Lees de meer gedetailleerde aankondigingsblogs over Fabric-ervaringen:

- [Blog over de Data Factory-ervaring in Fabric](https://aka.ms/Fabric-Data-Factory-Blog)

- [Blog over de Synapse Data Engineering-ervaring in Fabric](https://aka.ms/Fabric-DE-Blog)

- [Blog over de Synapse Data Science-ervaring in Fabric](https://aka.ms/Fabric-DS-Blog)

- [Blog over de Synapse Data Warehousing-ervaring in Fabric](https://aka.ms/Fabric-DW-Blog)

- [Blog over de Synapse Real-Time Analytics-ervaring in Fabric](https://aka.ms/Fabric-RTA-Blog)

- [Aankondigingsblog over Power BI](https://aka.ms/Fabric-PBI-Blog)

- [Blog over de Data Activator-ervaring in Fabric](https://aka.ms/Fabric-DA-Blog)

- [Blog over beheer en governance in Fabric](https://aka.ms/Fabric-Admin-Gov-Blog)

- [Blog over OneLake in Fabric](https://aka.ms/Fabric-OneLake-Blog)

- [Blog over de integratie van Dataverse en Microsoft Fabric](https://aka.ms/Dataverse-Fabric-Blog)

© 2026 Microsoft Corporation. Alle rechten voorbehouden.

Door gebruik te maken van deze demo/dit lab stemt u in met de volgende voorwaarden:

De technologie/functionaliteit die in deze demo/dit lab wordt beschreven, wordt door Microsoft Corporation aangeboden met als doel uw feedback te verkrijgen en u een leerervaring te bieden. U mag de demo/het lab uitsluitend gebruiken om dergelijke technologiefuncties en -functionaliteit te evalueren en feedback te geven aan Microsoft. U mag het niet voor enig ander doel gebruiken. U mag deze demo/dit lab of een deel ervan niet wijzigen, kopiëren, distribueren, verzenden, weergeven, uitvoeren, reproduceren, publiceren, in licentie geven, er afgeleide werken van maken, overdragen of verkopen.

HET KOPIËREN OF REPRODUCEREN VAN DE DEMO/HET LAB (OF EEN DEEL DAARVAN) NAAR ENIGE ANDERE SERVER OF LOCATIE VOOR VERDERE REPRODUCTIE OF HERDISTRIBUTIE IS UITDRUKKELIJK VERBODEN.

DEZE DEMO/DIT LAB BIEDT BEPAALDE SOFTWARETECHNOLOGIE-/PRODUCTFUNCTIES EN -FUNCTIONALITEIT, INCLUSIEF MOGELIJKE NIEUWE FUNCTIES EN CONCEPTEN, IN EEN GESIMULEERDE OMGEVING ZONDER COMPLEXE INSTALLATIE OF CONFIGURATIE VOOR HET HIERBOVEN BESCHREVEN DOEL. DE TECHNOLOGIE/CONCEPTEN DIE IN DEZE DEMO/DIT LAB WORDEN GEPRESENTEERD, VERTEGENWOORDIGEN MOGELIJK NIET DE VOLLEDIGE FUNCTIEFUNCTIONALITEIT EN WERKEN MOGELIJK NIET OP DE MANIER WAAROP EEN DEFINITIEVE VERSIE ZOU WERKEN. WIJ KUNNEN OOK BESLUITEN GEEN DEFINITIEVE VERSIE VAN DERGELIJKE FUNCTIES OF CONCEPTEN UIT TE BRENGEN. UW ERVARING MET HET GEBRUIK VAN DERGELIJKE FUNCTIES EN FUNCTIONALITEIT IN EEN FYSIEKE OMGEVING KAN OOK ANDERS ZIJN.

**FEEDBACK**. Als u feedback geeft over de technologiefuncties, functionaliteit en/of concepten die in deze demo/dit lab worden beschreven aan Microsoft, geeft u Microsoft het recht, zonder enige vergoeding, om uw feedback op welke manier dan ook en voor welk doel dan ook te gebruiken, delen en commercialiseren. U geeft ook aan derden, zonder enige vergoeding, alle octrooirechten die nodig zijn voor hun producten, technologieën en diensten om specifieke onderdelen van een Microsoft-software of -service die de feedback omvat te gebruiken of daarmee te communiceren. U zult geen feedback geven die onderworpen is aan een licentie die Microsoft verplicht om haar software of documentatie aan derden in licentie te geven omdat wij uw feedback daarin opnemen. Deze rechten blijven van kracht na het verstrijken van deze overeenkomst.

MICROSOFT CORPORATION WIJST HIERBIJ ALLE GARANTIES EN VOORWAARDEN MET BETREKKING TOT DE DEMO/HET LAB AF, INCLUSIEF ALLE GARANTIES EN VOORWAARDEN VAN VERKOOPBAARHEID, ONGEACHT OF DEZE UITDRUKKELIJK, IMPLICIET OF WETTELIJK ZIJN, GESCHIKTHEID VOOR EEN BEPAALD DOEL, EIGENDOMSRECHT EN NIET-INBREUK. MICROSOFT GEEFT GEEN GARANTIES OF VERKLARINGEN MET BETREKKING TOT DE NAUWKEURIGHEID VAN DE RESULTATEN, DE OUTPUT DIE VOORTKOMT UIT HET GEBRUIK VAN DE DEMO/HET LAB, OF DE GESCHIKTHEID VAN DE INFORMATIE IN DE DEMO/HET LAB VOOR ENIG DOEL.

**VRIJWARING**

Deze demo/dit lab bevat slechts een deel van de nieuwe functies en verbeteringen in Microsoft Power BI. Sommige functies kunnen in toekomstige versies van het product worden gewijzigd. In deze demo/dit lab leert u over enkele, maar niet alle, nieuwe functies.

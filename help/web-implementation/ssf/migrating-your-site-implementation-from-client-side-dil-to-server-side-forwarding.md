---
title: Migrera implementeringen av webbplatsen i Audience Manager från DIL på klientsidan till vidarebefordran på serversidan
description: Lär dig hur du migrerar implementeringen av Audience Manager (AAM) för din webbplats från vidarebefordran på klientsidan DIL till serversidan. Den här självstudiekursen gäller om du har både AAM och Adobe Analytics, och om du skickar träffar från sidan till AAM med DIL-kod (Data Integration Library) och du även skickar träffar från sidan till Adobe Analytics.
product: audience manager
feature: Adobe Analytics Integration
topics: null
activity: implement
doc-type: tutorial
team: Technical Marketing
kt: 1778
role: Developer, Data Engineer
level: Intermediate
exl-id: bcb968fb-4290-4f10-b1bb-e9f41f182115
source-git-commit: 2094d3bcf658913171afa848e4228653c71c41de
workflow-type: tm+mt
source-wordcount: '2333'
ht-degree: 0%

---

# Migrera implementeringen av webbplatsen i Audience Manager från DIL på klientsidan till vidarebefordran på serversidan {#migrating-your-site-s-aam-implementation-from-client-side-dil-to-server-side-forwarding}

Den här självstudiekursen gäller dig om du har både Adobe Audience Manager (AAM) och Adobe Analytics och du för närvarande skickar en träff från sidan till AAM med DIL ([!DNL Data Integration Library]) och dessutom skicka en träff från sidan till Adobe Analytics. Eftersom ni har båda dessa lösningar, och eftersom de båda är en del av Adobe Experience Cloud, har ni möjlighet att följa den bästa metoden att aktivera vidarebefordran på serversidan, vilket gör att [!DNL Analytics] datainsamlingsservrar för att vidarebefordra webbplatsanalysdata i realtid till Audience Manager, i stället för att låta klientkoden skicka ytterligare en träff från sidan till AAM. I den här självstudiekursen får du hjälp med att gå över från den tidigare DIL-implementeringen på klientsidan till den nyare vidarebefordringsmetoden på serversidan.

## Klientsidan (DIL) jämfört med serversidan {#client-side-dil-vs-server-side}

När du jämför och kontrasterar dessa två metoder för att hämta in Adobe Analytics-data i AAM kan det först vara bra att visualisera skillnaderna i följande bild:

![klientsida till serversida](assets/client-side_vs_server-side_aam_implementation.png)

### Implementering av DIL på klientsidan {#client-side-dil-implementation}

Om du använder den här metoden för att hämta Adobe Analytics-data till AAM kommer du att få två träffar från dina webbsidor: En kommer att [!DNL Analytics]och en kommer att AAM (efter att ha kopierat [!DNL Analytics] på webbsidan. [!UICONTROL Segments] returneras från AAM till sidan, där de kan användas för personalisering och så vidare. Detta betraktas som en äldre implementering och rekommenderas inte längre.

Förutom att detta inte följer bästa praxis, är nackdelarna med att använda denna metod bland annat:

* Två träffar på sidan istället för bara ett
* vidarebefordran på serversidan krävs för att dela AAM målgrupper i realtid till [!DNL Analytics]så att implementeringar på klientsidan inte tillåter den här funktionen (och eventuellt andra funktioner i framtiden)

Vi rekommenderar att du går över till en vidarebefordringsmetod på serversidan för AAM implementering.

### Vidarebefordransimplementering på serversidan {#server-side-forwarding-implementation}

Som framgår av bilden ovan kommer en träff från webbsidan till Adobe Analytics. [!DNL Analytics] sedan vidarebefordra dessa data till AAM i realtid, och besökarna utvärderas till AAM egenskaper och [!UICONTROL segments], precis som om träffen hade kommit direkt från sidan.

[!UICONTROL Segments] returneras vid samma träff i realtid tillbaka till [!DNL Analytics]som vidarebefordrar svaren till webbsidan för personalisering och så vidare.

Det finns ingen nedtid till att gå över till vidarebefordran på serversidan. Adobe rekommenderar varmt alla som har både Audience Manager och [!DNL Analytics] använder den här implementeringsmetoden.

## Du har två huvuduppgifter {#you-have-two-main-tasks}

Det finns en hel del information på den här sidan, och allt är förstås viktigt. Men **allt handlar om två saker som du behöver göra**:

1. Ändra koden från DIL-kod på klientsidan till kod för vidarebefordran på serversidan
1. Vänd knappen i [!DNL Analytics] [!DNL Admin Console] för att starta den faktiska dataöverföringen (per [!UICONTROL report suite])

Om du hoppar över någon av dessa åtgärder kommer vidarebefordran på serversidan inte att fungera korrekt. Steg och ytterligare data har lagts till i det här dokumentet för att hjälpa dig att göra de här två stegen på rätt sätt under installationen.

## Implementeringsalternativ {#implementation-options}

När du går över från klientsidan till serversidan är en av de uppgifter du kommer att ha att ändra koden till den nya koden för vidarebefordring på serversidan. Detta görs med något av följande alternativ:

* Adobe Experience Platform-taggar - Adobe rekommenderade implementeringsalternativ för webbegenskaper. Du kommer att se att det här är en enkel uppgift eftersom plattformstaggar har gjort allt det hårda arbete som du har gjort.
* På sidan - Du kan också placera den nya SSF-koden direkt i `doPlugins` i `appMeasurement.js` om du inte (än) använder Adobe Launch
* Andra tagghanterare - Dessa kan behandlas på samma sätt som föregående (på sidan) alternativ, eftersom du fortfarande placerar SSF-koden i `doPlugins`, oavsett var den andra tagghanteraren lagrar [!DNL AppMeasurement] kod

Vi tittar på de här nedan i _Uppdatera koden_ -avsnitt.

## Implementeringssteg {#implementation-steps}

I följande steg beskrivs implementeringen.

### Steg 0: Krav: Experience Cloud ID-tjänst (ECID) {#step-prerequisite-experience-cloud-id-service-ecid}

Den viktigaste förutsättningen för att gå över till vidarebefordran på serversidan är att Experience Cloud ID-tjänsten är implementerad. Detta är enklast om du använder Experience Platform Launch, och då installerar du bara ECID-tillägget så gör det resten.

Om du använder ett TMS som inte är Adobe eller inget TMS alls måste du implementera ECID för att köra **före** andra Adobe-lösningar. Se [ECID-dokumentation](https://experienceleague.adobe.com/docs/id-service/using/home.html) för mer information. Den enda andra förutsättningen är kodversioner, så när du bara använder de senaste versionerna av koden i följande steg kommer du att klara dig.

>[!NOTE]
>
>Läs hela dokumentet innan du implementerar det. Avsnittet&quot;Timing&quot; nedan innehåller viktig information om *när* implementera varje del, inklusive ECID (om den ännu inte implementerats).

### Steg 1: Registrera alternativ som används från DIL-kod {#step-record-currently-used-options-from-dil-code}

När du är redo att gå från DIL-kod på klientsidan till vidarebefordran på serversidan är det första steget att identifiera allt du gör med DIL-kod, inklusive anpassade inställningar och data som skickas till AAM. Några saker att tänka på:

* Normal [!DNL Analytics] variabler, använda `siteCatalyst.init` DIL-modulen - du behöver inte bekymra dig om den här, eftersom jobbet är att skicka det vanliga [!DNL Analytics] -variabler, och det sker genom att vidarebefordran på serversidan helt enkelt aktiveras.
* Partnerunderdomän - I `DIL.create` funktionen, gör en anteckning om `partner` parameter. Detta kallas din&quot;partnerunderdomän&quot; eller ibland&quot;partner-ID&quot; och kommer att behövas när du placerar den nya koden för vidarebefordran på serversidan.
* [!DNL Visitor Service Namespace] - Kallas även[!DNL Org ID]&quot; eller &quot;[!DNL IMS Org ID],&quot; behöver du det här också när du skapar den nya koden för vidarebefordran på serversidan. Notera det.
* containerNSID, uidCookie och andra avancerade alternativ - Anteckna eventuella ytterligare avancerade alternativ som du använder så att du kan ange dem även i koden för vidarebefordran på serversidan.
* Ytterligare sidvariabler - Om andra variabler skickas till AAM från sidan (utöver de normala) [!DNL Analytics] variabler som hanteras av siteCatalyst.init) måste du anteckna dem så att de kan skickas in via vidarebefordran på serversidan (mellanlagringsvarning: via [!DNL contextData] variabler).

### Steg 2: Uppdatera koden {#step-updating-the-code}

I [Implementeringsalternativ](#implementation-options) (ovan) anges flera alternativ för hur och var du implementerar vidarebefordran på serversidan. För att detta avsnitt ska bli effektivt måste vi dela upp det i dessa avsnitt (med två av dem kombinerade). Gå till den metod i det här avsnittet som bäst beskriver dina behov.

#### Adobe Experience Platform-taggar {#launch-by-adobe}

Titta på videon nedan om du vill veta mer om hur du flyttar implementeringsalternativ från DIL-kod på klientsidan till vidarebefordran på serversidan i Experience Platform Launch.

>[!VIDEO](https://video.tv.adobe.com/v/26310/?quality=12)

#### &quot;On the page&quot; eller non-Adobe tag manager {#on-the-page-or-non-adobe-tag-manager}

Titta på videon nedan om du vill veta mer om hur du flyttar implementeringsalternativ från DIL-kod på klientsidan till vidarebefordran på serversidan i [!DNL AppMeasurement] -kod som finns antingen i en fil eller i ett tagghanteringssystem som inte är Adobe.

>[!VIDEO](https://video.tv.adobe.com/v/26312/?quality=12)

### Steg 3: Aktivera vidarebefordran (per [!UICONTROL Report Suite]) {#step-enabling-the-forwarding-per-report-suite}

Än så länge har vi ägnat all vår tid åt att växla från DIL-kod på klientsidan till vidarebefordran på serversidan. Det är bra, eftersom det är den svåraste delen. Det här avsnittet är lika viktigt som att uppdatera koden, även om det är superenkelt. I den här videon får du se hur du kan vända på den övergång som gör att data kan skickas från Analytics till Audience Manager.

>[!VIDEO](https://video.tv.adobe.com/v/26355/?quality-12)

**OBS!** Som framgår av videon tar det upp till 4 timmar innan vidarebefordran kan genomföras till fullo på Experience Cloud backend.

## Timing {#timing}

Som en påminnelse finns det två huvuduppgifter för att gå över från DIL på klientsidan till vidarebefordran på serversidan:

1. Uppdatera koden
1. Vända knappen i [!DNL Analytics] [!DNL Admin Console]

Men frågan är vem gör du först? Spelar det någon roll? Det var två frågor. Men svaren beror på.. *kan* materia. Hur är det vagt? Låt oss bryta ned den. Men först ytterligare en fråga som kan uppstå om du är en stor organisation med många webbplatser: Måste jag göra allt på en gång? Den där är lite lättare. Nepp. Du kan göra det bit för bit.

### Lite djupdykning {#a-little-deeper-dive}

Orsaken till varför timing och beställning spelar roll är hur vidarebefordran sker _riktigt_ verk, som kan sammanfattas i följande tekniska fakta:

* Om du har implementerat Experience Cloud ID-tjänsten (ECID) och växeln i [!DNL Analytics] [!DNL Admin Console] (&quot;växeln&quot;) är aktiverad, data kommer att vidarebefordras från [!DNL Analytics] till AAM, även om du inte har uppdaterat koden än.
* Om du inte har ECID implementerat kommer data inte att vidarebefordras, även om du har växeln på och har vidarebefordringskoden på serversidan.
* Vidarebefordringskoden på serversidan (i plattformstaggar eller på sidan) hanterar svaret och är nödvändig för att slutföra migreringen.
* Kom ihåg att vidarebefordringsväxeln på serversidan aktiveras av [!UICONTROL report suite], men att koden hanteras av egenskapen i Platform-taggar, eller av [!DNL AppMeasurement] om du inte använder plattformstaggar.

### God praxis {#best-practices}

Baserat på dessa tekniska detaljer finns rekommendationer för när och när detta ska ske:

#### Om du INTE har ECID ännu {#if-you-do-not-have-ecid-yet-implemented}

1. Vänd strömbrytaren in [!DNL Analytics] för varje [!UICONTROL report suite] som du aktiverar för vidarebefordran på serversidan.

   1. Vidarebefordran startar inte än eftersom du inte har ECID.

1. Uppdatera koden per webbplats från vidarebefordran på klientsidan DIL till serversidan (detta kan vara i plattformstaggar) eller på sidan, vilket beskrivs i ett annat avsnitt ovan).

   1. Vidarebefordra nu flöden (när du har lagt till ECID), och du bör även få ett korrekt JSON-svar på dina [!DNL Analytics] fyr (mer information finns i avsnittet Validering och felsökning nedan).

#### Om du har ECID implementerat {#if-you-do-have-ecid-implemented}

1. Förbered och planera så att du är redo att uppdatera koden från DIL till serversidans vidarebefordran PER [!UICONTROL report suite] som du aktiverar för vidarebefordran på serversidan:

   1. Vänd strömbrytaren in [!DNL Analytics] för att möjliggöra vidarebefordran på serversidan.

      1. Vidarebefordran kommer att starta eftersom du har aktiverat ECID.
   1. Uppdatera koden så snart som möjligt från vidarebefordran på klientsidan DIL till ensidig vidarebefordran (detta kan vara i plattformstaggar eller på sidan, vilket beskrivs i ett annat avsnitt ovan).

      1. Du bör få ett korrekt JSON-svar på dina [!DNL Analytics] beacon (se [Validering och felsökning](#validation-and-troubleshooting) för mer information).


>[!NOTE]
>
>Det är viktigt att du utför dessa två steg så nära varandra som möjligt, eftersom du mellan steg 1 och 2 ovan kommer att få en dubblering av data att gå in i AAM. Med andra ord har vidarebefordran av data på en sida börjat skickas från [!DNL Analytics] till AAM, och eftersom DIL-koden fortfarande finns på sidan kommer det också att finnas en träff som går direkt från sidan till AAM, vilket fördubblar informationen. Så snart du uppdaterar koden från DIL till vidarebefordran på serversidan kommer detta att undvikas.

>[!NOTE]
>
>Om du hellre vill ha en liten avvikelse i data än en liten dubblett av data kan du ändra ordningen i steg 1 och 2 ovan. Om du flyttar koden från DIL till vidarebefordran på serversidan avbryts dataflödet till AAM tills du kan vända på växeln för att aktivera vidarebefordran på serversidan för [!UICONTROL report suite]. Vanligtvis vill kunderna hellre ha en liten dubblering av data än att missa att få besökare i sina egenskaper och [!UICONTROL segments].

#### Migreringstidsinställning när du har många webbplatser och [!UICONTROL report suites] {#migration-timing-when-you-have-many-sites-and-report-suites}

Detta ämne behandlas kortfattat i tidigare avsnitt, i den meningen att huvudstrategin kan sammanfattas av följande:

Migrera en webbplats/[!UICONTROL report suite] (eller grupp av platser/[!UICONTROL report suites]) i taget.

Detta kan dock bli lite knepigt baserat på några möjliga scenarier:

* Du har en plats som innehåller flera olika [!UICONTROL report suites]
* Du har en [!UICONTROL report suite] som innehåller flera webbplatser (som en global [!UICONTROL report suite])
* Du använder en plattformstaggegenskap för att täcka flera webbplatser
* Du har olika utvecklingsteam för olika webbplatser

På grund av dessa objekt kan det bli lite komplicerat. Det bästa jag kan föreslå är:

* Ta dig tid att ta fram en strategi för migrering till vidarebefordran på serversidan, baserat på vad som har förklarats ovan
* Baserat på det faktum att en enda egenskap i Platform-taggar (eller en enda [!DNL AppMeasurement] fil) mappar vanligtvis till 1 eller 2 distinkta [!UICONTROL report suites], kommer du antagligen att kunna göra en plan som fungerar på de olika grupperna en i taget och som uppdaterar ditt företag till serversidan
* Om du arbetar med Adobe Consulting kan du prata med dem om din migreringsplan, så att de kan hjälpa dig efter behov

## Validering och felsökning {#validation-and-troubleshooting}

Det viktigaste sättet att verifiera att vidarebefordran på serversidan är igång är att titta på svaret på eventuella Adobe Analytics-träffar som kommer från appen.

Om du inte vidarebefordrar data från servern [!DNL Analytics] till Audience Manager finns det ingen respons på [!DNL Analytics] beacon (förutom en 2x2 pixel). Om du utför vidarebefordran på serversidan finns det dock objekt som du kan verifiera i [!DNL Analytics] förfrågan och svar som meddelar dig om att [!DNL Analytics] kommunicerar korrekt med Audience Manager, vidarebefordrar träffen och får ett svar.

>[!VIDEO](https://video.tv.adobe.com/v/26359/?quality=12)

>[!WARNING]
>
>Se upp för det falska &quot;Success&quot;. Om det finns ett svar, och allt verkar fungera, se till att du har `stuff` -objektet i svaret. Annars kanske du får ett meddelande som säger `"status":"SUCCESS"`. Så galet som det låter är det faktiskt ett bevis på att det INTE fungerar som det ska.
>
>Om du ser detta innebär det att du har slutfört koduppdateringen i plattformstaggar eller [!DNL AppMeasurement], men att vidarebefordran i [!DNL Analytics] [!DNL Admin Console] har inte slutförts ännu. I det här fallet måste du verifiera att du har aktiverat vidarebefordran på serversidan i [!DNL Analytics] [!DNL Admin Console] för [!UICONTROL report suite]. Om du har gjort det, och det inte har gått fyra timmar än, var tålmodig, eftersom det kan ta så lång tid att göra alla nödvändiga ändringar på baksidan.


![false success](assets/falsesuccess.png)

Mer information om vidarebefordran på serversidan finns i [dokumentation](https://experienceleague.adobe.com/docs/analytics/admin/admin-tools/server-side-forwarding/ssf.html).

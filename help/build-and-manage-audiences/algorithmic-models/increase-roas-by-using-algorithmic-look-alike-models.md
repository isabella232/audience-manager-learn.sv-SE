---
title: Öka ROAS genom att använda algoritmiska (lookalike)-modeller i Audience Manager
description: Den verkliga styrkan hos Audience Manager Look-alike-modellering kommer när ni vill utöka er baslinjepublik mot en ny uppsättning kvalitetsanvändare från datakällor från andra och tredje part. I den här självstudiekursen lär du dig hur du skapar en modell utifrån dessa data.
feature: algorithmic models
topics: null
audience: all
activity: use
doc-type: feature video
team: Technical Marketing
kt: 1849
translation-type: tm+mt
source-git-commit: a108c51fdad66f4e7974eb96609b6d8f058cb6ff
workflow-type: tm+mt
source-wordcount: '860'
ht-degree: 0%

---


# Öka ROAS genom att använda algoritmisk (Look-Alike) [!UICONTROL Models] i Audience Manager {#increase-roas-by-using-algorithmic-look-alike-models-in-audience-manager}

Den verkliga kraften hos Audience Manager Look-alike [!UICONTROL Modeling] kommer när du vill utöka din målgrupp mot en ny uppsättning kvalitetsanvändare från [!UICONTROL second party] och [!UICONTROL third party] [!UICONTROL data sources]. I den här självstudiekursen får du lära dig hur du skapar en [!UICONTROL model] utifrån dessa data.

## Aktivera [!UICONTROL Second Party] eller [!UICONTROL Third Party] dataströmmar från Audience Marketplace {#enable-2nd-or-3rd-party-data-streams-from-the-audience-marketplace}

För att kunna använda [!UICONTROL second party]- och [!UICONTROL third party]-data i en look-alike [!UICONTROL model] måste vi först aktivera dessa data i Audience Manager. Adobe har ett stort antal [!UICONTROL second party]- och [!UICONTROL third party] dataleverantörer som du kan välja mellan. Dessa finns i ett självbetjäningsgränssnitt i AAM via Audience Marketplace. Navigera till Audience Marketplace och bläddra bland alternativen. I följande video visas hur du gör detta, inklusive hur du aktiverar kostnadsfria &quot;try before you buy&quot;-strömmar så att du kan låsa in de data som kommer att vara mest användbara för din organisation innan du bestämmer dig för dataleverantörens priser.

För att du ska kunna utforska och avgöra vilken dataleverantör som ska användas är en bra resurs [[!DNL Adobe Audience Finder]](https://www.adobe-audience-finder.com/).

>[!VIDEO](https://video.tv.adobe.com/v/25188/?quality=12)

## Identifiera/skapa en idealisk användare (konvertering) [!UICONTROL trait] eller [!UICONTROL segment] {#identify-create-an-ideal-user-conversion-trait-or-segment}

Vad försöker du få folk att göra på din sajt? Vad är din konverteringshändelse? Det finns förstås många olika svar på den här frågan, beroende på webbplatstyp/vertikal och organisationens mål. I vilket fall som helst är det vanligt att AAM skapar en [!UICONTROL trait] för besökare som uppfyller dessa villkor.

I videon nedan visar jag hur du skapar en konvertering [!UICONTROL trait] som du vill ha på plats när du fortsätter med den här självstudiekursen och skapar en look-alike [!UICONTROL model].

När du använder Adobe Analytics-händelser för att skapa [!UICONTROL traits] finns det dessutom en stor gotcha som du måste tänka på, så att du inte samlar in fler användare än du borde i [!UICONTROL trait]. Titta på följande video för den stora avslöjandet. :)

>[!VIDEO](https://video.tv.adobe.com/v/23431/?quality=12)

**Obs!** I videon ovan förutsätter jag att du har Adobe Analytics. Så är inte fallet. Om du har Google Analytics (GA) har vi en modul som du kan använda för att skicka data till AAM (se [dokumentationen](https://marketing.adobe.com/resources/help/en_US/aam/dil-google-universal-analytics.html)), och om din konverteringsaktivitet på din webbplats skickas till AAM av GA, kan du skapa din konvertering [!UICONTROL trait] utifrån detta. Om du har en annan analyslösning (eller ingen analyslösning) kan du ändå skicka in data till AAM via vår DIL-kod och funktionen `submit` osv. (se [dokumentationen](https://marketing.adobe.com/resources/help/en_US/aam/c_dil.html)). Skapa sedan konverteringen [!UICONTROL trait] baserat på data som skickas när konverteringsaktiviteten utförs på webbplatsen.

## Skapa en Look-alike [!UICONTROL Model] från [!UICONTROL Second Party] eller [!UICONTROL Third Party] Data {#create-a-look-alike-model-from-2nd-or-3rd-party-data}

När vi har slutfört stegen ovan är vi nu redo att skapa en algoritmisk (Look-alike) [!UICONTROL Model]. När vi konfigurerar [!UICONTROL model] kommer vi att använda konverteringen [!UICONTROL trait] som bas [!UICONTROL trait] (nyckelbesökare som vi vill duplicera), och vi kommer att använda den aktiverade [!UICONTROL third party]-dataströmmen som vår personpool att hämta från.

>[!VIDEO](https://video.tv.adobe.com/v/25190/?quality-12)

## En viktig bästa praxis {#an-important-best-practice}

När du skapar algoritmen [!UICONTROL model] i Audience Manager vill vi naturligtvis att [!UICONTROL model] ska vara så effektiv som möjligt. Eftersom [!UICONTROL model] överväger alla [!UICONTROL traits] som medlemmarna i din bas [!UICONTROL trait]/[!UICONTROL segment] är en del av, hjälper det inte [!UICONTROL model] om ALLA personer finns i en [!UICONTROL trait]/[!UICONTROL segment]. Om du har ett supergeneriskt [!UICONTROL traits] (som alla som gick till din webbplats, eller alla som har fått någon annons från dig, osv.) måste du därför se till att det [!UICONTROL data source] som de tillhör INTE ingår i [!UICONTROL data sources] i din [!UICONTROL model]. I den här artikelns användningsexempel är det osannolikt att du skulle göra det, eftersom vi fokuserar på att titta på [!UICONTROL third party]-data för våra nya look-alike, men det är värt att nämnas ändå, och gäller för ALLA dina algoritmiska [!UICONTROL models].

## Skapar en algoritmisk [!UICONTROL Trait] {#creating-an-algorithmic-trait}

Därefter måste vi skapa en algoritmisk [!UICONTROL Trait] så att resultaten från [!UICONTROL model] kan användas. Om du inte skapar en [!UICONTROL trait] är modellen oanvändbar. När [!UICONTROL model] har körts måste du gå till dialogrutan [!UICONTROL trait] och skapa en algoritmisk [!UICONTROL Trait]. I följande video visas några tips.

>[!VIDEO](https://video.tv.adobe.com/v/25191/?quality=12)

## Skapa en [!UICONTROL Segment] från [!UICONTROL Model]-data och skicka den till DSP {#creating-a-segment-from-the-model-data-and-sending-it-to-dsps}

När du har skapat en algoritmisk [!UICONTROL Trait] kan du skapa en ny [!UICONTROL segment] som du kan placera den i, så att du kan aktivera data (du kan inte aktivera en [!UICONTROL trait], utan i stället skapa en ny -[!UICONTROL trait] [!UICONTROL segment] med den algoritmiska [!UICONTROL Trait] i den, så att du kan aktivera (använda) [!UICONTROL segment]).

När du har skapat en [!UICONTROL segment] från denna algoritmisk [!UICONTROL trait] kommer du att ha en målgrupp med potentiella kunder som ser ut som personer som redan har konverterat på din webbplats. Nu kan du mappa denna [!UICONTROL segment] till någon av dina DSP [!UICONTROL destinations] i Audience Manager. Ni kommer att kunna inrikta er på marknadsföring mot de där lookagilla-markeringarna, som är mer benägna att konvertera på er webbplats än bara den vanliga publiken, vilket ökar avkastningen på annonskostnaderna. Lycka till!

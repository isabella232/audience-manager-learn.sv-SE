---
title: Använda lookalike-modeller för att utöka utsålda lager från era första parts data
description: I den här självstudiekursen går vi igenom de steg du bör ta för att konfigurera och använda stilliknande modeller, så att du kan skapa nya lookalike-målgrupper och sälja dem som ett tillägg till ditt konverteringssegment.
feature: algoritmiska modeller
topics: null
audience: all
activity: use
doc-type: feature video
team: Technical Marketing
thumbnail: 23523.jpg
kt: 1688
translation-type: tm+mt
source-git-commit: ba76f9437e5d8f0495e4f2dfafb90cbf2da6454f
workflow-type: tm+mt
source-wordcount: '827'
ht-degree: 0%

---


# Använda Look Alike [!UICONTROL Models] för att utöka utsålt lager från dina [!UICONTROL First Party]-data {#using-look-alike-models-to-extend-sold-out-inventory-from-your-st-party-data}

I den här självstudiekursen går vi igenom de steg du ska ta för att konfigurera och använda Look-Alike [!UICONTROL Models], så att du kan skapa nya lookalike-målgrupper och sälja dem som ett tillägg till din konvertering [!UICONTROL segment].

## Använd ärendeinformation {#use-case-details}

Du är innehållsutgivare. Om du redan har sålt ut lager för konverterare på din webbplats kanske du tror att dina möjligheter upphör där. Ange AAM look-Alike [!UICONTROL Models]. Genom att använda den här funktionen kan ni utöka det sålda lagret ytterligare och även sälja målgrupper som kanske inte har konverterat än, men som ser ut eller beter sig som personer som har konverterat. Den här målgruppen [!UICONTROL segment] skulle vanligtvis sälja för mindre än de faktiska konverterarna, men ändå göra det möjligt för er att utöka resultatet genom att erbjuda ett extra målgruppsalternativ för de annonsörer som vill placera ut annonser på er webbplats. Den ytterligare fördelen med detta användningsexempel är att det inte kostar er något att köra den här modellen på era egna data från första part.

Stegen i den här självstudiekursen är som följer:

1. Identifiera/skapa en idealisk användare (konvertering) [!UICONTROL trait] eller [!UICONTROL segment]
1. Skapa en [!UICONTROL model] med den här konverteringen [!UICONTROL trait]/[!UICONTROL segment] som basobjekt
1. Välj [!UICONTROL First party] datakälla(er) i [!UICONTROL model] och kör [!UICONTROL model]
1. Skapa en algoritmisk [!UICONTROL Trait] från [!UICONTROL model]-resultaten och lägg till [!UICONTROL trait] till en [!UICONTROL segment]
1. Erbjud [!UICONTROL segment] till intresserade annonsörer för att utöka konverteringen [!UICONTROL segment] försäljningen

## Identifiera/skapa en idealisk användare (konvertering) [!UICONTROL trait] eller [!UICONTROL segment] {#identify-create-an-ideal-user-conversion-trait-or-segment}

Vad försöker du få folk att göra på din sajt? Vad är din konverteringshändelse? Det finns förstås många olika svar på den här frågan, beroende på webbplatstyp/vertikal och organisationens mål. I vilket fall som helst är det vanligt att AAM skapar en [!UICONTROL trait] för besökare som uppfyller dessa villkor.

I det här fallet antas detta redan eftersom du har sålt lagret för personer som är konverterare. I den här självstudiekursen kan det dock vara bra att diskutera den som referens för resten av användningsfallet.

När du använder händelser för att skapa [!UICONTROL traits] finns det dessutom en stor gotcha som du måste tänka på, så att du inte samlar in fler användare än du borde i [!UICONTROL trait]. Titta på följande video för den stora avslöjandet. :)

>[!VIDEO](https://video.tv.adobe.com/v/23431/?quality=12)

**Obs!** I videon ovan förutsätter jag att du har Adobe Analytics. Så är inte fallet. Om du har Google Analytics (GA) har vi en modul som du kan använda för att skicka data till AAM (se [dokumentationen](https://marketing.adobe.com/resources/help/en_US/aam/dil-google-universal-analytics.html)). Om din konverteringsaktivitet på din webbplats skickas till AAM av GA kan du skapa din konverteringsegenskap utifrån detta. Om du har en annan analyslösning (eller ingen analyslösning) kan du ändå skicka in data till AAM via vår DIL-kod och funktionen `submit` osv. (se [dokumentationen](https://marketing.adobe.com/resources/help/en_US/aam/c_dil.html)). Sedan skapar du konverteringsegenskapen utifrån de data som skickas när konverteringsaktiviteten utförs på webbplatsen.

## Skapar en Look-Alike [!UICONTROL Model] från [!UICONTROL First Party]-data {#creating-a-look-alike-model-from-first-party-data}

I det här steget ska vi skapa en [!UICONTROL First Party] Look-Alike [!UICONTROL Model]. Det innebär att vi inte bara kommer att använda en [!UICONTROL first party]-konvertering [!UICONTROL trait]/[!UICONTROL segment] för vår bas [!UICONTROL trait]/[!UICONTROL segment] (detta skulle vara normalt för de flesta [!UICONTROL models] ändå), utan vi kommer också att undersöka poolen med [!UICONTROL first party]-data för fler personer som ser ut som konverterarna. Vi kommer inte att titta på [!UICONTROL second party]- eller [!UICONTROL third party]-data.

I det här fallet är detta viktigt, eftersom vi försöker skapa en [!UICONTROL segment]-användare på vår webbplats som ser ut som konverterare men inte har konverterat än, så att vi kan sälja den här lookalike [!UICONTROL segment] till intresserade annonsörer.

>[!VIDEO](https://video.tv.adobe.com/v/23504/?quality-12)

## Skapar en algoritmisk [!UICONTROL Trait] {#creating-an-algorithmic-trait}

Därefter måste vi skapa en algoritmisk [!UICONTROL Trait] så att resultaten från [!UICONTROL model] kan användas. Om du inte skapar en [!UICONTROL trait] är [!UICONTROL model] oanvändbar. När [!UICONTROL model] har körts måste du gå till dialogrutan [!UICONTROL trait] och skapa en algoritmisk [!UICONTROL Trait]. I följande video visas några tips.

>[!VIDEO](https://video.tv.adobe.com/v/23523/?quality=12)

## Erbjuda den algoritmiska [!UICONTROL Segment] till annonsörer {#offering-the-algorithmic-segment-to-advertisers}

När du har skapat en algoritmisk [!UICONTROL Trait] kan du skapa en ny [!UICONTROL segment] som du kan placera den i, så att du kan aktivera data (du kan inte aktivera en [!UICONTROL trait], utan i stället skapa en ny -[!UICONTROL trait] [!UICONTROL segment] med den algoritmiska [!UICONTROL Trait] i den, så att du kan aktivera (använda) [!UICONTROL segment].

När du har skapat en [!UICONTROL segment] av [!UICONTROL first party]-besökare som har fått hög kvalitet i lookalike [!UICONTROL model] (d.v.s. som ser ut som konverterare men ännu inte konverterat), kan du erbjuda denna [!UICONTROL segment] till annonsörer på webbplatsen, även efter att du har sålt ut hela ert lager med konverterare på webbplatsen. Detta är ett bra sätt att utöka den här målgruppen och fortsätta att se ytterligare intäkter genom att använda Look-Alike [!UICONTROL Models] i Audience Manager.

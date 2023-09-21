---
description: I det här avsnittet beskrivs grammatiken för konfigurationsindata, med betoning på giltiga och ogiltiga indataalternativ och hur utelämnade valfria fält tolkas.
title: RBOP-grammatik
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '461'
ht-degree: 0%

---

# RBOP-grammatik {#rbop-grammar}

I det här avsnittet beskrivs grammatiken för konfigurationsindata, med betoning på giltiga och ogiltiga indataalternativ och hur utelämnade valfria fält tolkas.

Den upplösningsbaserade grammatiken för skydd av utdata definieras som en sekvens med regler, där varje regel kan ha flera giltiga former:

```
Rule ::=       
 
    Form 
     
AnotherRule ::=     
 
    DifferentForm 
```

## Använda grammatikregler {#section_A7216BD585FF4EB88737B643B36C2781}

>[!NOTE]
>
>För att förbättra läsbarheten för grammatiken återspeglas följande egenskaper inte i grammatiken, men de har fortfarande värdet true:

1. Ordningen på paren som definieras i objekten är inte fast, vilket innebär att all permutation i paren är giltig.

   Om vi till exempel har definierat ett objekt som detta:

   ```
   {  
     "foo": <Foo>,  
     "bar":<Bar>,  
     "baz":<Baz>  
   }
   ```

   så anses även följande struktur vara giltig: =

   ```
   {  
     "baz":<Baz>,  
     "foo":<Foo>,  
     "bar":<Bar> 
   }
   ```

1. För varje par i ett objekt antas det att endast en instans av det paret finns i en given instans av ett visst objekt.

   Om vi till exempel har definierat ett objekt som detta:

   ```
   {  
     "foo": <Foo>,  
     "bar":<Bar>,  
     "baz":<Baz>  
   }
   ```

   skulle följande instans vara ogiltig eftersom det finns två `foo` par inom samma objekt:

   ```
   { 
     "foo":<Foo>,  
     "bar":<Bar>,  
     "baz":<Baz>,  
   } 
   ```

   Du kan också ha två objekt som:

   ```
   {  
     "foo": <Foo>,  
     "bar":<Bar>,  
     "baz":<Baz>  
   }
   ```

   och:

   ```
   {  
     "baz":<Baz>,  
     "foo":<Foo>,  
     "bar":<Bar> 
   }
   ```

   är giltig eftersom de är oberoende instanser av samma objekt.

1. För definitioner där en eller flera strängsekvenser kan väljas hanterar du strängarna som en uppsättning där dubblettposter behandlas som en enda post. Till exempel: `["foo", "bar", "foo", "baz"]` motsvarar `["foo", "bar", "baz"]`

1. För att definiera tal används ett blanksteg mellan reglerna (t.ex. `Digit Digits`), men inget sådant utrymme ska användas när regeln används.

   Om vi till exempel uttrycker talet *etthundrahundratjugotre* enligt regeln NonZeroInteger ska det uttryckas som `123` i stället för `1 2 3`trots att regeln innehåller ett mellanrum mellan NonZeroDigit och Digits.

1. Vissa regler tillåter flera formulär. I dessa fall separeras de olika formulären med `'|'` tecken.

   Den här regeln:

   ```
   Foo ::= "A" | "B" | "C"
   ```

   betyder att en instans av `Foo` kan ersättas med &quot;A&quot;, &quot;B&quot; eller &quot;C&quot;. Detta ska inte blandas ihop med ett formulär som sträcker sig över flera rader, det vill säga en funktion som gör längre formulär lättare att läsa.

## Grammatiken {#section_52189FD66B1A46BA9F8FDDE1D7C8E8E8}

```
PixelBasedOPConfig ::= 
      {} 
    | { "maxPixel": NonNegativeInteger } 
    | { "pixelConstraints": PixelConstraintsSeq } 
    | { "pixelConstraints": PixelConstraintsSeq, 
        "maxPixel": NonNegativeInteger } 
 
PixelConstraintsSeq ::= 
      [] 
    | [ PixelConstraints ] 
 
PixelConstraints ::= 
      PixelConstraint 
    | PixelConstraint, PixelConstraints 
 
PixelConstraint ::= 
      { "pixelCount": NonNegativeInteger } 
    | { "pixelCount": NonNegativeInteger, 
        "digital": DigitalOutputRestrictionsSeq } 
    | { "pixelCount": NonNegativeInteger, 
        "analog": AnalogOutputRestriction } 
    | { "pixelCount": NonNegativeInteger, 
        "ota": OTAOutputRestriction } 
    | { "pixelCount": NonNegativeInteger, 
        "digital": DigitalOutputRestrictionsSeq, 
        "analog": AnalogOutputRestriction } 
    | { "pixelCount": NonNegativeInteger, 
        "digital": DigitalOutputRestrictionsSeq, 
         "ota": OTAOutputRestriction } 
    | { "pixelCount": NonNegativeInteger, 
        "analog": AnalogOutputRestriction, 
        "ota": OTAOutputRestriction } 
    | { "pixelCount": NonNegativeInteger, 
        "digital": DigitalOutputRestrictionsSeq, 
        "analog": AnalogOutputRestriction, 
        "ota": OTAOutputRestriction } 
 
DigitalOutputRestrictionsSeq ::= 
      [] 
    | [ DigitalOutputRestrictions ] 
 
DigitalRestrictions ::= 
      DigitalRestriction 
    | DigitalRestriction, DigitalRestrictions 
 
DigitalRestriction ::= 
      { "output": DigitalOutputOption } 
    | { "output": DigitalOutputOption, "hdcp": HDCP } 
 
DigitalOutputOption ::= 
      "NO_PROTECTION" 
    | "USE_IF_AVAILABLE" 
    | "REQUIRED" 
    | "NO_PLAYBACK" 
 
HDCP ::= 
    { "major": PositiveInteger, "minor": NonNegativeInteger } 
 
AnalogOutputRestriction ::= 
    { "output": AnalogOutputOption } 
 
AnalogOutputOption ::= 
      "NO_PROTECTION" 
    | "USE_IF_AVAILABLE" 
    | "USE_IF_AVAILABLE_ACP" 
    | "USE_IF_AVAILABLE_CGMSA" 
    | "REQUIRED" 
    | "REQUIRED_ACP" 
    | "REQUIRED_CGMSA" 
    | "NO_PLAYBACK" 
 
OTAOutputRestriction ::= 
    { "whitelist": OTAWhitelistSeq } 
 
OTAWhitelistSeq ::= 
      [] 
    | [ OTAWhitelist ] 
 
OTAWhitelist ::= 
      OTAConnectionType 
    | OTAConnectionType, OTAWhitelist 
 
OTAConnectionType ::= 
      "MIRACAST" 
    | "AIRPLAY" 
    | "WIDI" 
    | "DLNA" 
 
NonNegativeInteger ::= 
      Digit 
    | NonZeroDigit Digits 
 
PositiveInteger ::= 
      NonZeroDigit 
    | NonZeroDigit Digits 
 
Digits ::= 
      Digit 
    | Digit Digits 
 
Digit ::= 
      0 
    | NonZeroDigit

NonZeroDigit ::= 
      1 
    | 2 
    | 3 
    | 4 
    | 5 
    | 6 
    | 7 
    | 8 
    | 9
```

## Semantics: Legal but invalid configurations {#section_709BE240FF0041D4A1B0A0A7544E4966}

The *Exempel på konfiguration för utdataskydd* ämnet visade en giltig konfiguration tillsammans med dess semantiska betydelse. Föregående avsnitt i *this* ämnet presenterade grammatikreglerna för konfigurationer. Grammatiken säkerställer syntaktisk korrekthet, men det finns syntaktiskt juridiska konfigurationer som inte är semantiskt korrekta (dvs. de är inte logiska). I det här avsnittet visas konfigurationer som *syntaktiskt* legal, men *semantiskt* felaktigt. Tänk på att exemplen i det här avsnittet har reducerats till den minimistruktur som krävs för att illustrera det scenario som diskuteras.

* Det är inte tillåtet att definiera flera pixelbegränsningar med samma pixelantal.

  ```
  {  
    "pixelConstraints":  
      [  
        { "pixelCount": 720 }  
      ]  
   }  
  ```

* Ett pixelantal får inte överskrida den högsta angivna pixelupplösningen.

  ```
  { 
    "maxPixel": 720, 
    "pixelConstraints": 
      [ 
        {"pixelCount": 1080} 
      ] 
  } 
  ```

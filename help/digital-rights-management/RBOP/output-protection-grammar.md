---
description: I det här avsnittet beskrivs grammatiken för konfigurationsindata, med betoning på giltiga och ogiltiga indataalternativ och hur utelämnade valfria fält tolkas.
title: RBOP-grammatik
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
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

## Använda grammatikreglerna {#section_A7216BD585FF4EB88737B643B36C2781}

>[!NOTE]
>
>För att förbättra läsbarheten för grammatiken återspeglas följande egenskaper inte i grammatiken, men de har fortfarande värdet true:

1. Ordningen på de par som definieras inom objekten är inte fast. Alla permutationer av paren är alltså giltiga.

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

   kommer följande instans att vara ogiltig eftersom det finns två `foo`-par i samma objekt:

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

1. För definitioner där en eller flera strängsekvenser kan väljas hanterar du strängarna som en uppsättning där dubblettposter behandlas som en enda post. `["foo", "bar", "foo", "baz"]` motsvarar till exempel `["foo", "bar", "baz"]`

1. För att definiera tal används ett mellanrum mellan reglerna (t.ex. `Digit Digits`), men inget sådant mellanrum bör användas när regeln används.

   Om vi till exempel uttrycker talet *etthundra3* per regeln NonZeroInteger, ska det uttryckas som `123` i stället för `1 2 3`, även om regeln innehåller ett mellanrum mellan NonZeroDigit och Digits.

1. Vissa regler tillåter flera formulär. I dessa fall avgränsas de olika formerna av tecknet `'|'`.

   Den här regeln:

   ```
   Foo ::= "A" | "B" | "C"
   ```

   betyder att en instans av `Foo` kan ersättas med A, B eller C. Detta ska inte blandas ihop med ett formulär som sträcker sig över flera rader. som gör längre formulär mer läsbara.

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

## Semantik: Juridiska men ogiltiga konfigurationer {#section_709BE240FF0041D4A1B0A0A7544E4966}

Avsnittet *Sample Output Protection Configuration* innehöll en giltig konfiguration tillsammans med dess semantiska betydelse. I föregående avsnitt i *det här* ämnet presenterades grammatikreglerna för konfigurationer. Grammatiken säkerställer syntaktisk korrekthet, men det finns syntaktiskt juridiska konfigurationer som inte är semantiskt korrekta (dvs. de är inte logiska). I det här avsnittet visas konfigurationer som är *syntaktiskt* juridiskt giltiga, men *semantiskt* felaktiga. Tänk på att exemplen i det här avsnittet har reducerats till den minimistruktur som krävs för att illustrera det scenario som diskuteras.

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

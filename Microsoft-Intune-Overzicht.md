# Microsoft Intune – Overzicht

Dit document geeft een kort overzicht van Microsoft Intune: wat het is, waarom bedrijven het gebruiken en hoe het zich verhoudt tot de klassieke manier om Windows-toestellen te beheren met Group Policy.

## Wat is Microsoft Intune?

Microsoft Intune is een clouddienst om de toestellen en apps die mensen voor hun werk gebruiken te beheren en te beveiligen. Het ondersteunt Windows, macOS, iOS/iPadOS, Android en Linux, allemaal vanuit één beheerportaal (het Intune admin center), zonder dat je een eigen server nodig hebt.

Intune doet twee grote dingen:

- **Mobile Device Management (MDM):** het toestel wordt ingeschreven en het bedrijf beheert het volledig. Intune kan er instellingen, beveiligingspolicies, apps en updates naartoe sturen, controleren of het aan de beveiligingsregels voldoet, en het op afstand vergrendelen of wissen.
- **Mobile Application Management (MAM):** alleen de werkapps en de bedrijfsdata daarin worden beheerd. Dat gebruik je voor persoonlijke toestellen (BYOD), waar het bedrijf zijn data wil beschermen maar niets te zoeken heeft in de rest van de telefoon.

Intune werkt niet alleen. Het steunt op **Microsoft Entra ID** (vroeger Azure AD) voor de identiteit van gebruikers en toestellen, en werkt nauw samen met **Microsoft Defender** voor de beveiliging van toestellen en met **Windows Autopilot** om nieuwe toestellen in te stellen. Intune zit in licenties zoals Microsoft 365 Business Premium en Microsoft 365 E3/E5, maar je kan het ook apart kopen.

## Waarom Intune gebruiken in een werkomgeving?

De manier waarop mensen werken is veranderd. Laptops gaan mee naar huis, medewerkers werken thuis of onderweg, en veel mensen lezen hun werkmail op hun eigen telefoon. Toch moet een bedrijf al die toestellen veilig en up-to-date houden, ook als ze nooit met het bedrijfsnetwerk verbinden. Dat probleem lost Intune op.

**Centraal beheer, overal.** Zolang een toestel internet heeft, krijgt het zijn policies en apps. Een beheerder beheert een laptop in iemands woonkamer op dezelfde manier als een pc op kantoor.

**Beveiliging en compliance.** Intune kan zaken afdwingen zoals BitLocker-versleuteling, een actieve firewall en antivirus, een minimale versie van het besturingssysteem en een pincode of wachtwoord. Toestellen die niet aan die regels voldoen, worden als niet-compliant gemarkeerd. In combinatie met Conditional Access kan je ze de toegang tot bedrijfsdata ontzeggen tot het probleem opgelost is.

**Data beschermen op persoonlijke toestellen.** Met app protection policies kan het bedrijf een pincode eisen op Outlook of Teams, het kopiëren van data naar privéapps blokkeren, en alleen de bedrijfsdata wissen als iemand vertrekt, zonder aan foto's of persoonlijke apps te komen.

**Sneller nieuwe toestellen instellen.** Met Windows Autopilot kan een nieuwe laptop rechtstreeks van de leverancier naar de medewerker. Zodra die zich aanmeldt met zijn werkaccount, installeert Intune automatisch de apps en instellingen. IT hoeft het toestel niet eerst zelf klaar te maken.

**Apps en updates.** Microsoft 365 Apps, apps uit de store en eigen bedrijfssoftware (als Win32-app) kan je uitrollen naar groepen gebruikers of toestellen. Ook Windows-updates beheer en plan je vanuit hetzelfde portaal.

**Acties op afstand en rapportering.** Beheerders zien de status van elk toestel en kunnen op afstand ingrijpen: herstarten, synchroniseren, vergrendelen, resetten of een verloren of gestolen toestel wissen.

## Intune tegenover Group Policy

Group Policy (GPO) is de klassieke manier om Windows-computers te beheren in een Active Directory-domein. Je maakt policies op een domeincontroller en past ze toe op computers en gebruikers in organisatie-eenheden (OU's). Dat werkt al meer dan twintig jaar goed, maar het is gebouwd voor een wereld waarin elke computer op kantoor staat, op het bedrijfsnetwerk.

|  | Group Policy | Microsoft Intune |
| --- | --- | --- |
| Infrastructuur | Eigen domeincontrollers (Active Directory) | Clouddienst, geen servers te onderhouden |
| Verbinding nodig | Toestel moet een domeincontroller bereiken (op kantoor of via VPN) | Eender welke internetverbinding |
| Platformen | Alleen Windows | Windows, macOS, iOS/iPadOS, Android, Linux |
| Koppeling toestel | Lid van het domein (AD) | Entra joined of hybrid joined |
| Doelgroepen | OU's, beveiligingsgroepen, WMI-filters | Entra-groepen, ook dynamische groepen en filters |
| Persoonlijke toestellen (BYOD) | Niet ondersteund | App protection policies (MAM) zonder het toestel in te schrijven |
| Compliance en toegang | Geen ingebouwde compliancecontrole of toegangsbeheer | Compliancepolicies in combinatie met Conditional Access |
| Apps uitrollen | Beperkt (MSI via software installation) | Microsoft 365 Apps, store-apps, Win32-apps, mobiele apps |
| Nieuwe toestellen | Imaging of manuele installatie door IT | Zero-touch met Windows Autopilot |
| Acties op afstand | Geen (extra tools nodig) | Vergrendelen, resetten, wissen, retire, synchroniseren vanuit het portaal |
| Rapportering | Beperkt (bv. gpresult per toestel) | Centrale rapporten over compliance, apps en configuratie |

### Belangrijkste voordelen van Intune

- **Gemaakt voor thuiswerk en hybride werken.** Policies bereiken een toestel waar het ook is, zonder VPN. Bij GPO krijgt een laptop die al weken niet op het bedrijfsnetwerk zat, gewoon zijn nieuwe policies niet.
- **Eén tool voor alle platformen.** Windows, Mac, iPhone en Android beheer je op één plek, in plaats van GPO voor Windows en iets anders voor de rest.
- **Beveiliging op basis van de staat van het toestel.** GPO kan een configuratie instellen, maar kan de toegang niet blokkeren als een toestel niet aan de regels voldoet. Met compliancepolicies en Conditional Access kan dat in Intune wel, wat past bij een Zero Trust-aanpak.
- **Veilig werken op persoonlijke toestellen.** Bedrijfsdata wordt beschermd op privételefoons zonder het hele toestel te beheren.
- **Minder infrastructuur.** Voor toestelbeheer heb je geen domeincontrollers, VPN of SYSVOL-replicatie meer nodig.
- **Sneller in- en uitstromen.** Autopilot zorgt voor nieuwe toestellen, en met retire of wipe verdwijnt de bedrijfsdata als iemand vertrekt.
- **Eenvoudige overstap.** De meeste GPO-instellingen hebben een tegenhanger in de Settings catalog van Intune, en met *Group Policy analytics* kan je bestaande GPO's importeren en zien welke instellingen je kan overzetten.

### Wanneer Group Policy nog zinvol is

Group Policy is niet dood. Organisaties met veel eigen servers, oudere applicaties of heel specifieke oudere instellingen steunen er vaak nog op. Sommige instellingen bestaan alleen als GPO, en GPO zit zonder extra kost in Windows Server. Daarom werken veel bedrijven een tijd hybride: toestellen zijn lid van zowel AD als Entra, en policies verhuizen stap voor stap van GPO naar Intune. Als beide dezelfde instelling toepassen, kan je in Intune instellen dat de MDM-instelling voorrang krijgt op de GPO.

## Besluit

Microsoft Intune verplaatst toestelbeheer van het bedrijfsnetwerk naar de cloud. Group Policy blijft nuttig in klassieke omgevingen met eigen servers, maar het werkt alleen voor Windows-computers die lid zijn van het domein en een domeincontroller kunnen bereiken. Intune beheert alle grote platformen, waar het toestel ook is, koppelt beveiliging aan toegang via compliance en Conditional Access, en beschermt bedrijfsdata op privételefoons. Voor een moderne werkplek met thuiswerk en mobiele toestellen is Intune daarom de logische keuze, met Group Policy vooral voor oudere toepassingen tijdens de overgang.

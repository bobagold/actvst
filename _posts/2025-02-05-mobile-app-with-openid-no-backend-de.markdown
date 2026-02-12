---
layout: single
title: "Entwicklung einer Mobile-App mit OpenID-Authentifizierung ohne traditionelles Backend"
date: 2025-02-05
categories: mobile development openid
audience: clients
lang: de
---

## Eine Mobile-App ohne traditionelles Backend erstellen

Nicht jedes Projekt benötigt von Anfang an ein vollständiges Backend. Wenn Geschwindigkeit und Kosteneffizienz wichtig sind – besonders für MVPs oder Proof-of-Concepts – nutze ich verwaltete Dienste für die Authentifizierung und halte die Architektur flexibel für zukünftiges Wachstum.

Dieser Ansatz hat sich für mehrere Kunden bewährt, die ihr Produkt schnell validieren mussten, ohne vorab in Infrastruktur zu investieren.

### Mein Ansatz

Dies erreichte ich durch die Nutzung von Keycloak as a Service für OpenID-Authentifizierung, was eine nahtlose Verwaltung von Benutzeridentität und Zugriff ermöglichte. Hier ist eine detaillierte Aufschlüsselung meines Ansatzes:

1. **Verwendung von Keycloak as a Service**
   - [Keycloak](https://www.keycloak.org/) ist eine Open-Source-Lösung für Identitäts- und Zugriffsverwaltung. Durch die Nutzung [als Service](https://www.cloud-iam.com) konnte ich OpenID-Authentifizierung implementieren, ohne einen eigenen Authentifizierungsserver einrichten zu müssen. Keycloak kümmert sich um die Benutzerauthentifizierung und bietet sofort sicheren token-basierten Zugriff.

2. **Mock-API mit OpenAPI-Spezifikation**
   - Anstatt ein vollwertiges Backend zu entwickeln, schrieb ich eine OpenAPI (Swagger) Spezifikation, um die Endpunkte und deren Antworten für die API meiner Anwendung zu definieren. Diese Spezifikation dient als Vertrag für das, was meine App vom Server erwartet, und verbessert die Zusammenarbeit und Klarheit zwischen Teams.

3. **Verwendung von Stoplight Prism für Mocking**
   - Um eine Serverumgebung zu simulieren, nutzte ich [Stoplight Prism](https://stoplight.io/open-source/prism), das einen Mock-Service basierend auf der von mir erstellten OpenAPI-Spezifikation bereitstellen kann. Prism ermöglicht sowohl statische Mock-Antworten als auch [dynamische Antwortgenerierung](https://github.com/stoplightio/prism/blob/master/docs/guides/01-mocking.md). Diese Echtzeit-Generierung wird durch die Faker-Bibliothek ermöglicht und erlaubt mir, realistische Datenantworten zu erstellen, die dem ähneln, was ein echter Server liefern würde.

### Vorteile dieses Ansatzes

- **Reduzierte Entwicklungszeit**: Durch die Verwendung einsatzbereiter Dienste wie Keycloak und Prism sparte ich Zeit, die sonst für Backend-Setup und -Wartung aufgewendet worden wäre.
  
- **Fokus auf Frontend-Entwicklung**: Dieser Ansatz ermöglichte es mir, mich mehr auf den Aufbau des Frontend der Mobile-Anwendung zu konzentrieren und die Benutzererfahrung und das Interface-Design zu verbessern, ohne mich in Backend-Komplexitäten zu verlieren.

- **Flexibilität und Skalierbarkeit**: Mit einer Mock-API kann ich die API-Spezifikation einfach aktualisieren und die Entwicklung fortsetzen, auch während das eigentliche Backend später entwickelt wird oder wenn verschiedene Backend-Lösungen in Betracht gezogen werden.

## Wann dieser Ansatz sinnvoll ist

Dieses Setup ist perfekt für:
- **MVPs**, die schnell Product-Market-Fit validieren müssen
- **Projekte mit begrenztem Anfangsbudget**, die Backend-Kosten aufschieben möchten
- **Teams, die Frontend und Backend unabhängig entwickeln möchten**
- **Proof-of-Concepts** für Stakeholder-Buy-in vor vollständiger Investition

Ich arbeite Vollzeit für große Unternehmenskunden, übernehme aber ausgewählte Projekte, bei denen ich diese kosteneffizienten Strategien anwenden kann. Wenn Sie eine Mobile-App starten und die Anfangsinvestition minimieren möchten, während Sie Ihre Optionen offen halten, könnte dies der richtige Ansatz sein.

**Haben Sie eine Mobile-App-Idee, sind aber besorgt über Backend-Komplexität?** [Kontaktieren Sie mich](contact.html) für eine kostenlose Beratung. Ich bewerte Ihre Bedürfnisse und gebe Ihnen ein klares Angebot, um Ihre App schnell auf den Markt zu bringen.

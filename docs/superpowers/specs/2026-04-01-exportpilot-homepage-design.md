# ExportPilot — Homepage Design Spec

## Résumé

Page d'accueil unique (single page) pour ExportPilot, offre de conseil export digitalisée ciblant les PME françaises. La page présente les 4 piliers de l'offre et canalise vers l'audit export comme point d'entrée. Design inspiré de chatseo.app/fr — esthétique SaaS moderne, fond blanc, bleu comme couleur primaire, typographie Montserrat.

## Marque

- **Nom** : ExportPilot
- **Positionnement** : "Votre passeur digital vers l'export" — ouvre les portes, le client reste l'acteur commercial
- **Public cible** : dirigeants de PME françaises souhaitant exporter
- **CTA principal** : Demander un audit export

## Charte graphique

### Couleurs

| Rôle | Hex | Usage |
|------|-----|-------|
| Primaire | `#3B82F6` | Boutons, accents, liens, icônes |
| Primaire foncé | `#1E40AF` | Hover boutons, titres accentués |
| Primaire clair | `#DBEAFE` | Fonds de section, badges, pills |
| Bleu très clair | `#EFF6FF` | Dégradés hero, arrière-plans subtils |
| Texte principal | `#111827` | Titres, corps de texte |
| Texte secondaire | `#6B7280` | Sous-titres, descriptions |
| Fond | `#FFFFFF` | Fond principal |
| Fond alterné | `#F8FAFC` | Sections alternées |
| Bordure | `#E5E7EB` | Séparateurs, bordures cartes |

### Typographie

- **Police** : Montserrat (Google Fonts)
- **Titres (h1)** : 800 (ExtraBold), 48-56px
- **Titres (h2)** : 700 (Bold), 36-40px
- **Titres (h3)** : 700 (Bold), 20-24px
- **Corps** : 400 (Regular), 16-18px
- **Petits textes** : 500 (Medium), 14px

### Composants

- **Bouton primaire** : fond `#3B82F6`, texte blanc, border-radius 8px, padding 14px 28px, font-weight 600
- **Bouton secondaire** : fond transparent, bordure 2px `#3B82F6`, texte `#3B82F6`, border-radius 8px
- **Cartes** : fond blanc, border-radius 16px, box-shadow `0 1px 3px rgba(0,0,0,0.08)`, padding 24-32px
- **Sections arrondies** : border-radius 48px sur le conteneur (style ChatSEO)
- **Spacing** : sections séparées de 80-120px, padding interne 60-80px

## Structure de la page (10 sections)

### 1. Header (sticky)

- **Position** : fixe en haut, fond blanc avec légère ombre au scroll
- **Gauche** : logo "ExportPilot" (texte stylisé, pas d'image pour l'instant)
- **Centre-droite** : liens navigation — Offre, Méthode, Blog, Contact
- **Droite** : bouton CTA bleu "Demander un audit"
- **Note** : pas de menu hamburger pour le moment (desktop only en V1)

### 2. Hero

- **Fond** : dégradé `from #EFF6FF via #DBEAFE/20 to white`
- **Layout** : centré, texte au centre
- **Éléments dans l'ordre** :
  1. **Pill/badge** : fond `#DBEAFE`, texte `#1E40AF`, border-radius 999px — "La plateforme export digitalisée"
  2. **Headline h1** : "L'ultime outil pour votre développement **EXPORT**" — le mot EXPORT en couleur `#3B82F6` ou en gras accentué
  3. **Sous-titre** : "ExportPilot combine expertise terrain, data et digital pour ouvrir vos marchés à l'international. Vous restez l'acteur commercial, nous ouvrons les portes." — couleur `#6B7280`, max-width 640px centré
  4. **2 boutons CTA** : "Demander mon audit export" (primaire) + "Découvrir l'offre" (secondaire, outline)
  5. **Social proof** : texte "Accompagnement de PME françaises vers 15+ pays" + rangée de petits drapeaux (FR, MA, SN, CI, DE, AE) en emoji ou mini-icônes
- **Visuel** : carte du monde stylisée en arrière-plan ou en dessous du texte — points de connexion et lignes entre pays (réseau international). Style SVG épuré en `#DBEAFE` / `#3B82F6` avec opacité réduite pour ne pas écraser le texte

### 3. Bandeau chiffres clés

- **Fond** : blanc
- **Layout** : 3 colonnes horizontales, centrées
- **Contenu** :
  - **44 500** — "exportateurs français chaque année"
  - **26%** — "abandonnent en cours de route"
  - **8+ ans** — "d'expérience terrain à l'international"
- **Style** : chiffre en `#3B82F6`, font-weight 800, taille 40-48px. Label en `#6B7280`, 14-16px
- **Séparateurs** : ligne verticale fine `#E5E7EB` entre chaque stat

### 4. Les 4 piliers de l'offre

Section principale de présentation. Layout en alternance gauche/droite comme les features de ChatSEO.

**Titre de section** : "Une offre complète pour chaque étape de votre export"
**Sous-titre** : "De l'audit initial à l'accompagnement terrain, ExportPilot structure votre développement international."

#### 4.1 Audit Export (image gauche, texte droite)
- **Badge** : "Point d'entrée obligatoire"
- **Titre h3** : "Le diagnostic qui change tout"
- **Description** : "Un audit complet de votre potentiel export : marchés cibles, positionnement concurrentiel, capacité opérationnelle. Le socle de toute stratégie réussie."
- **Détail prix** : "À partir de 990€ HT"
- **CTA** : lien "Demander mon audit →"
- **Visuel** : placeholder rectangle arrondi, fond `#EFF6FF` avec icône ou illustration simple (checklist/radar)

#### 4.2 Abonnements mensuels (texte gauche, image droite)
- **Badge** : "Accompagnement continu"
- **Titre h3** : "Un copilote, pas un coup d'éclat"
- **Description** : "Choisissez la formule adaptée à votre ambition. Engagement 6 mois minimum pour des résultats mesurables."
- **3 mini-cartes** empilées ou côte à côte :
  - Starter — 590€/mois
  - Business — 790€/mois (badge "Populaire")
  - Expert — 2 490€/mois
- **CTA** : lien "Comparer les formules →"

#### 4.3 Missions terrain & salons (image gauche, texte droite)
- **Badge** : "Représentation"
- **Titre h3** : "Votre présence là où ça se joue"
- **Description** : "Représentation en salon, prospection terrain, rencontres acheteurs. Des missions ponctuelles, vendues séparément, pour un impact maximal."
- **CTA** : lien "En savoir plus →"
- **Visuel** : placeholder avec icône globe/avion

#### 4.4 Services complémentaires (texte gauche, image droite)
- **Badge** : "À la carte"
- **Titre h3** : "Formation, conformité, recrutement agents"
- **Description** : "Des services one-shot pour renforcer votre capacité export : formation interne, conformité documentaire, aide au financement, recrutement d'agents locaux."
- **CTA** : lien "Découvrir les services →"

**Fond** : sections alternées blanc / `#F8FAFC`. Chaque bloc a un border-radius arrondi (48px) sur le conteneur extérieur comme ChatSEO.

### 5. Pourquoi ExportPilot

- **Fond** : `#F8FAFC` ou dégradé bleu très subtil, conteneur arrondi 48px
- **Titre h2** : "Pas un cabinet de conseil classique. Votre passeur digital vers l'export."
- **3 arguments** (icône + texte) :
  1. Icône graphique → "Des ratios de conversion transparents, pas des promesses de volume"
  2. Icône écran → "Une méthodologie digitalisée, pas des PowerPoint"
  3. Icône poignée de main → "Un passeur terrain, pas un commercial à votre place"
- **CTA** : "Demander mon audit export" (bouton primaire)
- **Mention** : "Sans engagement · Premier échange gratuit"

### 6. Comment ça marche

- **Fond** : blanc
- **Titre h2** : "3 étapes pour lancer votre export"
- **Layout** : 3 colonnes (ou étapes numérotées reliées par une ligne)
- **Étapes** :
  1. **Numéro 1** cercle bleu — "Audit export" — "On analyse votre potentiel, vos marchés et votre capacité opérationnelle."
  2. **Numéro 2** cercle bleu — "Plan d'action" — "Vous recevez une feuille de route claire : marchés cibles, stratégie, outils."
  3. **Numéro 3** cercle bleu — "Accompagnement" — "On vous accompagne avec un abonnement mensuel et des missions terrain ciblées."
- **Ligne de connexion** : trait pointillé ou continu `#DBEAFE` entre les étapes

### 7. Témoignages

- **Fond** : `#F8FAFC`, conteneur arrondi 48px
- **Titre h2** : "Ils ont franchi le pas de l'export"
- **Layout** : carousel ou grille 3 colonnes de cartes
- **Chaque carte** :
  - Photo (avatar rond)
  - Citation entre guillemets
  - Nom, titre, entreprise
- **Note** : en V1, utiliser des témoignages fictifs/placeholder avec mention "Témoignages à venir" ou des cas d'usage génériques si Clément préfère

### 8. FAQ

- **Fond** : blanc
- **Titre h2** : "Toutes les réponses à vos questions"
- **Layout** : accordion (questions dépliables), max-width 720px centré
- **Questions** :
  1. "Combien coûte un audit export ?" → réponse avec les paliers 990-2990€
  2. "Quelle est la durée d'engagement ?" → 6 mois minimum sur les abonnements
  3. "En quoi ExportPilot est différent d'un cabinet de conseil ?" → positionnement digital, transparence, passeur
  4. "Quels marchés couvrez-vous ?" → Afrique, Maghreb, Moyen-Orient, Europe de l'Est + ouverture
  5. "Je n'ai jamais exporté, c'est pour moi ?" → oui, l'audit est conçu pour ça
  6. "Que comprend l'abonnement mensuel ?" → détail selon formule

### 9. CTA final

- **Fond** : dégradé bleu clair (`#EFF6FF` → `#DBEAFE`), conteneur arrondi 48px
- **Titre h2** : "Prêt à ouvrir de nouveaux marchés ?"
- **Sous-titre** : "Commencez par un audit export. Sans engagement, sans surprise."
- **Bouton** : "Demander mon audit export" (bouton primaire, taille large)
- **Mention** : "Premier échange gratuit · Réponse sous 48h"

### 10. Footer

- **Fond** : `#111827` (dark) ou blanc selon cohérence
- **Layout** : 3-4 colonnes
- **Colonne 1** : logo ExportPilot + tagline "Votre passeur digital vers l'export"
- **Colonne 2** : liens — Offre, Méthode, Blog, Contact
- **Colonne 3** : liens légaux — Mentions légales, CGV, Politique de confidentialité
- **Colonne 4** : réseaux sociaux (LinkedIn icône)
- **Bas** : © 2026 ExportPilot. Tous droits réservés.

## Spécifications techniques

- **Stack** : HTML + CSS + JS vanilla (single file `index.html` ou fichiers séparés)
- **Responsive** : desktop-first, mais pensé pour mobile (pas de menu hamburger en V1)
- **Fonts** : Google Fonts — Montserrat 400, 500, 600, 700, 800
- **Icônes** : Lucide Icons (CDN) ou SVG inline
- **Animations** : fade-in au scroll (CSS `@keyframes` + `IntersectionObserver`), hover sur boutons et cartes
- **Pas de framework** : HTML/CSS/JS pur pour compatibilité Hostinger Horizons
- **Images** : placeholders en V1, remplacés plus tard par de vrais visuels

## Hors scope (V1)

- Menu navigation mobile (hamburger)
- Blog
- Page tarifs détaillée
- Formulaire d'audit fonctionnel (lien vers calendly ou email en V1)
- Multilingue
- Analytics / tracking

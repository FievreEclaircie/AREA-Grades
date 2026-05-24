# INSIGNUM
### Suite de gestion des insignes militaires

> Collecte, nomme, trie et convertit les insignes de grades militaires OTAN et non-OTAN depuis Wikipedia.

🌐 **[Ouvrir INSIGNUM](https://fievreeclaircie.github.io/rename/)**

---

## Les outils

### 🎖️ [Collecte](https://fievreeclaircie.github.io/rename/nato-renamer.html)
Scrape les pages Wikipedia de grades militaires et télécharge les insignes en les nommant selon la nomenclature standardisée.

- Pages **OTAN** : détection automatique des codes OF/OR depuis les tableaux Wikipedia
- Pages **non-OTAN** : analyse par Claude (IA) pour assigner les équivalents OF/OR
- Nomenclature : `PAYS_BRANCHE_GRADE_NomDuGrade.svg`
- Téléchargement en ZIP

### 📁 [Tri](https://fievreeclaircie.github.io/rename/thot-sorter.html)
Lit les noms de fichiers et déplace automatiquement chaque insigne dans l'arborescence correcte.

- Détecte les dossiers existants et les réutilise
- Crée les dossiers manquants (noms en majuscules sans accents)
- Sépare automatiquement **OTAN** et **NON-OTAN** selon la liste des 32 membres
- Gère les corps spéciaux (ex : IRGC iranien)
- Les fichiers non reconnus restent dans "A trier"
- **Chrome/Edge uniquement** (écriture directe sur disque)

### 🖼️ [Conversion](https://fievreeclaircie.github.io/rename/thot-rename-ext.html)
Convertit les fichiers SVG en vrais PNG (pixels) directement dans le dossier source.

- Conversion réelle via Canvas (pas un simple renommage)
- Largeur configurable, hauteur proportionnelle automatique
- Écriture directe sur disque (Chrome/Edge) ou téléchargement individuel (Firefox)

---

## Workflow

```
1. COLLECTE          2. EXTRAIRE           3. TRI               4. CONVERSION
nato-renamer.html → ZIP extrait localement → thot-sorter.html → thot-rename-ext.html
Wikipedia/Claude     Dossier "A trier"       GRADE/OTAN/PAYS/    SVG → PNG sur disque
```

---

## Structure des dossiers

```
GRADE/
├── A TRIER/                    ← dossier de dépôt des ZIP extraits
├── OTAN/
│   ├── FRANCE/
│   │   ├── AIR/
│   │   ├── TERRE/
│   │   └── MER/
│   ├── ALLEMAGNE/
│   └── ...  (32 pays)
└── NON-OTAN/
    ├── IRAN/
    │   ├── AIR/
    │   ├── TERRE/
    │   └── AIR/IRGC/           ← corps spéciaux
    ├── RUSSIE/
    └── ...
```

---

## Nomenclature des fichiers

| Format | Exemple |
|--------|---------|
| `PAYS_BRANCHE_GRADE_Nom.svg` | `FRA_AIR_OF6_General-de-Brigade.svg` |
| `PAYS_BRANCHE_CORPS_GRADE_Nom.svg` | `IRN_AIR_IRGC_OF8_Brigadier-General.svg` |

**Codes pays** : trigrammes ISO 3166-1 alpha-3  
**Branches** : `AIR` · `TERRE` · `MER` (les forces spatiales sont classées `AIR`)  
**Grades OTAN** : `OF1`–`OF10` · `OR1`–`OR9` · `OFD` (cadet/aspirant)

---

## Pays OTAN reconnus

| Trigramme | Pays | Trigramme | Pays |
|-----------|------|-----------|------|
| ALB | Albanie | MKD | Macédoine du Nord |
| DEU | Allemagne | MNE | Monténégro |
| BEL | Belgique | NOR | Norvège |
| BGR | Bulgarie | NLD | Pays-Bas |
| CAN | Canada | POL | Pologne |
| HRV | Croatie | PRT | Portugal |
| DNK | Danemark | CZE | République tchèque |
| ESP | Espagne | ROU | Roumanie |
| EST | Estonie | GBR | Royaume-Uni |
| USA | États-Unis | SVK | Slovaquie |
| FIN | Finlande | SVN | Slovénie |
| FRA | France | SWE | Suède |
| GRC | Grèce | TUR | Turquie |
| HUN | Hongrie | ISL | Islande |
| ITA | Italie | LUX | Luxembourg |
| LVA | Lettonie | LTU | Lituanie |

---

## Compatibilité navigateurs

| Fonctionnalité | Chrome/Edge | Firefox |
|----------------|-------------|---------|
| Collecte | ✅ | ✅ |
| Tri (écriture directe) | ✅ | ❌ |
| Conversion (écriture directe) | ✅ | ⚠️ téléchargements individuels |

> Le tri et la conversion nécessitent l'API **File System Access** disponible uniquement dans Chrome et Edge.

---

## Infrastructure

- **Worker Cloudflare** : `https://massive-rename.fievre-eclaircie.workers.dev`
  - `/scrape-wiki` — scraping Wikipedia (modes OTAN et non-OTAN)
  - `/proxy-image` — proxy pour télécharger les images Wikimedia
  - `/claude` — proxy vers l'API Anthropic Claude
- **Variable d'environnement** : `CLAUDE_API_KEY` (clé API Anthropic)
- **Plan Cloudflare** : Workers payant ($5/mois)

---

*INSIGNUM — Gestion des insignes militaires*

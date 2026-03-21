# BINGO HOTEL MEXIQUE — Meliá Hotels International

## Workflow

Utiliser le skill `/workflow` pour toute tache de dev sur ce projet :
- Plan first, subagents, self-improvement, verification, elegance
- Chaque phase doit etre validee avant de passer a la suivante

---

## 1. CONTEXTE PROJET

| Champ | Valeur |
|---|---|
| Client | **Meliá Hotels International** — Mexique |
| Usage | Animation de groupe pour les clients de l'hotel |
| Public | Touristes internationaux, toutes tranches d'age |
| Langue | **Espagnol uniquement** |
| Livraison | **Fichier HTML unique** — double-clic et ca tourne |
| Compatibilite | Windows + Mac (HTML natif, pas d'installation) |
| Internet requis | **Non** — fonctionne 100% offline |

---

## 2. TYPE DE BINGO

- **Format** : Bingo 75 boules (style americain)
- **Numeros** : 1 a 75
- **Colonnes** : B (1-15) / I (16-30) / N (31-45) / G (46-60) / O (61-75)
- **Cartons** : Physiques, deja imprimes par le client — le jeu ne gere PAS les cartons
- **Validation gagnant** : Le staff verifie physiquement le carton du joueur

---

## 3. FONCTIONNEMENT DU JEU

### Tirage
- **Mode** : Automatique — les numeros tombent seuls
- **Intervalle** : Configurable (defaut : **8 secondes** entre chaque tirage)
- **Ordre** : Aleatoire, sans repetition
- **Fin de partie** : Quand tous les 75 numeros ont ete tires OU quand un gagnant est declare

### Controles staff (boutons visibles a l'ecran)

| Bouton | Action |
|---|---|
| INICIAR | Lance la partie / reprend si en pause |
| PAUSAR | Met le tirage en pause |
| NUEVO JUEGO | Remet tout a zero, retour a l'ecran de demarrage |
| Son | Active / coupe le son |

### Etats du jeu
1. **Pantalla de inicio** — Ecran d'accueil avec le nom du jeu et bouton Iniciar
2. **En juego** — Tirage automatique en cours
3. **En pausa** — Tirage suspendu
4. **BINGO!** — Bouton gagnant presse, animation de victoire
5. **Fin de partida** — Tous les numeros tires

---

## 4. INTERFACE — LAYOUT GRAND ECRAN

```
+-----------------------------------------------------+
|  [LOGO HOTEL]           B I N G O        [SON] [?]  |
|                                                      |
|         +----------------------------+               |
|         |                            |               |
|         |   NUMERO ACTUAL :  42      |               |  <- TRES GRAND
|         |         N - 42             |               |
|         |                            |               |
|         +----------------------------+               |
|                                                      |
|   +------------------------------------------+       |
|   |  NUMEROS ANTERIORES                       |       |
|   |  5  12  33  67  21  44  8  59  ...        |       |  <- grille des deja tires
|   +------------------------------------------+       |
|                                                      |
|      [ PAUSAR ]              [ NUEVO JUEGO ]         |
+-----------------------------------------------------+
```

### Zones cles
- **Numero actuel** : Occupe 40% de l'ecran, lisible a 10 metres
- **Lettre BINGO** : Affichee sous le numero (ex: "N - 42")
- **Historique** : Grille compacte des numeros deja sortis, colores par colonne
- **Compteur** : "Numeros cantados: 12 / 75"

---

## 5. DESIGN VISUEL

### Direction artistique : "Luxury Fiesta"
Melia est une marque **sobre et luxueuse**. Le bingo est **festif et colore**. On marie les deux :
- Le logo Melia trone en haut, discret et elegant
- Le fond est sombre et premium
- Les couleurs festives explosent sur le fond sombre — vivantes mais jamais vulgaires
- L'or remplace le jaune criard comme accent principal

### Palette de couleurs

| Role | Couleur |
|---|---|
| Fond principal | Noir luxe `#0D0D0D` |
| Accent Melia | Gris argent `#9E9E9E` |
| Numero principal | Or chaud `#D4AF37` |
| Accent secondaire | Rouge grenat `#C0392B` |
| Colonne B | Bleu saphir `#2E86DE` |
| Colonne I | Emeraude `#00B894` |
| Colonne N | Or `#D4AF37` |
| Colonne G | Corail `#E17055` |
| Colonne O | Violet `#A855F7` |
| Texte principal | Blanc casse `#F5F5F0` |

### Typographie

| Usage | Font |
|---|---|
| Numero principal | **Bebas Neue** ou **Black Ops One** |
| Titres / BINGO | **Fredoka One** |
| Interface | **Nunito** |

### Animations obligatoires
- Numero actuel : entree avec rebond / zoom depuis le centre
- Boule animee qui "tombe" avant d'afficher le numero
- Numeros historique : apparition progressive avec color-coding
- Fond : particules legeres ou confettis subtils en continu
- Ecran BINGO! : explosion de confettis, clignotement or
- Boutons : hover glow + micro-animation au clic
- Barre de progression : compte a rebours visuel avant le prochain tirage

---

## 6. SON

- **Son au tirage** : effet "boule qui roule" + bip festif
- **Son de victoire** : fanfare courte quand BINGO! est declenche
- **Musique de fond** : Optionnel (a confirmer)
- **Controle** : Bouton mute/unmute toujours visible
- **Format** : Sons generes via **Web Audio API** (pas de fichiers externes) ou base64 embarques

---

## 7. LIVRABLE

```
bingo-hotel.html          <- fichier unique, tout embarque dedans
```
- HTML + CSS + JS dans un seul fichier
- Fonts chargees en base64 ou via CDN avec fallback offline
- Sons embarques en base64
- Aucune dependance externe requise au runtime

---

## 8. CONTRAINTES TECHNIQUES

- **Pas de serveur** — tout tourne dans le navigateur
- **Pas d'internet requis** au moment du jeu
- **Teste sur** : Chrome, Edge (Windows) + Safari, Chrome (Mac)
- **Resolution cible** : 1920x1080 minimum (TV/projecteur)
- **Responsive** : Non prioritaire — optimise grand ecran horizontal

---

## 9. PHASES DE DEV

| Phase | Contenu | Priorite |
|---|---|---|
| 1 | Structure HTML + timer + tirage aleatoire 75 boules | CORE |
| 2 | Affichage grand ecran + historique colore | CORE |
| 3 | Boutons Iniciar / Pausar / Nuevo Juego | CORE |
| 4 | Design festif + animations + fonts | IMPORTANT |
| 5 | Sons Web Audio API | BONUS |
| 6 | Ecran d'accueil + ecran victoire | BONUS |
| 7 | Logo hotel + personnalisation couleurs | PERSO |

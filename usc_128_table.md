Universal Symbolic Core — Table étendue USC‑128 (v0.1)
=====================================================

Portée
------

- **USC‑128** : noyau recommandé, extension directe de **USC‑96**.
- **Objectif** : ajouter **32 symboles** (`ID 96..127`) sans toucher aux IDs `0..95` déjà gelés par USC‑96.
- Domaines ajoutés (conformément au livre) :
  - **Mathématiques étendues** (constantes, fonctions, structures),
  - **Concepts scientifiques élémentaires** (physique simple, énergie, signal),
  - **Relations logiques enrichies** (implication, équivalence, nécessité…),
  - quelques **unités physiques** minimales.

Invariants
----------

- **IDs 0–95** : identiques à `usc_96_table.md` (USC‑96).
- **IDs 96–127** : ajoutés par USC‑128, mais **USC‑96 reste un sous‑ensemble stable**.
- Encodage binaire :
  - En mode **strict USC‑96**, on n’utilise que `0..95`.
  - En mode **USC‑128**, on autorise `0..127` (7 bits pleins).

Table USC‑128 — nouveaux symboles (96–127)
------------------------------------------

### Bloc 96–111 : Math étendues (MATH‑*)

| ID  | SYMBOL        | CLASS | GLOSS                                                   |
|-----|---------------|-------|---------------------------------------------------------|
| 96  | MATH-PI       | MATH  | constante π (pi)                                       |
| 97  | MATH-E        | MATH  | constante e (base du logarithme naturel)               |
| 98  | MATH-INF      | MATH  | infini (∞, conceptuel)                                 |
| 99  | MATH-LIM      | MATH  | limite (lim)                                           |
| 100 | MATH-DERIV    | MATH  | dérivée / taux de variation                            |
| 101 | MATH-INTEG    | MATH  | intégrale                                              |
| 102 | MATH-VECTOR   | MATH  | vecteur                                                |
| 103 | MATH-MATRIX   | MATH  | matrice                                                |
| 104 | MATH-NORM     | MATH  | norme / magnitude                                      |
| 105 | MATH-SET      | MATH  | ensemble mathématique (théorie des ensembles)         |
| 106 | MATH-FUNC     | MATH  | fonction mathématique (application)                   |
| 107 | MATH-REL      | MATH  | relation mathématique                                 |
| 108 | MATH-PROB     | MATH  | probabilité (objet mathématique, distribution)        |
| 109 | MATH-EXPECT   | MATH  | espérance mathématique (valeur attendue)              |
| 110 | MATH-VAR      | MATH  | variance / dispersion                                 |
| 111 | MATH-STD      | MATH  | écart‑type                                             |

### Bloc 112–119 : Logique avancée (LOG‑*)

| ID  | SYMBOL       | CLASS | GLOSS                                                    |
|-----|--------------|-------|----------------------------------------------------------|
| 112 | LOG-IMPLIES  | LOG   | implication (⇒)                                          |
| 113 | LOG-IFF      | LOG   | équivalence logique (si et seulement si, ⇔)             |
| 114 | LOG-NEC      | LOG   | nécessité (modalité □)                                  |
| 115 | LOG-POSS     | LOG   | possibilité (modalité ◇)                                |
| 116 | LOG-TRUE     | LOG   | vrai (valeur de vérité)                                 |
| 117 | LOG-FALSE    | LOG   | faux (valeur de vérité)                                 |
| 118 | LOG-TAUTO    | LOG   | tautologie (toujours vrai)                              |
| 119 | LOG-CONTRA   | LOG   | contradiction (impossible)                              |

### Bloc 120–127 : Concepts scientifiques elementaires (SCI‑*, UNIT‑*)

| ID  | SYMBOL        | CLASS | GLOSS                                                     |
|-----|---------------|-------|-----------------------------------------------------------|
| 120 | SCI-MASS      | SCI   | masse (concept physique élémentaire)                      |
| 121 | SCI-FORCE     | SCI   | force                                                     |
| 122 | SCI-ENERGY    | SCI   | énergie                                                   |
| 123 | SCI-POWER     | SCI   | puissance (énergie / temps)                              |
| 124 | SCI-FIELD     | SCI   | champ (ex. champ électrique, gravitationnel)             |
| 125 | SCI-WAVE      | SCI   | onde (propagation périodique)                            |
| 126 | UNIT-MASS     | UNIT  | unité abstraite de masse (ex. kilogramme canonique)      |
| 127 | UNIT-ENERGY   | UNIT  | unité abstraite d’énergie (ex. joule canonique)          |

Encodage USC‑128
----------------

- **ID** : entier dans \[0, 127\].
- **CODE7** : représentation binaire sur 7 bits (0–127).
- En pratique :
  - **USC‑96** n’utilise que `0..95`.
  - **USC‑128** utilise `0..127`.
- Le schéma de trame (version, checksum, etc.) reste au niveau **protocole externe** et ne modifie pas cette numérotation.

Exemple USC‑128
---------------

Intention (informelle) :  
> “Un capteur humain estime la variance d’une mesure de masse.”

Séquence de symboles :

1. `ENT-HUMAN` (86)
2. `ENT-MACHINE` (87) + `REL-PART-OF` (17) pour marquer un dispositif porté
3. `ENT-ACTION` (93)
4. `OP-MEAS` (34)
5. `SCI-MASS` (120)
6. `MATH-VAR` (110)

Séquence d’IDs :  
`[86, 87, 17, 93, 34, 120, 110]`

En JSON compact :

```json
{
  "usc_version": "128-v0.1",
  "symbols": [86, 87, 17, 93, 34, 120, 110]
}
```

Compatibilité
-------------

- Tout décodeur USC‑128 doit :
  - interpréter correctement **USC‑96** (0–95),
  - comprendre qu’un symbole `≥96` indique l’usage d’USC‑128.
- Un flux strictement limité à `0..95` reste **100 % compatible USC‑96**.



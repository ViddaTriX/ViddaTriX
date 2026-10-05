# Pose Sténopé

Calculateur de temps de pose pour appareil photo sténopé, en une seule page HTML sans dépendance.
Ouvrez `index.html` dans un navigateur (ordinateur ou téléphone).

## Fonctions

- **Sténopé** : diamètre du trou et focale → ouverture (f/N), avec le diamètre optimal (critère de Rayleigh).
- **Lumière**, trois façons de la renseigner :
  - *Scène* : situations types (plein soleil IL 15, couvert IL 12, intérieur…) ;
  - *Posemètre* : ouverture et vitesse lues sur un posemètre ou une appli de téléphone ;
  - *IL manuel* : indice de lumination à ISO 100.
- **Compensation** en IL (contre-jour, filtre…).
- **Film** : sensibilité et correction de l'effet Schwarzschild (défaut de réciprocité)
  - Ilford / Kentmere : formule `t corrigé = t^p` ;
  - Kodak Tri-X, T-Max, Fomapan 100 : tableaux du fabricant, interpolés en échelle log ;
  - papier photo, numérique (sans correction), ou exposant `p` personnalisé.
- **Minuteur** avec bips sur les 5 dernières secondes, signal de fin, vibration et maintien de l'écran allumé.
- **Tableau** des poses pour toutes les situations types avec le réglage courant.

Les réglages sont mémorisés dans le navigateur.

## Formules

- `N = focale / diamètre`
- `t = N² / 2^(IL100 + log2(ISO/100) − compensation)`
- diamètre optimal : `d = 1,9 × √(focale × 0,00055 mm)`

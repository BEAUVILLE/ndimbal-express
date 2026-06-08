# NDIMBAL Express — DIGIYLYFE

NDIMBAL Express est la porte DIGIYLYFE dédiée aux **missions courtes, urgentes ou ponctuelles**.

Le principe est simple :

- le public voit les missions validées ;
- la personne qui veut publier passe par un PIN ;
- le formulaire de dépôt reste séparé de l’admin ;
- l’admin DIGIY valide avant affichage public ;
- DIGIYLYFE ne prend pas de commission.

---

## Doctrine

```txt
PUBLIC = voir les missions validées
PIN = serrure d’entrée
INDEX = formulaire de dépôt mission
ADMIN = validation DIGIY séparée
```

Le circuit propre est :

```txt
public.html
→ mur public NDIMBAL Express

pin.html
→ vérifie le PIN
→ redirige vers index.html

index.html
→ formulaire de dépôt mission courte

admin-ndimbal-express.html
→ contrôle, validation ou refus côté DIGIY
```

Aucune porte publique ne doit ouvrir l’admin par défaut.

---

## Pages principales

### `public.html`

Page publique NDIMBAL Express.

Rôle :

- afficher les missions validées ;
- permettre la recherche ;
- filtrer par zone ;
- ouvrir WhatsApp ou SMS ;
- rappeler le 0% commission ;
- envoyer vers le dépôt via le PIN.

Lien de publication depuis la page publique :

```txt
./pin.html?redirect=./index.html
```

---

### `pin.html`

Serrure NDIMBAL Express.

Rôle :

- demander téléphone + PIN ;
- vérifier l’accès avec Supabase ;
- ouvrir uniquement `index.html`.

Destination correcte :

```js
const DEFAULT_REDIRECT = "./index.html";
```

Le PIN ne doit pas diriger vers :

```txt
admin-ndimbal-express.html
```

---

### `index.html`

Formulaire de dépôt mission courte.

Rôle :

- titre de mission ;
- zone / localisation ;
- téléphone WhatsApp ;
- urgence / moment ;
- détails supplémentaires ;
- prévisualisation ;
- sauvegarde automatique ;
- publication en attente.

`index.html` est le module de dépôt.  
Il ne doit pas être remplacé par une page admin ou un espace PRO général.

---

### `admin-ndimbal-express.html`

Page de contrôle DIGIY.

Rôle :

- voir les missions / tickets en attente ;
- vérifier les paiements ou preuves si nécessaire ;
- valider ;
- refuser ;
- préparer l’affichage public.

Cette page est séparée du circuit public et du circuit PIN utilisateur.

---

## Statuts des missions

La page publique doit afficher uniquement les missions validées.

Statuts compatibles côté public :

```txt
approved
published
validated
public
valide
validé
active
online
```

Si l’admin utilise un autre statut, ajuster le filtre dans `public.html`.

---

## Supabase

Table utilisée par défaut :

```txt
jef_missions
```

Champs lus par la page publique :

```txt
title
zone
phone
when_text
details
status
created_at
id / ref
```

La page publique filtre les lignes validées avant affichage.

---

## Règle de sécurité

Ne jamais exposer côté public :

```txt
PIN
owner_id
notes internes sensibles
liens admin
téléphones cachés non destinés au contact
données de contrôle DIGIY
```

La page publique montre seulement ce qui sert au contact direct pour la mission validée.

---

## Liens recommandés

### Public

```txt
https://ndimbal-annonces-pro.digiylyfe.com/public.html
```

### Dépôt mission

```txt
https://ndimbal-annonces-pro.digiylyfe.com/pin.html?redirect=./index.html
```

### Admin DIGIY

```txt
https://ndimbal-annonces-pro.digiylyfe.com/admin-ndimbal-express.html
```

L’admin ne doit pas être utilisé comme lien d’entrée public.

---

## Test après push

Après modification, tester avec cache-busting :

```txt
https://ndimbal-annonces-pro.digiylyfe.com/public.html?v=public-ok
https://ndimbal-annonces-pro.digiylyfe.com/pin.html?v=pin-index-ok
https://ndimbal-annonces-pro.digiylyfe.com/index.html?v=index-ok
```

Résultat attendu :

```txt
public.html affiche les missions validées
pin.html ouvre index.html après validation
index.html dépose une mission
admin reste séparé
```

---

## Phrase doctrine

```txt
NDIMBAL Express relie besoin court, mission urgente et contact direct.
DIGIYLYFE organise la porte, protège le dépôt, laisse le terrain garder la main.
0% commission.
```

---

## État du circuit validé

```txt
NDIMBAL Express PUBLIC
→ public.html

NDIMBAL Express DÉPÔT
→ pin.html
→ index.html

NDIMBAL Express ADMIN
→ admin-ndimbal-express.html
```

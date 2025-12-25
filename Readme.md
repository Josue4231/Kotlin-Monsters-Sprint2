# 🐉 Kotlin Monsters - Sprint 2

## 🎮 Aperçu du projet

*Kotlin Monsters* est un jeu textuel développé en **Kotlin**, inspiré de Pokémon.  
Le joueur incarne un dresseur et interagit avec un monde peuplé de monstres, villes et arènes.  
Ce projet permet de pratiquer la **POO**, la **modularité** et la **logique métier**.

---

## 🔗 Versions du projet

- Sprint 1 : [Lien vers Sprint 1](https://github.com/Josue4231/kotlin-Monsters)  
- Sprint 2 : version détaillée ci-dessous  
- Sprint 3 : [Lien vers Sprint 3](https://github.com/Josue4231/Kotlin-Monsters-Sprint3)  

---

## 🏃‍♂️ Sprint 2 – Nouvelles fonctionnalités

### 🌱 Système d’évolution

#### Classe `PalierEvolution`
- Définit un palier d’évolution pour un monstre (niveau requis, espèce cible).  
- Méthode `peutEvoluer(individu: IndividuMonstre)` retourne `true` si le monstre peut évoluer.

```kotlin
class PalierEvolution (
    val id: Int,                  
    val niveauRequis: Int,         
    val evolution: EspeceMonstre   
) {
    fun peutEvoluer(individu: IndividuMonstre): Boolean {
        return individu.niveau >= niveauRequis
    }
}
```
---

## Méthodes levelUp() et evoluer()

levelUp() : incrémente le niveau et déclenche l’évolution si les conditions sont remplies.

evoluer() : change l’espèce du monstre et informe le joueur.
```kotlin
fun evoluer() {
    especeMonstre = palierEvolution?.evolution ?: especeMonstre
    println("Le monstre évolue en ${especeMonstre.nom} !")
}

fun levelUp() {
    niveau++
    if (especeMonstre.palierEvolution?.peutEvoluer(this) == true) {
        evoluer()
    }
}
```

## Nouvelle espèce : Pyrokip

Évolution de Flamkip au niveau 7.
Statistiques améliorées et lore détaillé.
ASCII Art pour front et back inclus.
Palier d’évolution créé pour associer Flamkip à Pyrokip.

--- 

## 🏙️ Ville
Création de la classe Ville et modification de Zone

Ville hérite de Zone et ajoute :
arene : instance d’une arène
lignesMagasin : articles disponibles
```kotlin
class Ville(id: Int, nom: String, expZone: Int, especesMonstres: MutableList<EspeceMonstre> = mutableListOf()) : Zone(id, nom, expZone, especesMonstres) {
    lateinit var arene: Arene
    var lignesMagasin: MutableList<LigneMagasin> = mutableListOf()
}
```
  ## Connexion des zones
```kotlin
route2.zoneSuivante = racailleCity
racailleCity.zonePrecedente = route2
```

  ## Méthodes soignerEquipe() et choisirMonstre()

soignerEquipe() : restaure les PV de tous les monstres

choisirMonstre() : permet de sélectionner un monstre pour le combat

---

## ⚔️ CombatDresseur

Méthodes implémentées :
avoirGagne()
avoirPerdu()
lancerCombat()
---

## 🧪 Tests unitaires

Classe IndividuMonstreTest : vérifie le passage au niveau supérieur et l’évolution correcte de Flamkip → Pyrokip.
```kotlin
@Test
fun levelUp() {
    var monstre1 = IndividuMonstre(id=2, nom="flamkip", experience=1500.0, especeMonstre=especeFlamkip, entraineur=null)
    monstre1.levelUp() // Niveau 6
    monstre1.levelUp() // Niveau 7 → évolue en Pyrokip
    assertEquals(especePyrokip, monstre1.especeMonstre)
}
```
---

## 📁 Structure du projet


- `/src/org/example/monstre` : contient les classes principales du jeu et la logique d’évolution.  
- `/ressources/art/pyrokip` : fichiers ASCII art pour représenter les monstres.  
- `/test` : tests unitaires pour valider l’évolution des monstres et le comportement du jeu.

---

## 🏗️ Sprint 2 – Évolution & Villes

### 🌱 Évolution des monstres
- Classe `PalierEvolution` pour gérer les conditions d’évolution.
- Méthodes `levelUp()` et `evoluer()` dans `IndividuMonstre` pour la progression automatique.
- Création d’une nouvelle espèce : **Pyrokip**, évolution de Flamkip.

### 🏙️ Villes et exploration
- Création de la classe `Ville` héritant de `Zone`.
- Gestion des déplacements entre zones.
- Ajout de méthodes dans `Entraîneur` : `soignerEquipe()` et `choisirMonstre()`.

### ⚔️ Combats
- Introduction des **arènes**.
- Méthodes `avoirGagne()`, `avoirPerdu()` et `lancerCombat()` pour gérer les combats contre les dresseurs.

---

## 🧩 Compétences mises en œuvre
- Programmation orientée objet en **Kotlin**.
- Gestion de la progression et évolution des entités.
- Conception de classes modulaires et héritage.
- Tests unitaires pour vérifier le comportement du jeu.
- Manipulation de fichiers ASCII pour représenter les monstres.
- Gestion de l’interaction utilisateur avec menus et saisies console.

---

## 📌 Objectif
Créer un **jeu textuel évolutif**, illustrant des concepts OOP et une progression logique, tout en offrant une expérience ludique et immersive pour l’utilisateur.

---


  ---

## 🧩 Compétences mises en œuvre

Kotlin & Android Studio
POO (héritage, composition, polymorphisme)
Gestion de collections et logique métier
Tests unitaires avec Kotlin
Organisation de projet en sprints

## 🎯 Objectifs du Sprint 2

Implémenter l’évolution des monstres
Créer des villes et gérer la navigation entre zones
Ajouter un système de combat avec arènes
Préparer l’application pour le Sprint 3 : fonctionnalités avancées et UI améliorée

---

# 🐉 Kotlin Monsters

## 🎮 Introduction

*Kotlin Monsters* est un projet de jeu textuel développé en **Kotlin**, inspiré des mécaniques classiques des jeux de type **Pokémon**. Le joueur incarne un dresseur de monstres qui explore un monde peuplé de créatures, traverse des **villes**, affronte des **dresseurs dans des arènes**, et fait **évoluer ses monstres** en les entraînant.

Ce projet a été réalisé dans le cadre d’un **sprint de développement**, avec pour objectif de mettre en œuvre des concepts de **programmation orientée objet**, de **modularité** et de **logique métier**, tout en créant une expérience de jeu immersive et évolutive.

Ce `README` présente les différentes fonctionnalités implémentées lors du **Sprint 2**, notamment :

- 🌱 Le système d’**évolution des monstres**
- 🏙️ L’ajout de **villes** dans l’univers du jeu
- ⚔️ L’introduction des **arènes** et des combats contre dresseurs

---

## 📑 Sommaire

### 2) 🌱 Évolution

- A) [La classe `PalierEvolution`](#a-la-classe-palierEvolution)
- B) [Modification de la classe `IndividuMonstre`](#b-modification-de-la-classe-individumonstre)
- C) [Création d’une nouvelle espèce](#c-création-dune-nouvelle-espèce)

### 3) 🏙️ Ville

- A) [Création de la classe `Ville` et modification de la classe `Zone`](#a-création-de-la-classe-ville-et-modification-de-la-classe-zone)
- B) [Ajout des méthodes `soignerEquipe()` et `choisirMonstre()` dans la classe `Entraîneur`](#b-ajout-des-méthodes-soignerequipe-et-choisirmonstre-dans-la-classe-entraineur)
- C) [Modification de la méthode `jouer()` de la classe `Partie`](#c-modification-de-la-méthode-jouer-de-la-classe-partie)

### 4) ⚔️ CombatDresseur

- A) [Méthode `avoirGagne()`](#a-méthode-avoirgagne)
- B) [Méthode `avoirPerdu()`](#b-méthode-avoirperdu)
- C) [Méthode `lancerCombat()`](#c-méthode-lancercombat)

### 2) 🌱 Évolution

### A) La classe `PalierEvolution`

<!-- Présentation générale -->
La classe `PalierEvolution`, située dans le package `org.example.monstre`, représente un palier d’évolution possible pour un monstre.  
Elle définit les conditions nécessaires à l’évolution d’un individu en spécifiant :

- Un **identifiant unique** (`id`) permettant d’identifier le palier,
- Le **niveau requis** (`niveauRequis`) que doit atteindre l’individu pour pouvoir évoluer,
- L’**espèce cible** (`evolution`) vers laquelle l’individu peut évoluer.

<!-- Explication de la méthode -->
La méthode `peutEvoluer()` prend en paramètre un objet de type `IndividuMonstre` et retourne un booléen indiquant si l’individu a atteint ou dépassé le niveau requis pour évoluer.  
Si la condition est remplie, la méthode retourne `true`, sinon `false`.
<!-- Le code -->
```kotlin
package org.example.monstre

class PalierEvolution (
    val id: Int,                  
    val niveauRequis: Int,         
    val evolution: EspeceMonstre   
) {
    
    fun peutEvoluer(individu: IndividuMonstre): Boolean {
        
        if (individu.niveau >= niveauRequis) {
            return true
        } else {
            
            return false
        }
    }
}
```
<!-- Résumé de l’utilité -->
Cette classe permet ainsi d’intégrer facilement la logique d’évolution dans le système des monstres, en vérifiant les conditions d’évolution avant d’effectuer une transformation vers une nouvelle espèce.


### B) Modification de la classe `IndividuMonstre`

#### Diagramme d’activité

![Diagramme d'activité : Vérification d'évolution dans levelUp()](/imgs%20sprint2/diagramme_levelup.png)

Ce diagramme illustre le processus de vérification d’évolution lors du passage au niveau supérieur (`levelUp()`).

---

#### Méthode `evoluer()`
<!-- Explication de la méthode -->
La méthode `evoluer()` ne prend pas de paramètre et ne retourne rien.  
Son rôle est de remplacer l’espèce actuelle du monstre par son évolution définie dans le palier d’évolution, puis d’afficher un message pour informer que le monstre évolue.

<!--Le code-->
```kotlin
fun evoluer() {
    especeMonstre = palierEvolution?.evolution ?: especeMonstre
    println("Le monstre évolue en ${especeMonstre.nom} !")
}
```

### Méthode `levelup()`
<!-- Explication de la méthode -->
La méthode `levelup()` gère la montée de niveau du monstre.
Elle incrémente le niveau, puis vérifie si un palier d’évolution est défini et si les conditions d’évolution sont remplies.
Si c’est le cas, elle appelle evoluer() pour transformer le monstre.

<!--Le code-->
```kotlin
fun levelUp() {
    niveau++ // Incrémente le niveau du monstre de 1

    
    if (especeMonstre.palierEvolution != null) {
        
        if (especeMonstre.palierEvolution!!.peutEvoluer(this)) {
            evoluer() // Appelle la méthode pour faire évoluer le monstre
        } else {
            
        }
    } else {
        
        println("Pas de palier d'évolution défini")
    }
}
```


<!-- Résumé de l’utilité -->

Les méthodes `levelUp()` et `evoluer()` jouent un rôle clé dans la gestion de la progression des monstres.

- La méthode `levelUp()` permet d’augmenter le niveau de l’individu, ce qui reflète son entraînement et sa croissance.
- Après l’incrément du niveau, `levelUp()` vérifie si le monstre peut évoluer en fonction des conditions définies dans le palier d’évolution associé à son espèce.
- Si ces conditions sont remplies, la méthode `evoluer()` est appelée pour transformer l’espèce du monstre en une forme évoluée, améliorant ainsi ses capacités.
- La méthode `evoluer()` met à jour l’espèce du monstre et informe le joueur de cette évolution par un message.

Ensemble, ces deux méthodes garantissent une évolution cohérente et automatique des monstres, enrichissant la dynamique du jeu et motivant le joueur à faire progresser ses créatures.

### C) Création d’une nouvelle espèce : Pyrokip



<!-- Présentation générale -->
Cette section présente la création d'une nouvelle espèce de monstre nommée **Pyrokip**, évolution de **Flamkip**.  
Cette espèce possède des caractéristiques améliorées et un lore enrichi, ce qui renforce l’immersion et la dynamique du jeu.

<!-- Explication de la méthode -->
La création se fait via une instance de la classe `EspeceMonstre`, en précisant ses statistiques de base, modificateurs, description, particularités, caractères et éléments associés.  
L’exemple de code ci-dessous illustre cette création :
<!--Le code -->
```kotlin
val especePyrokip = EspeceMonstre(
    id = 5,                            // Identifiant unique de l'espèce
    nom = "pyrokip",                  // Nom de l'espèce
    type = "Animal",                  // Type de l'espèce
    
    baseAttaque = 18,                 
    baseDefense = 12,
    baseVitesse = 15,
    baseAttaqueSpe = 22,
    baseDefenseSpe = 11,
    basePv = 70,
    
    modAttaque = 12.0,
    modDefense = 8.0,
    modVitesse = 11.0,
    modAttaqueSpe = 12.5,
    modDefenseSpe = 8.0,
    modPv = 15.0,
    
    description = "Pyrokip, l’évolution de Flamkip. Son feu est devenu intense et ses flammes sont capables de fondre la pierre. Fier et courageux, il protège son dresseur à tout prix.",
    particularites = "Ses flammes changent de couleur selon son humeur : rouge vif en colère, dorées quand il est calme.",
    caracteres = "Fier, protecteur, explosif.",
    elements = mutableListOf(feu)
)
```
<!-- Résumé de l’utilité -->

Cette nouvelle espèce permet de montrer concrètement comment une évolution peut se traduire par une amélioration des statistiques et une personnalisation narrative.
Elle offre au joueur un objectif motivant : faire évoluer ses monstres pour découvrir des formes plus puissantes et uniques.

### C) Création d’une nouvelle espèce : Pyrokip (suite)
![Diagramme d'activité :Front.txt](/imgs%20sprint2/front.txt.png)



![Diagramme d'activité : Back.txt](/imgs%20sprint2/back.txt.png)

<!-- Présentation générale -->
Dans cette partie, nous ajoutons l’ASCII art représentant Pyrokip dans le dossier de ressources,  
puis nous créons un palier d’évolution qui permettra à l’espèce Flamkip d’évoluer en Pyrokip au niveau 7.

> **Note** : L’attribut `elements` doit être utilisé uniquement si le module Element est intégré dans le projet.

<!-- Explication de la méthode -->

#### ASCII Art

Deux fichiers ASCII sont créés dans `ressource/art/pyrokip/` :

- `front.txt`: Représentation frontale de Pyrokip.

Le front.txt :
\u001B[31m
                 .-'*'-.
                /       \
               |   o  o   |
               |    ^^^    |
               |   ( - )   |
                \   '-'   /
               ~~~  | |  ~~~
              ~~~~~  |  ~~~~~
              (    ___    )
               '-./   \.-'
                  /   \
                 /     \
                '       '
\u001B[0m

- `back.txt` : Vue arrière de Pyrokip.

Le back.txt :
\u001B[31m
                 .-'*'-.
                /       \
               |         |
               |   /^\\   |
               |  (   )  |
                \  \_/  /
               ~~~     ~~~
              ~~~~~ | ~~~~~
              (         )
               '-.___.-'
                  |   |
                 /     \
                '       '
\u001B[0m
Palier d’évolution

Palier d’évolution
Avant la fonction main(), on crée le palier d’évolution :
<!--Le code dans main.kt-->
```kotlin
val palierPyrokip = PalierEvolution(
    id = 1,
    niveauRequis = 7,
    evolution = especePyrokip
)
```
Puis dans la fonction main(), on associe ce palier à l’espèce Flamkip :
<!--le code-->
```kotlin
fun main() {
    especeFlamkip.palierEvolution = palierPyrokip

    // Reste du code principal ...
}
```
<!-- Résumé de l’utilité -->

L’ASCII art permet de donner une identité visuelle forte à Pyrokip, enrichissant l’expérience utilisateur.

Le palier d’évolution structure la progression naturelle des monstres, définissant clairement à quel niveau ils peuvent évoluer.

Cette étape prépare le système d’évolution à accueillir de nouvelles espèces et évolutions dans le futur.

<!-- Note -->

Le test de cette évolution en jeu nécessite que le monstre atteigne le niveau 7, ce qui peut prendre du temps dans le contexte actuel où il faut gagner des combats pour monter de niveau.
Des améliorations ultérieures pourraient faciliter ce processus.


### C) Création d’une nouvelle espèce : Pyrokip (fin)

<!-- Présentation générale -->
Afin de vérifier que l'évolution de **Flamkip** en **Pyrokip** fonctionne correctement, nous avons mis en place un test unitaire automatique dans la classe `IndividuMonstreTest`.

Ce test simule la montée de niveau d’un monstre et vérifie son changement d’espèce au bon moment.

> Le fichier de test se trouve dans :  
`test/kotlin/IndividuMonstreTest.kt`

---

<!-- Explication de la méthode -->

Voici le code du test :
```kotlin

class IndividuMonstreTest {

    // Cette méthode est exécutée avant chaque test
    @BeforeTest
    fun setUp() {
        // On associe le palier d’évolution à Flamkip
        especeFlamkip.palierEvolution = palierEvolutionFlamkip
    }

    @Test
    fun levelUp() {
        // Création d’un monstre Flamkip de niveau 5
        var monstre1 = IndividuMonstre(
            id = 2,
            nom = "flamkip",
            experience = 1500.0,
            especeMonstre = especeFlamkip,
            entraineur = null
        )

        // Étape 1 : Niveau 5 → espèce = Flamkip
        assertEquals(especeFlamkip, monstre1.especeMonstre)
        assertEquals(5, monstre1.niveau)

        // Étape 2 : Passage au niveau 6 → pas encore d’évolution
        monstre1.levelUp()
        assertEquals(6, monstre1.niveau)
        assertEquals(especeFlamkip, monstre1.especeMonstre)

        // Étape 3 : Passage au niveau 7 → évolution vers Pyrokip
        monstre1.levelUp()
        assertEquals(7, monstre1.niveau)
        assertEquals(especePyrokip, monstre1.especeMonstre)
    }
}
```

<!-- Résumé de l’utilité -->

Ce test permet de :
Vérifier que l'évolution ne se déclenche pas trop tôt (niveau 5 → 6).
Confirmer que l’évolution fonctionne lorsque le monstre atteint le niveau 7.
Valider automatiquement le comportement de la méthode levelUp() et de l’attribution du palierEvolution.



### 3) 🏙️ Ville

### A) Création de la classe Ville et modification de la classe Zone

<!-- Présentation générale -->
 La classe Zone est rendue ouverte à l'héritage pour permettre la création de sous-classes,
 notamment la classe Ville qui représente un type particulier de zone dans le jeu.

 <!-- Explication de la méthode -->
 Pour cela, on ajoute le mot-clé `open` devant la déclaration de la classe Zone,
 ce qui permet à Ville d’en hériter.
<!--Le code -->
```kotlin
open class Zone(
    val id: Int,
    val nom: String,
    val expZone: Int,
    val especesMonstres: MutableList<EspeceMonstre> = mutableListOf()
) {
    var zoneSuivante: Zone? = null
    var zonePrecedente: Zone? = null
}
```

<!-- Présentation générale -->
 La classe Ville hérite de Zone et ajoute des propriétés spécifiques,
 comme une arène et une liste d’articles en magasin.

 <!-- Explication de la méthode -->
 Ville récupère toutes les propriétés de Zone et ajoute :
 - arene : une instance d’Arene (à définir plus tard)
 - lignesMagasin : une liste d'articles vendus dans la ville (à définir plus tard)
<!--Le code-->
```kotlin
class Arene {

}
class LigneMagasin {
    // TODO : ajouter les propriétés comme item et quantité
}
// Classe représentant une ville, qui est une zone spéciale
// Elle hérite de Zone et ajoute des propriétés spécifiques aux villes
class Ville(
    id: Int,
    nom: String,
    expZone: Int,
    especesMonstres: MutableList<EspeceMonstre> = mutableListOf()
) : Zone(id, nom, expZone, especesMonstres) {

    // TODO - à implémenter plus tard
    lateinit var arene: Arene  // Une ville peut contenir une arène (à définir plus tard)
    var lignesMagasin: MutableList<LigneMagasin> = mutableListOf()     // Une ville peut avoir un magasin avec plusieurs articles à vendre
}
```
### Création de la ville RacailleCity et modification des connexions des zones (suite de A )
 <!-- Présentation générale -->
 Dans main.kt, on crée une instance de Ville appelée RacailleCity, où le joueur peut rencontrer des monstres de l’espèce Galum.

 <!-- Explication de la méthode -->
 On connecte RacailleCity à la zone route2 pour pouvoir naviguer dans les deux sens :
 - route2.zoneSuivante = racailleCity
 - racailleCity.zonePrecedente = route2
<!--Le code-->
```kotlin
val racailleCity = Ville(
    id = 3,
    nom = "RacailleCity",
    expZone = 300,
    especesMonstres = mutableListOf(galum)
)


 Connexion de route2 à RacailleCity (aller)
route2.zoneSuivante = racailleCity

// Connexion de RacailleCity à route2 (retour)
racailleCity.zonePrecedente = route2

// Test fonctionnel pour vérifier la navigation dans les deux sens
println("Depuis route2, la zone suivante est : ${route2.zoneSuivante?.nom}")
println("Depuis RacailleCity, la zone précédente est : ${racailleCity.zonePrecedente?.nom}")

assert(route2.zoneSuivante?.nom == "RacailleCity")
assert(racailleCity.zonePrecedente?.nom == "Route 2")

println("Tests OK")
```

<!-- Résumé de l’utilité -->

La classe Ville étend la classe Zone pour représenter des zones spéciales où le joueur peut s’arrêter, rencontrer des monstres spécifiques, accéder à une arène, ou acheter des objets dans un magasin. La modification des connexions entre zones permet de naviguer facilement dans le monde du jeu, garantissant une exploration fluide entre les routes et les villes.



### B) Ajout des méthodes `soignerEquipe()` et `choisirMonstre()` dans la classe `Entraîneur`
![Diagramme d'activité soignerEquipe : ](/imgs%20sprint2/soigner%20equipe.png)



![Diagramme d'activité choisirMonstre: ](/imgs%20sprint2/choisirmontres.png)




<!-- Présentation générale -->
Ces deux méthodes permettent de gérer l’équipe du dresseur en combat ou hors combat :
soigneEquipe() restaure la santé de tous les monstres en assignant leurs points de vie (PV) au maximum.
choisirMonstre() facilite la sélection d’un monstre pour le combat, avec un choix automatique si un seul est disponible, sinon un menu interactif est affiché pour que l’utilisateur choisisse.

<!-- Explication de la méthode -->
soigneEquipe() parcourt simplement la liste equipeMonstre et remet les PV au maximum.
choisirMonstre() filtre les monstres vivants (PV > 0), affiche la liste avec leurs indices, et demande à l’utilisateur de saisir un choix valide en boucle.

<!--Le code -->
```kotlin
/**
 * Permet de soigner tous les monstres de l'équipe en restaurant leurs PV au maximum.
 * Parcourt chaque monstre et assigne sa valeur de PV maximale à ses PV actuels.
 */
fun soigneEquipe() {
    // Parcours de chaque monstre dans l'équipe
    for (monstre in equipeMonstre) {
        // On assigne les PV actuels (pv) à la valeur maximale (pvMax)
        monstre.pv = monstre.pvMax
    }
}

/**
 * Permet de choisir un monstre valide dans l'équipe.
 * - Si un seul monstre est en état de combattre (pv > 0), il est choisi automatiquement.
 * - Sinon, on affiche un menu pour choisir parmi les monstres vivants.
 *
 * @return le monstre choisi
 */
fun choisirMonstre(): IndividuMonstre {
    // Filtrer la liste des monstres vivants (pv > 0)
    val monstresVivants = equipeMonstre.filter { it.pv > 0 }

    // Si un seul monstre est vivant, le retourner directement (choix automatique)
    if (monstresVivants.size == 1) {
        return monstresVivants[0]
    }

    // Afficher le message pour inviter à choisir un monstre
    println("Choisir un monstre de l'équipe :")

    // Afficher la liste des monstres vivants avec leur index et leurs PV
    monstresVivants.forEachIndexed { index, monstre ->
        println("$index: ${monstre.especeMonstre.nom} (PV: ${monstre.pv}/${monstre.pvMax})")
    }

    // Boucle pour demander une saisie valide à l'utilisateur
    while (true) {
        print("Entrez le numéro du monstre : ")

        // Lire la saisie utilisateur et tenter de la convertir en entier
        val choix = readLine()?.toIntOrNull()

        // Vérifier si le choix est valide (index dans la liste)
        if (choix != null && choix in monstresVivants.indices) {
            // Retourner le monstre choisi
            return monstresVivants[choix]
        }

        // En cas d'erreur, afficher un message et recommencer la saisie
        println("Choix invalide, réessayez.")
    }
}
```
<!-- Résumé de l’utilité -->

Ces méthodes améliorent l’expérience de jeu en automatisant la gestion des monstres soignés et en rendant intuitive la sélection d’un monstre disponible en combat.



### C) Modification de la méthode `jouer()` de la classe `Partie`
![Diagramme d'activité jouer() : ](/imgs%20sprint2/joeur.png)

<!-- Présentation générale -->

Cette méthode jouer() gère le déroulement d’une action dans une partie. Elle affiche la zone actuelle où se trouve le joueur, propose un menu d’actions et exécute l’action choisie par le joueur en fonction de sa saisie.

<!-- Explication de la méthode -->
La méthode affiche la zone courante, puis propose 4 choix :
Rencontrer un monstre sauvage dans la zone (en appelant la méthode rencontreMonstre() de la zone).
Examiner l’équipe de monstres du joueur (avec examineEquipe()).
Aller vers la zone suivante si elle existe (sinon message d’erreur).
Revenir à la zone précédente si elle existe (sinon message d’erreur).
La saisie est lue via readLine(), et un when permet de gérer chaque choix. En cas de saisie invalide, un message d’erreur est affiché.
<!--Le code -->
```kotlin
fun jouer() {
    // Afficher la zone actuelle
    println("Vous êtes dans la zone : ${zone.nom}")

    // Afficher les actions possibles
    println("Que souhaitez-vous faire ?")
    println("1 - Rencontrer un monstre sauvage")
    println("2 - Examiner l’équipe de monstres")
    println("3 - Aller à la zone suivante")
    println("4 - Aller à la zone précédente")
    print("Entrez le numéro de votre choix : ")

    // Lire la réponse de l'utilisateur
    when (readLine()?.trim()) {
        "1" -> {
            // Appeler la méthode rencontreMonstre() de la zone
            zone.rencontreMonstre(entraineur = joueur)
        }

        "2" -> {
            // Appeler la méthode examineEquipe() de la zone
            this.examineEquipe()
        }

        "3" -> {
            // Vérifier si zoneSuivante existe
            val zoneSuivante = zone.zoneSuivante
            if (zoneSuivante != null) {
                // Modifier la zone courante
                zone = zoneSuivante
                println("Vous avancez vers la zone suivante.")
            } else {
                println("Il n'y a pas de zone suivante.")
            }
        }

        "4" -> {
            // Vérifier si zonePrecedente existe
            val zonePrecedente = zone.zonePrecedente
            if (zonePrecedente != null) {
                // Modifier la zone courante
                zone = zonePrecedente
                println("Vous revenez à la zone précédente.")
            } else {
                println("Il n'y a pas de zone précédente.")
            }
        }

        else -> {
            println("Choix invalide. Veuillez réessayer.")
        }
    }
}
```
<!-- Résumé de l’utilité -->
La méthode jouer() structure l’interaction utilisateur à chaque tour, permettant de naviguer entre les zones, d’affronter des monstres ou de gérer son équipe. Elle est essentielle pour la boucle principale de la partie.

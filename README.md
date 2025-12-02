---

# TD2 – Algorithme de Bernstein-Vazirani


Ce projet présente la construction d’un oracle quantique générique et l’implémentation complète de l’algorithme de Bernstein-Vazirani. Il inclut la génération d’une matrice unitaire représentant un oracle, l’exécution de l’algorithme sur un simulateur quantique et l’encodage d’un oracle personnalisable permettant de retrouver un bitstring secret en une seule requête.

---

## 1. Construction d’un oracle quantique générique

Un oracle quantique réalise la transformation suivante :

$$
|x\rangle |y\rangle \longrightarrow |x\rangle |y \oplus f(x)\rangle
$$

avec :

* (x) encodé sur (n) qubits,
* (y) encodé sur (m) qubits,
* (f(x)) une fonction booléenne.

La matrice unitaire (U) associée à cet oracle est explicitement construite sous la forme d’une matrice de permutation de dimension :

$$
2^{n+m} \times 2^{n+m}
$$

L’implémentation repose sur :

* l’itération sur toutes les valeurs possibles de (x) et (y),
* la construction de l’état d’entrée et de sortie via concaténation binaire,
* la mise à jour de la matrice en plaçant un 1 à la position correcte,
* la vérification de l’unitarité via :

$$
U \cdot U^{T} = I
$$

Cette méthode garantit une représentation fidèle de la transformation définie par l’oracle.

---

## 2. Algorithme de Bernstein-Vazirani

Cet algorithme permet d’extraire un bitstring secret (s) définissant la fonction :

$$
f(x) = s \cdot x \pmod{2}
$$

### Étapes du protocole

1. Allouer (n) qubits de données et un qubit ancilla.
2. Appliquer une porte **X** sur l’ancilla pour l’initialiser en $(|1\rangle)$.
3. Appliquer une porte **Hadamard** sur tous les qubits.
4. Appliquer l’oracle, sous forme d’une suite de portes **CNOT** contrôlées.
5. Appliquer une seconde porte **Hadamard** sur les qubits de données.
6. Mesurer les qubits de données : le bitstring obtenu correspond exactement au secret.

L'algorithme garantit la récupération du secret en une seule requête à l’oracle grâce au phénomène d’interférence quantique.

---

## 3. Oracle paramétrable pour un secret arbitraire

Une version généralisée du circuit permet de spécifier un secret encodé sur (n) bits.
Le programme :

* convertit le secret en chaîne binaire,
* applique les portes CNOT nécessaires correspondant aux bits à 1 du secret,
* exécute le circuit sur un simulateur linéaire,
* affiche l’état mesuré et sa probabilité.

Cette version permet de tester l’algorithme avec n’importe quelle valeur secrète.

---

## 4. Résultats

Les expériences réalisées montrent que :

* l’oracle fixe fournit correctement le bitstring `11101`,
* pour un secret personnalisé (exemple : `25`), l’état mesuré est `100111`,
* en retirant le bit ancilla, le bitstring secret reconstitué est `11001`, correspondant à la valeur 25.

Les sorties observées correspondent aux valeurs attendues, validant la construction de l’oracle et le fonctionnement de l’algorithme.

---

## 5. Synthèse

Le projet met en œuvre :

* la construction explicite d’une matrice unitaire représentant un oracle quantique,
* l’implémentation et l’exécution de l’algorithme de Bernstein-Vazirani,
* la création d’un oracle personnalisable pour n’importe quel secret,
* la vérification expérimentale du fonctionnement du circuit quantique.



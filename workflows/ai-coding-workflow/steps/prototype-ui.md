# Prototype UI

**Skill :** `prototype-ui`

**Statut :** On-demand step.

**Rôle :** Explorer rapidement plusieurs directions frontend jetables avant d'intégrer proprement une UI dans le produit.

**Quand l'utiliser :** UX incertaine, écran important, besoin de comparer plusieurs directions visuelles, risque d'AI slop frontend, feature produit où le ressenti utilisateur compte.

**Inputs possibles :** brief, PRD, captures, design system, composants existants, contraintes responsive, parcours utilisateur, inspirations visuelles.

**Actions :**

- définit ce qu'on cherche à apprendre avant de prototyper
- crée une zone temporaire isolée, route de prototype ou sandbox locale
- produit plusieurs variantes cliquables si utile
- utilise des données réalistes ou fixtures légères
- évite toute intégration prématurée dans l'architecture produit
- documente ce qui fonctionne, ce qui ne fonctionne pas, et les éléments à réutiliser
- marque clairement les fichiers comme temporaires ou prépare leur suppression

**Output :** prototypes jetables, synthèse des options, recommandation UX, éléments à réinjecter dans `PRD`, `Tech Design`, `Build` ou support actif.

**Publication de l'artefact :** Les prototypes restent locaux et jetables par défaut. Si une issue parente existe, proposer un commentaire de synthèse avec l'option retenue et les éléments à réinjecter ; ne pas publier le prototype brut comme source de vérité produit.

**Contenu de l'output :**

Contenu obligatoire :

- variantes créées
- option recommandée et raison
- compromis UX
- recommandation d'intégration propre
- fichiers temporaires à supprimer ou conserver brièvement

Contenu conditionnel :

- composants ou patterns réutilisables
- points responsive et accessibilité à surveiller

À éviter :

- transformation implicite du prototype en code produit
- plan produit complet
- description exhaustive de chaque détail visuel

**Tailles possibles :** micro-prototype d'un composant, ou exploration de plusieurs écrans dans une route isolée.

**Gate humain :** choisir la direction visuelle et valider ce qui mérite d'être intégré proprement.

**Important :** Un prototype UI est jetable. Il ne doit pas devenir du code produit par accident.

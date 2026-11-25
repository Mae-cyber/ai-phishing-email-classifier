# AI Phishing Email Classifier

Classification automatique d'emails (phishing vs légitime) à partir du texte, avec analyse qualitative des erreurs du modèle.

## Problème
Les filtres anti-spam par règles sont facilement contournés par reformulation. Ce projet explore une approche par apprentissage statistique du texte pour détecter le phishing.

## Dataset
[zefang-liu/phishing-email-dataset](https://huggingface.co/datasets/zefang-liu/phishing-email-dataset) (Hugging Face, copie du dataset Kaggle "Phishing Email Detection") — 18 634 emails après nettoyage, 61% Safe / 39% Phishing.

## Méthodologie
- Vectorisation TF-IDF (10 000 features, stop words anglais)
- Classification par régression logistique
- Split stratifié 80/20, évaluation par precision/recall/F1 (pas seulement l'accuracy, critique en sécurité)

## Résultats
- **Accuracy : 97%**
- **Recall phishing : 0.98** (peu de phishing non détecté)
- **Precision phishing : 0.96**

## Analyse des erreurs
Examen qualitatif des faux positifs/négatifs sur le jeu de test, et un jeu de test fait main couvrant des techniques connues d'évasion :
- Le modèle rate certains emails contenant du JS embarqué et du bourrage de mots aléatoires dans le dataset d'origine, mais les détecte correctement sur des exemples reformulés — signe d'une généralisation partielle.
- Un cas révélateur de qualité de données : certaines lignes du dataset contenaient la valeur littérale `"empty"` au lieu d'un champ vide, faussant potentiellement l'évaluation.
- Sur un jeu de test construit à la main (10 exemples couvrant les grandes familles de phishing), le modèle obtient 8/10, avec des erreurs discutées individuellement dans le notebook.

## Limites
- Dataset pas nécessairement représentatif des campagnes de phishing actuelles
- Pas testé sur des emails réels en conditions de production
- Approche texte seul : ne couvre pas le phishing par pièce jointe/image

## Compétences démontrées
NLP (TF-IDF), machine learning supervisé, évaluation critique d'un modèle (au-delà de l'accuracy), audit de qualité de données, application concrète à un cas d'usage cybersécurité — en lien avec mon travail de thèse MSc sur la détection d'intrusions par IA (transfer learning, meta-learning).

## Auteur
Maeva Lengue — [LinkedIn](https://linkedin.com/in/maeva-lengue) · [GitHub](https://github.com/Mae-cyber)

# Système RAG avec Routage Intelligent

Un système de chatbot basé sur RAG (Retrieval-Augmented Generation) avec plusieurs stratégies de routage intelligent pour améliorer la qualité des réponses.

## 📋 Description

Ce projet implémente un système RAG avancé qui utilise des techniques de routage pour diriger les questions vers le traitement le plus approprié :

1. **Routage Simple/Complexe** : Détecte si une question est simple ou complexe et adapte le traitement en conséquence
2. **Routage Import/Export** : Route les questions vers le bon vector store selon qu'elles concernent l'import ou l'export

### Fonctionnalités

- ✅ Chargement et traitement de documents (DOCX)
- ✅ Création d'embeddings avec HuggingFace
- ✅ Stockage vectoriel avec ChromaDB
- ✅ Routage intelligent des questions
- ✅ Décomposition de questions complexes en sous-questions
- ✅ Support de plusieurs vector stores (import/export)

## 🚀 Installation

### Prérequis

- Python 3.8+
- Ollama (pour le LLM local)
- Jupyter Notebook

## 📁 Structure du Projet

```
RAG Jupyter/
├── rag_embedding_storing.ipynb    # Création des embeddings et vector stores
├── rag_routing.ipynb              # Système de routage intelligent
├── documents/                     # Dossier pour vos documents (à créer)
│   ├── import_document.docx
│   └── export_document.docx
├── chroma_store/                  # Vector stores persistés (généré automatiquement)
│   ├── import/
│   └── export/
├── .env.example                   # Exemple de fichier de configuration
├── requirements.txt               # Dépendances Python
└── README.md                      # Ce fichier
```

## 🔧 Configuration

### 1. Préparer vos documents

Placez vos documents dans le dossier `documents/` :
- `documents/import_document.docx` : Documents relatifs à l'import
- `documents/export_document.docx` : Documents relatifs à l'export

### 2. Créer les vector stores

Exécutez le notebook `rag_embedding_storing.ipynb` pour :
- Charger vos documents
- Les découper en chunks
- Créer les embeddings
- Persister les vector stores dans `chroma_store/`

**Important** : Modifiez les chemins des documents dans la cellule 2 du notebook avant d'exécuter.

### 3. Utiliser le système de routage

Exécutez le notebook `rag_routing.ipynb` pour utiliser le système de routage intelligent.

## 📖 Utilisation

### Routage Simple/Complexe

Le système détecte automatiquement si une question est simple ou complexe :

- **Questions simples** : Traitées directement avec un RAG standard
- **Questions complexes** : Décomposées en sous-questions, traitées individuellement, puis synthétisées

Exemple :
```python
result = hybrid_routing_pipeline("Quelles sont les exigences pour importer du matériel médical au Maroc ?")
```

### Routage Import/Export

Le système route automatiquement les questions vers le bon vector store :

```python
result = import_export_router("Quels sont les documents nécessaires pour exporter du textile ?")
```

## 🛠️ Technologies Utilisées

- **LangChain** : Framework pour les applications LLM
- **ChromaDB** : Base de données vectorielle
- **HuggingFace Embeddings** : Modèles d'embedding (BAAI/bge-large-en-v1.5)
- **Ollama** : LLM local (Mistral)
- **Jupyter Notebook** : Environnement de développement

## ⚙️ Paramètres Configurables

### Embeddings
- Modèle : `BAAI/bge-large-en-v1.5` (ou `BAAI/bge-base-en-v1.5` pour une version plus légère)
- Modifiable dans `rag_embedding_storing.ipynb`

### Text Splitting
- `chunk_size` : 1000 caractères
- `chunk_overlap` : 100 caractères
- Séparateur personnalisé pour les codes SH

### LLM
- Modèle : Mistral (via Ollama)
- Modifiable dans `rag_routing.ipynb`

## 📝 Notes Importantes

1. **Modèles d'embedding** : Assurez-vous d'utiliser le même modèle d'embedding lors de la création des vector stores et lors de leur utilisation.

2. **Chemins des documents** : Modifiez les chemins dans `rag_embedding_storing.ipynb` pour pointer vers vos propres documents.

3. **Ollama** : Le système utilise Ollama pour le LLM local. Assurez-vous qu'Ollama est en cours d'exécution avant d'utiliser les notebooks.

4. **Vector stores** : Les vector stores sont persistés dans `chroma_store/`. Ne supprimez pas ce dossier si vous voulez réutiliser les embeddings.

## 🤝 Contribution

Les contributions sont les bienvenues ! N'hésitez pas à ouvrir une issue ou une pull request.

## 📄 Licence

Ce projet est sous licence MIT.

## 👤 Auteur

Créé dans le cadre d'un projet de stage.

## 🙏 Remerciements

- LangChain pour le framework
- HuggingFace pour les modèles d'embedding
- Ollama pour le LLM local

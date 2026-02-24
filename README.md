# Vilaine Amont

Visualisation et prédiction des hauteurs d'eau et débits des 11 stations hydrométriques du bassin Vilaine Amont, à partir des données ouvertes de [Hydro EauFrance](https://www.hydro.eaufrance.fr), avec un modèle ML de prévision de crues.

## Démarrage rapide

```bash
# Installer les dépendances
npm -C backend install
npm -C frontend install

# Lancer le projet
npm run dev
```

Le frontend est accessible sur http://localhost:5173.

## Fonctionnalités

- Sélection parmi les 11 stations du bassin Vilaine Amont
- Récupération des séries Hauteur (H) et Débit (Q) via l'API Hydro EauFrance
- Graphique interactif double axe avec tooltip
- Prévisions ML (modèle Station-Attention) avec intervalles de confiance

## Architecture

```
vilaine-amont/
  backend/          Proxy Express (port 3001) + inférence ONNX
  frontend/         SPA SolidJS + uPlot (Vite, port 5173)
  ml/               Pipeline ML (PyTorch) pour l'entraînement
```

Le backend sert de proxy pour contourner les restrictions CORS de l'API EauFrance et exécute le modèle de prévision ONNX. Le frontend appelle `/api/station/:id/series` qui est relayé par Vite en dev.

Le pipeline ML (collecte, préparation, entraînement, export ONNX) est documenté dans [ml/README.md](ml/README.md).

## Licence

Ce projet est sous licence [MIT](LICENSE).

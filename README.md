🏢 API Immobilier — Les Résidences Relief

Bienvenue dans la documentation de l'API REST des Résidences Relief. Cette API permet d'accéder aux données immobilières de nos projets, incluant les immeubles (blocs) et les unités individuelles (appartements, villas, locaux commerciaux, etc.).

🌐 Configuration Globale

URL de base : https://admin.reliefresidences.ma/api/v1

Format de réponse : Tous les retours de l'API sont au format JSON.

🔐 Authentification

L'API utilise une authentification par clé API. Tous les endpoints (à l'exception de /health) nécessitent une clé valide.

Option recommandée : En-tête HTTP
Ajoutez votre clé dans les en-têtes de votre requête :

X-API-Key: votre_clé_api_ici


Alternative (pour les tests uniquement) : Paramètre d'URL

GET /api/v1/properties?api_key=votre_clé_api_ici


🚀 Endpoints Disponibles

1. Vérification de santé (Public)

GET /health : Vérifie que le service API est en ligne.

2. Propriétés / Unités

GET /properties : Liste toutes les unités immobilières avec support de la pagination et de multiples filtres (type, statut, prix, nombre de pièces, etc.).

GET /properties/{id} : Récupère les détails complets d'une unité spécifique (incluant les commodités, coordonnées GPS, et informations du propriétaire).

3. Projets Immobiliers

GET /projects : Liste tous les projets immobiliers (ex: RELIEF I).

GET /projects/{id} : Récupère les détails d'un projet, incluant la liste de ses immeubles (blocs) et de toutes ses unités associées.

💻 Exemples d'utilisation

cURL

Récupérer les appartements F3 disponibles à la vente :

curl -H "X-API-Key: VOTRE_CLE_API" \
  "[https://admin.reliefresidences.ma/api/v1/properties?unit_morphology=f3&stage=available&sale_lease=for_sale](https://admin.reliefresidences.ma/api/v1/properties?unit_morphology=f3&stage=available&sale_lease=for_sale)"


JavaScript (Fetch)

const BASE_URL = "[https://admin.reliefresidences.ma/api/v1](https://admin.reliefresidences.ma/api/v1)";
const API_KEY = "VOTRE_CLE_API";

async function fetchProperties() {
  const response = await fetch(`${BASE_URL}/properties?type=residential`, {
    headers: {
      "X-API-Key": API_KEY
    }
  });
  
  const result = await response.json();
  if(result.success) {
      console.log(`Trouvé ${result.pagination.total} propriétés.`);
      console.log(result.data);
  }
}

fetchProperties();


⚠️ Format des Réponses et Erreurs

Toutes les réponses de l'API suivent une structure standardisée :

En cas de succès (200 OK) :

{
  "success": true,
  "data": { ... },
  "pagination": { "page": 1, "per_page": 50, "total": 120, "total_pages": 3 } 
}


En cas d'erreur (401, 404, etc.) :

{
  "success": false,
  "error": "Description de l'erreur"
}


📚 Documentation complète

Pour consulter la liste exhaustive des paramètres de filtrage, les dictionnaires de données (statuts, types, etc.) et le détail des objets JSON retournés, veuillez vous référer à la Documentation API Complète (PDF).
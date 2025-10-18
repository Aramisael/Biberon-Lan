rules\_version \= '2';  
service cloud.firestore {  
match /databases/{database}/documents {  
// Definimos el ID de la aplicación que usamos en index.html  
// Debe coincidir con la variable 'appId' en index.html ("mr-biberon-final")  
function getAppId() {  
return "mr-biberon-final";  
}  
// Ruta a la colección pública de High Scores  
match /artifacts/{appId}/public/data/high\_scores/{scoreId} {  
  // 1\. Permite la lectura (listas y documentos individuales) a CUALQUIER USUARIO (incluso sin autenticación)  
  allow read: if true; 

  // 2\. Permite la creación de un nuevo score si:  
  allow create: if request.auth.uid \!= null  // El usuario está autenticado (aunque sea anónimamente)  
               && request.resource.data.score \> 0 // El score es positivo  
               && request.resource.data.name.size() \<= 12 // El nombre no supera los 12 caracteres  
               && request.resource.data.userId \== request.auth.uid // El usuario solo puede registrar su propio ID  
               && getAppId() \== appId; // Asegura que el acceso es solo para esta aplicación

  // Prohibir actualizaciones y eliminaciones de scores existentes para mantener la integridad del ranking  
  allow update, delete: if false;  
}

// Prohibir acceso a otras colecciones por defecto  
match /{document=\*\*} {  
  allow read, write: if false;  
}

}  
}
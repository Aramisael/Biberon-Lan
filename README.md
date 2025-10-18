# **MR.BIBERÓN FINAL**

¡Bienvenido al juego MR. BIBERÓN\! Esquiva obstáculos y recolecta mamaderas en un ambiente de movimiento fluido y un ranking de puntuaciones compartido.

## **🚀 Cómo Jugar**

1. Abre el archivo index.html directamente en tu navegador.  
2. Elige tu Guardián.  
3. Usa las flechas **Izquierda/Derecha** (PC) o **Swipe/Desliza** (Móvil) para moverte y recolectar las mamaderas (🍼) y esquivar los obstáculos (💥 y 💣).

## **🏆 Tabla de Clasificación Compartida (High Scores)**

Este juego utiliza Google Firestore (Firebase) para mantener una tabla de clasificación global y persistente. **Es OBLIGATORIO configurar Firebase para que esto funcione.**

### **⚠️ PASO CRÍTICO DE CONFIGURACIÓN DE FIREBASE ⚠️**

Para que la tabla de clasificación funcione, debes reemplazar los marcadores de posición en index.html:

1. **Crea o usa un Proyecto en Firebase.** Habilita **Authentication (Anónimo)** y **Firestore Database**.  
2. **Obtén tu configuración web (firebaseConfig).**  
3. **Edita index.html:** Busca el siguiente bloque de código cerca de la línea 550 y reemplaza **todos** los valores TU\_API\_KEY\_AQUI, etc., con tus claves reales.  
   const FIREBASE\_CONFIG\_PLACEHOLDER \= "TU\_API\_KEY\_AQUI"; // Este es el marcador de posición. Reemplazar\!

   const firebaseConfig \= {  
       apiKey: FIREBASE\_CONFIG\_PLACEHOLDER,   
       authDomain: FIREBASE\_CONFIG\_PLACEHOLDER,  
       projectId: FIREBASE\_CONFIG\_PLACEHOLDER,   
       // ... el resto de tus claves  
   };

4. **Configurar Reglas de Seguridad (Imprescindible):**  
   * En la consola de Firebase, ve a **Firestore Database** \-\> Pestaña **"Reglas"**.  
   * Copia y pega el contenido del archivo firestore.rules de este repositorio y **PUBLICAR** las reglas.

### **💡 Solución de Problemas**

#### **Error: Firebase NO CONFIGURADO: Por favor, inserte su firebaseConfig real en index.html.**

**Causa:** El juego está detectando que los marcadores de posición (TU\_API\_KEY\_AQUI) aún no han sido reemplazados por tus valores reales de Firebase.

**Solución:** Ve al paso 3 de la sección anterior y asegúrate de que **TODAS** las propiedades del objeto firebaseConfig tengan valores reales obtenidos de tu consola de Firebase.

#### **Error: El TOP 5 no se muestra o las puntuaciones no se guardan.**

**Causa 1 (Guardar/Escribir):** Las reglas de seguridad de Firestore no están configuradas correctamente o no se han publicado.

**Solución:** Asegúrate de que las reglas de firestore.rules estén copiadas y publicadas en la pestaña "Reglas" de tu Firestore Database.

**Causa 2 (Autenticación):** El método de inicio de sesión "Anónimo" no está habilitado en Firebase Authentication.

**Solución:** Habilita el inicio de sesión "Anónimo" en tu proyecto de Firebase.
# TP 27 : Test de charge & Observabilité : Concurrence + Verrou DB + Resilience4j + Actuator 

## ✅ Ce que ce TP permet de vérifier (validation finale)

À la fin du TP, on peut confirmer que l’architecture fonctionne **comme en production**.

### 🔄 Concurrence & intégrité des données
Plusieurs emprunts arrivent **en même temps** sur les 3 instances :

- http://localhost:8081  
- http://localhost:8083  
- http://localhost:8084  

✔ Le **verrou en base de données** empêche le stock de devenir négatif.  
➡️ Aucun double-emprunt impossible, même avec 3 instances.

---

### 🛡 Résilience applicative

Quand **pricing-service tombe en panne** :

- book-service **continue**
- un **fallback** est appliqué (prix par défaut)
- l’utilisateur ne subit pas d’erreur critique

✔ Les métriques Actuator montrent que :

- **Retry** se déclenche
- **CircuitBreaker** s’ouvre après plusieurs échecs

---
<img width="1098" height="559" alt="image" src="https://github.com/user-attachments/assets/0ead8479-8482-4d80-9654-fdeffcc16d6c" />
<img width="1089" height="245" alt="image-1" src="https://github.com/user-attachments/assets/08bd4ae5-f718-47b2-b2d8-4e4507af222f" />
## 🚦 Prérequis avant de commencer les tests

Assurez-vous que toute la stack Docker est lancée :

```bash
docker compose up -d --build



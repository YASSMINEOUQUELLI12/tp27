# TP 27 : Test de charge & Observabilité : Concurrence + Verrou DB + Resilience4j + Actuator 

# Etape A :
<img width="1098" height="559" alt="image" src="https://github.com/user-attachments/assets/0ead8479-8482-4d80-9654-fdeffcc16d6c" />


# Etape B :
<img width="1089" height="245" alt="image-1" src="https://github.com/user-attachments/assets/08bd4ae5-f718-47b2-b2d8-4e4507af222f" />

# Etape C :
<img width="1093" height="309" alt="image-2" src="https://github.com/user-attachments/assets/ddbab232-9a69-4482-8fb7-0a6fbd1817b9" />

# Etape D :
<img width="1074" height="244" alt="image-3" src="https://github.com/user-attachments/assets/da97cbf8-d621-4d29-b5fa-134bca96acf0" />

# Etape E :
<img width="1096" height="462" alt="image-4" src="https://github.com/user-attachments/assets/3e78b2c1-8596-476b-8a70-ad2d578b0aac" />

# Etape F1 :
<img width="1082" height="157" alt="image-5" src="https://github.com/user-attachments/assets/135d860b-d552-4c68-8b0c-f3ec4c6949f1" />

# Etape F2 :
<img width="1084" height="248" alt="image-6" src="https://github.com/user-attachments/assets/804f1a94-f7c7-47fb-b749-52d10162dc35" />

# Etape F3 :
<img width="1091" height="650" alt="image-7" src="https://github.com/user-attachments/assets/604f9cda-ecad-4b4f-b0a2-2e1e1ac454a2" />

# Etape F4 :
<img width="1081" height="296" alt="image-8" src="https://github.com/user-attachments/assets/6035ab5b-7f91-422e-b077-b1288086ef01" />

# Etape G1 :
<img width="1096" height="659" alt="image-9" src="https://github.com/user-attachments/assets/025760b4-6e30-4633-8a98-4d9d62c26d4e" />

# Etape G2 :
<img width="1086" height="453" alt="image-10" src="https://github.com/user-attachments/assets/f4382316-9358-45fb-aa1e-f6b5302aca23" />

## Conclusion

1. **Verrou DB nécessaire :** En multi-instances, sans verrou pessimiste (`SELECT ... FOR UPDATE`), plusieurs instances liraient le même stock simultanément et le décrémentent toutes, causant un stock négatif. Le verrou garantit une modification atomique.

2. **Circuit Breaker :** Il "ouvre le circuit" après un seuil d'échecs pour éviter de surcharger un service défaillant, puis teste périodiquement sa disponibilité (état HALF_OPEN) avant de reprendre les appels normaux.

3. **Fallback :** Quand le service externe est indisponible, il retourne une valeur par défaut (`price=0.0`) pour que l'application reste fonctionnelle sans bloquer l'utilisateur.

4. **Résilience combinée :** Retry (erreurs temporaires) + Circuit Breaker (isolation des pannes) + Fallback (réponse dégradée) = système robuste et haute disponibilité.

5. **Observabilité :** Les métriques Actuator permettent de monitorer l'état du circuit breaker et les retries en temps réel pour anticiper et diagnostiquer les incidents.



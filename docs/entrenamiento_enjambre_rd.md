# Entrenamiento para un enjambre de agentes que predigan la reacción ciudadana ante medidas políticas en la República Dominicana

## 1) Objetivo del sistema
Diseñar un enjambre de agentes de IA que simulen segmentos de la ciudadanía dominicana para estimar:
- aceptación/rechazo de una medida;
- probabilidad de protesta, apoyo o indiferencia;
- narrativas clave por territorio y grupo social;
- riesgos de polarización y desinformación.

> **Nota**: este sistema debe usarse para análisis de políticas públicas y participación ciudadana, no para manipulación política.

---

## 2) Definición del problema

### Salidas esperadas
Para cada medida política (input), el sistema debe producir:
1. **Índice de aprobación estimado** (0–100);
2. **Distribución emocional** (confianza, enojo, esperanza, miedo);
3. **Temas dominantes** por segmento (empleo, seguridad, costo de vida, corrupción, servicios);
4. **Probabilidad de movilización social** a 7/30/90 días;
5. **Explicaciones trazables** de por qué ciertos segmentos reaccionan así.

### Granularidad recomendada
- **Geográfica**: macro-regiones y principales provincias.
- **Socioeconómica**: nivel de ingreso, ocupación, informalidad laboral.
- **Demográfica**: edad, género, nivel educativo.
- **Conductual**: consumo de noticias, confianza institucional, participación cívica.

---

## 3) Arquitectura del enjambre (multiagente)

### Agentes sugeridos
1. **Agente Censo**: sintetiza composición poblacional por segmento.
2. **Agente Economía del Hogar**: modela sensibilidad a inflación, subsidios, empleo.
3. **Agente Territorial**: incorpora prioridades locales y desigualdades territoriales.
4. **Agente Narrativas**: identifica marcos discursivos favorables y adversos.
5. **Agente Redes Sociales**: modela propagación y amplificación de mensajes.
6. **Agente Confianza Institucional**: estima credibilidad del emisor de la medida.
7. **Agente Historial Político**: usa precedentes de políticas similares.
8. **Agente Moderador/Árbitro**: agrega resultados y detecta inconsistencias.

### Mecanismo de coordinación
- Cada agente emite una predicción con **incertidumbre**.
- Un agregador tipo **mixture-of-experts** combina salidas ponderadas.
- Se ejecutan rondas de **debate interno** entre agentes para reducir sesgos.
- Se conserva un **registro de razonamiento resumido** por trazabilidad.

---

## 4) Datos de entrenamiento

### Fuentes útiles
- Encuestas de opinión pública históricas.
- Series de indicadores económicos y sociales.
- Hemerotecas y comunicados oficiales.
- Corpus de redes sociales (anonimizado y agregado).
- Registros de eventos de movilización/protesta.

### Variables clave (features)
- Tipo de medida: fiscal, seguridad, salud, transporte, educación.
- Intensidad percibida del impacto económico en el hogar.
- Momento macroeconómico (inflación, empleo, salarios reales).
- Credibilidad del gobierno y de actores opositores.
- Exposición mediática y tono informativo.

### Etiquetas (targets)
- Aprobación/rechazo observado.
- Variación temporal del sentimiento.
- Nivel de conflictividad social asociado.

---

## 5) Pipeline de entrenamiento

1. **Ingesta y normalización** de datos multimodales.
2. **Construcción de perfiles sintéticos** por segmento ciudadano.
3. **Entrenamiento especializado por agente** (cada agente aprende una dimensión).
4. **Calibración conjunta** del agregador del enjambre.
5. **Backtesting temporal** con políticas reales del pasado.
6. **Stress tests** (shocks económicos, campañas de desinformación, crisis).
7. **Monitoreo continuo** de deriva de datos y degradación de desempeño.

---

## 6) Métricas de evaluación

- **Clasificación**: F1, precisión, recall en apoyo/rechazo.
- **Probabilidad**: Brier score, log-loss, curvas de calibración.
- **Ranking de riesgo social**: NDCG/Precision@K para eventos de alta tensión.
- **Robustez**: desempeño por región y segmento (equidad de error).
- **Estabilidad**: sensibilidad de predicciones ante pequeños cambios de input.

---

## 7) Validación causal y de política pública

Para evitar correlaciones espurias:
- usar diseños cuasi-experimentales cuando sea posible;
- separar efectos de comunicación vs efectos reales de la medida;
- incluir contrafactuales: “¿qué pasaría sin la medida?”;
- someter resultados a revisión de expertos en política pública y ciencias sociales.

---

## 8) Riesgos y guardrails éticos

1. **No microtargeting manipulativo** de grupos vulnerables.
2. **Privacidad por diseño**: anonimización, agregación y minimización de datos.
3. **Transparencia**: reportar incertidumbre y límites del modelo.
4. **Auditoría de sesgos**: revisar sesgo territorial, socioeconómico y de género.
5. **Uso responsable**: soporte a decisiones públicas, no sustituto del debate democrático.

---

## 9) Plan de implementación (90 días)

### Fase 1 (Semanas 1–3): Fundaciones
- Definir taxonomía de medidas políticas.
- Unificar esquema de datos y crear diccionario de variables.
- Prototipo de 2–3 agentes base.

### Fase 2 (Semanas 4–8): Enjambre mínimo viable
- Entrenar agentes especializados.
- Integrar agregador y calibración.
- Backtesting con 3–5 casos históricos.

### Fase 3 (Semanas 9–12): Piloto operativo
- Tablero de riesgo/reacción ciudadana.
- Validación con expertos locales.
- Documento de gobernanza y uso ético.

---

## 10) Entregables recomendados

- Modelo multiagente entrenado + reporte técnico.
- Dashboard con escenarios “qué pasa si”.
- Protocolo de monitoreo y recalibración mensual.
- Guía de interpretación para decisores públicos.

---

## 11) Recomendación práctica inicial

Comenzar con un **MVP de bajo riesgo**:
- 5 segmentos ciudadanos;
- 3 tipos de medidas (económicas, seguridad, servicios públicos);
- horizonte de predicción de 30 días;
- revisión humana obligatoria antes de cualquier uso institucional.

Este enfoque reduce complejidad inicial y permite aprender rápido antes de escalar.

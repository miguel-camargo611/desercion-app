# Alerta temprana de deserción — app

App Streamlit del proyecto integrador de **Machine Learning II** (Universidad Externado de
Colombia, 2026-2) · Miguel Camargo y Camilo Hernández · Prof. Wilmer Pineda.

Estima, al terminar el primer semestre, la probabilidad de que un estudiante de pregrado ya no
esté matriculado al cerrar su primer año, la clasifica en un nivel de riesgo con una acción
sugerida y explica la predicción con SHAP. Admite un estudiante o un archivo CSV/Excel con varios.

| | |
|---|---|
| Modelo | LightGBM dentro de un Pipeline (imputación, escalado, one-hot) |
| Datos de entrenamiento | *Student Dropout Dataset*, Tec de Monterrey, cohortes AD19–AD20 |
| Evaluación única en prueba sellada | PR-AUC 0,220 (azar 0,076) · ROC-AUC 0,708 · el 20 % de mayor riesgo concentra el 48 % de los desertores |

## Qué contiene este repositorio

Solo lo necesario para ejecutar la app; **no contiene datos de estudiantes**:

- `app/` — interfaz, servicio del modelo (validación contra el contrato, predicción, SHAP), estilo y gráficos.
- `artifacts/model.joblib` — el Pipeline entrenado (parámetros del modelo).
- `artifacts/model_metadata.json` — contrato: orden y rangos de las variables, umbral, versión, métricas y limitaciones.
- `artifacts/reference_prediction.json` — un perfil **ficticio** y su probabilidad, para verificar que el modelo da lo mismo en cualquier entorno.

El análisis completo (preparación de datos, comparación de 9 modelos con validación cruzada
anidada, pruebas de sensibilidad, Docker y pruebas automáticas) está en el repositorio
principal del proyecto, que es privado porque los datos del TEC DataHub no se redistribuyen.

## Ejecutar en local

```bash
pip install -r app/requirements.txt
streamlit run app/main.py
```

## Uso responsable

Demostración académica: no usar para decisiones sobre estudiantes reales. La señal es débil
(ROC-AUC ≈ 0,7): la alerta sirve para priorizar a quién acompañar, no para diagnosticar. SHAP
describe cómo decide el modelo, no relaciones causales.

# 20 - Machine Learning y Deep Learning

> Sistemas que aprenden de datos para hacer predicciones, clasificaciones y generación de contenido.

[🏠 Volver al índice](./00-indice.md)

---

## 📋 Índice Rápido

- [🤖 Machine Learning](#machine-learning)
- [📊 Tipos de Aprendizaje](#tipos-de-aprendizaje)
- [🧠 Algoritmos Clásicos (ML)](#algoritmos-clasicos-ml)
- [🧠 Deep Learning](#deep-learning)
- [🗣️ NLP (Natural Language Processing)](#nlp-natural-language-processing)
- [👁️ Computer Vision](#computer-vision)
- [🔄 MLOps](#mlops)
- [📊 Pipeline ML](#pipeline-ml)
- [🎯 Evaluación de Modelos](#evaluacion-de-modelos)
- [🔧 Feature Engineering](#feature-engineering)
- [⚙️ Optimización Hiperparámetros](#optimizacion-hiperparametros)
- [🧪 Validación](#validacion)
- [🚫 Problemas Comunes](#problemas-comunes)
- [🔐 Ética y Fairness](#etica-y-fairness)
- [📚 Recursos](#recursos)
---

## 🤖 Machine Learning

**What:** Algoritmos que mejoran con experiencia sin ser programados explícitamente.

**Why:** Automatizar decisiones, encontrar patrones, personalización.

**Who:** Data Scientists, ML Engineers, Research Engineers.

**How much:** Alta inversión inicial (datos, entrenamiento), ROI variable según caso de uso.

---

## 📊 Tipos de Aprendizaje

| Tipo | What | When | Algoritmos |
|:-----|:-----|:-----|:-----------|
| **Supervisado** | Aprender de datos etiquetados | Clasificación, regresión | Linear Regression, Random Forest, XGBoost, SVM |
| **No Supervisado** | Encontrar patrones sin etiquetas | Clustering, reducción dimensionalidad | K-Means, DBSCAN, PCA, t-SNE |
| **Semi-Supervisado** | Pocos labels + muchos unlabeled | Etiquetado costoso | Self-training, co-training |
| **Reinforcement Learning** | Aprender por reward/penalty | Gaming, robótica, trading | Q-Learning, DQN, PPO, A3C |

---

## 🧠 Algoritmos Clásicos (ML)

| Algoritmo | What | When | Pros/Cons |
|:----------|:-----|:-----|:----------|
| **Linear Regression** | Predecir valor continuo | Relación lineal | ✅ Simple, interpretable<br>❌ Solo lineal |
| **Logistic Regression** | Clasificación binaria | Baseline classification | ✅ Rápido, probabilístico<br>❌ Solo linealmente separable |
| **Decision Trees** | Árbol de decisiones | Interpretabilidad | ✅ Fácil explicar<br>❌ Overfitting |
| **Random Forest** | Ensemble de árboles | Clasificación/regresión robusta | ✅ Reduce overfitting<br>❌ Menos interpretable |
| **XGBoost** | Gradient boosting optimizado | Competencias Kaggle | ✅ SOTA en tabular<br>❌ Tuning complejo |
| **SVM** | Support Vector Machines | Clasificación con kernel | ✅ Efectivo high-dim<br>❌ Lento en big data |
| **K-Means** | Clustering por centroides | Segmentación clientes | ✅ Simple<br>❌ Requiere K predefinido |
| **PCA** | Reducción dimensionalidad | Visualización, preprocessing | ✅ Elimina colinealidad<br>❌ Pierde interpretabilidad |

**Herramientas:** [scikit-learn](https://scikit-learn.org/), [XGBoost](https://xgboost.readthedocs.io/), [LightGBM](https://lightgbm.readthedocs.io/)

---

## 🧠 Deep Learning

**What:** Redes neuronales con múltiples capas.

**Why:** Aprende representaciones complejas, SOTA en visión, NLP, audio.

| Arquitectura | What | When | Use Cases |
|:-------------|:-----|:-----|:----------|
| **CNN** (Convolutional) | Redes para datos espaciales | Imágenes, video | Clasificación imágenes, detección objetos |
| **RNN** (Recurrent) | Redes para secuencias | Series temporales, texto | Predicción series, sentiment analysis |
| **LSTM** (Long Short-Term Memory) | RNN con memoria long-term | Secuencias largas | Traducción, generación texto |
| **Transformer** | Attention mechanism | NLP moderno | BERT, GPT, traducción |
| **GAN** (Generative Adversarial) | Generador vs Discriminador | Generar imágenes realistas | Deepfakes, data augmentation |
| **Autoencoder** | Encoder-Decoder | Reducción dimensionalidad, denoising | Compresión, anomalías |
| **Diffusion Models** | Generación iterativa | Generación imagen SOTA | DALL-E, Stable Diffusion |

**Frameworks:** [PyTorch](https://pytorch.org/), [TensorFlow](https://www.tensorflow.org/), [Keras](https://keras.io/), [JAX](https://github.com/google/jax)

---

## 🗣️ NLP (Natural Language Processing)

| Tarea | What | Modelos |
|:------|:-----|:--------|
| **Clasificación texto** | Categorizar documentos | BERT, RoBERTa, DistilBERT |
| **NER** (Named Entity Recognition) | Extraer entidades | spaCy, Flair |
| **Sentiment Analysis** | Detectar sentimiento | Fine-tuned BERT |
| **Traducción** | Traducir entre idiomas | mT5, MarianMT |
| **Question Answering** | Responder preguntas | BERT-QA, T5 |
| **Text Generation** | Generar texto coherente | GPT-4, Claude, LLaMA |
| **Embeddings** | Vectorizar texto | Word2Vec, GloVe, BERT embeddings |

**Herramientas:** [Hugging Face](https://huggingface.co/), [spaCy](https://spacy.io/), [LangChain](https://www.langchain.com/)

---

## 👁️ Computer Vision

| Tarea | What | Modelos |
|:------|:-----|:--------|
| **Clasificación** | Etiquetar imagen | ResNet, EfficientNet, Vision Transformer |
| **Detección objetos** | Ubicar objetos en imagen | YOLO, Faster R-CNN |
| **Segmentación** | Clasificar cada pixel | U-Net, Mask R-CNN |
| **Pose Estimation** | Detectar posición humana | OpenPose, MediaPipe |
| **OCR** | Extraer texto de imagen | Tesseract, EasyOCR |
| **Face Recognition** | Identificar personas | FaceNet, ArcFace |

**Herramientas:** [OpenCV](https://opencv.org/), [YOLO](https://github.com/ultralytics/ultralytics), [MediaPipe](https://mediapipe.dev/)

---

## 🔄 MLOps

**What:** DevOps para Machine Learning (automatizar pipeline ML).

**Why:** Reproducibilidad, deployment continuo, monitoreo modelos.

| Fase | What | Herramientas |
|:-----|:-----|:-------------|
| **Experiment Tracking** | Registrar entrenamientos | [MLflow](https://mlflow.org/), [Weights & Biases](https://wandb.ai/) |
| **Feature Store** | Centralizar features | [Feast](https://feast.dev/), [Tecton](https://www.tecton.ai/) |
| **Model Registry** | Versionar modelos | MLflow, [DVC](https://dvc.org/) |
| **Training** | Pipeline entrenamiento | [Kubeflow](https://www.kubeflow.org/), [SageMaker](https://aws.amazon.com/sagemaker/) |
| **Serving** | Deploy modelos | [TorchServe](https://pytorch.org/serve/), [TensorFlow Serving](https://www.tensorflow.org/tfx/guide/serving) |
| **Monitoring** | Detectar drift | [Evidently](https://www.evidentlyai.com/), [WhyLabs](https://whylabs.ai/) |

---

## 📊 Pipeline ML

```
1. Problem Definition
   ↓
2. Data Collection
   ↓
3. Data Cleaning & EDA
   ↓
4. Feature Engineering
   ↓
5. Model Training
   ↓
6. Evaluation (test set)
   ↓
7. Hyperparameter Tuning
   ↓
8. Deployment
   ↓
9. Monitoring & Retraining
```

---

## 🎯 Evaluación de Modelos

### Clasificación

| Métrica | What | When |
|:--------|:-----|:-----|
| **Accuracy** | % correctos | Clases balanceadas |
| **Precision** | % de positivos correctos | Minimizar falsos positivos |
| **Recall** | % de positivos encontrados | Minimizar falsos negativos |
| **F1-Score** | Media armónica precision/recall | Balance |
| **ROC-AUC** | Área bajo curva ROC | Evaluar probabilidades |
| **Confusion Matrix** | Visualizar errores | Entender errores |

### Regresión

| Métrica | What | When |
|:--------|:-----|:-----|
| **MAE** | Mean Absolute Error | Interpretar error promedio |
| **MSE** | Mean Squared Error | Penalizar errores grandes |
| **RMSE** | Root MSE | Misma escala que target |
| **R²** | Varianza explicada | Comparar modelos |

---

## 🔧 Feature Engineering

| Técnica | What | Ejemplo |
|:--------|:-----|:--------|
| **Encoding** | Convertir categóricas | One-hot, label encoding |
| **Scaling** | Normalizar rangos | StandardScaler, MinMaxScaler |
| **Binning** | Discretizar continuas | Edad → grupos etarios |
| **Interactions** | Combinar features | precio * cantidad |
| **Time Features** | Extraer de fechas | día_semana, mes, hora |
| **Text Features** | De texto a números | TF-IDF, embeddings |

---

## ⚙️ Optimización Hiperparámetros

| Método | What | When |
|:-------|:-----|:-----|
| **Grid Search** | Probar todas combinaciones | Pocos hiperparámetros |
| **Random Search** | Sampling aleatorio | Más hiperparámetros |
| **Bayesian Optimization** | Optimización inteligente | Entrenamientos costosos |
| **Optuna** | AutoML hyperparameter tuning | Automatizar búsqueda |

**Herramientas:** [Optuna](https://optuna.org/), [Ray Tune](https://docs.ray.io/en/latest/tune/index.html), [Hyperopt](http://hyperopt.github.io/hyperopt/)

---

## 🧪 Validación

| Técnica | What | When |
|:--------|:-----|:-----|
| **Train/Test Split** | 80-20 o 70-30 | Dataset suficientemente grande |
| **K-Fold CV** | K subsets, entrenar K veces | Datasets pequeños |
| **Stratified K-Fold** | Mantener proporción clases | Clases desbalanceadas |
| **Time Series Split** | No mezclar temporal | Series temporales |

---

## 🚫 Problemas Comunes

| Problema | Causa | Solución |
|:---------|:------|:---------|
| **Overfitting** | Modelo memoriza training | Regularization, más datos, dropout |
| **Underfitting** | Modelo muy simple | Más features, modelo más complejo |
| **Data Leakage** | Info de test en training | Validar splits, feature engineering post-split |
| **Imbalanced Classes** | 99% clase A, 1% clase B | Oversampling (SMOTE), class weights |
| **Concept Drift** | Distribución cambia en prod | Retraining periódico, monitoring |

---

## 🔐 Ética y Fairness

| Aspecto | What | Cómo mitigar |
|:--------|:-----|:-------------|
| **Bias** | Modelo discrimina grupos | Auditar datasets, fairness metrics |
| **Privacy** | Datos sensibles | Differential privacy, federated learning |
| **Explainability** | Black-box decisions | SHAP, LIME, feature importance |
| **Transparency** | Comunicar limitaciones | Documentar asunciones, model cards |

**Herramientas:** [SHAP](https://shap.readthedocs.io/), [LIME](https://github.com/marcotcr/lime), [Fairlearn](https://fairlearn.org/)

---

## 📚 Recursos

- [fast.ai](https://www.fast.ai/)
- [Deep Learning Book - Goodfellow](https://www.deeplearningbook.org/)
- [Kaggle Learn](https://www.kaggle.com/learn)
- [Papers with Code](https://paperswithcode.com/)
- [Hugging Face Course](https://huggingface.co/learn)

---

[⬅️ Anterior: Optimización de Costos](./19-cost-optimization.md) | [⬆️ Volver arriba](#20-machine-learning-y-deep-learning) | [➡️ Siguiente: Ciencia de Datos](./21-ciencia-datos.md)
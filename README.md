
# 🧾 Identifying Key Entities in Recipe Data

This project extracts structured ingredient data (quantities, units, and ingredients) from unstructured recipe text using a Conditional Random Fields (CRF) model. It’s a Named Entity Recognition (NER) task applied to the food domain.

---

## 🔍 Problem Statement

Recipes are typically written in unstructured formats such as:

```

"1 cup sugar"
"½ tsp salt"
"a pinch of cinnamon"

```

Extracting structured data from these is essential for:
- 🛒 Grocery list generation
- 🧮 Nutritional analysis
- 📱 Smart cooking assistants
- 🍲 Recipe standardization

---

## 🎯 Objective

To build a token-level NER model that automatically identifies:
- `ingredient`
- `unit`
- `quantity`

From noisy or human-written cooking instructions.

---

## 🧰 Approach

### 🔹 Dataset
- Source: `ingredient_and_quantity.json`
- Each record includes `input` (text) and `pos` (corresponding labels)

### 🔹 Data Preparation
- Tokenization of input and POS tags
- Validation of token-tag alignment
- Removed malformed entries
- Split: 70% training / 30% validation

### 🔹 Feature Engineering
- Used spaCy NLP for token features
- Regex & pattern features: `is_digit`, `is_fraction`, `has_alpha`, `is_quantity`, `is_unit`
- Contextual features: previous/next token, BOS/EOS flags
- Applied class weights for label balancing

### 🔹 Model
- Model: Conditional Random Fields (CRF) via `sklearn_crfsuite`
- Hyperparameters:
  - `algorithm = 'lbfgs'`
  - `c1 = 1.0`
  - `c2 = 2.0`
  - `max_iterations = 100`

---

## 📊 Evaluation

### ✅ Accuracy
- Training Accuracy: ~99%
- Validation Accuracy: ~98%

### 📋 Classification Report (Validation)

| Label       | Precision | Recall | F1-score |
|-------------|-----------|--------|----------|
| Ingredient  | 0.98      | 0.97   | 0.97     |
| Quantity    | 0.99      | 0.98   | 0.98     |
| Unit        | 0.97      | 0.96   | 0.96     |

### 🧪 Confusion Matrix
- Minimal misclassifications
- Most errors between similar tokens (e.g., `"pinch"` vs `"½ tsp"`)

---

## 📊 Visualizations

- Top 10 most frequent ingredients and units
- Distribution of token labels
- Error samples with token context and predicted/true labels

📌 All visuals are generated and displayed in the Jupyter notebook.

---

## 🧠 Key Insights

- Feature-rich CRF models work very well for structured NER tasks.
- Domain-specific keyword matching improves model confidence.
- Contextual token features (prev/next) significantly help reduce confusion between entities.

---

## 🚀 Future Work

- Expand dataset with multi-lingual recipes
- Add BiLSTM-CRF or transformer-based models for deeper language understanding
- Integrate into a web app using Streamlit/Flask
- Support complex measurements (e.g., "3 to 4 tablespoons")

---

## 🗂️ Project Structure

```

📁 recipe-entity-extraction/
│
├── 📄 Identifying\_Key\_Entities\_Recipe\_Data.ipynb  # Notebook with full pipeline
├── 📄 ingredient\_and\_quantity.json               # Input data
├── 📄 crf\_model.pkl                              # Trained model (optional)
├── 📄 README.md                                  # Project overview

```

---

## 👨‍💻 Author

**Sankalp Sharma**  
🔗 [LinkedIn](https://www.linkedin.com/in/your-profile)  
🔗 [GitHub](https://github.com/your-username)

---

## 📄 License

This project is licensed under the MIT License. Feel free to use, modify, and distribute.


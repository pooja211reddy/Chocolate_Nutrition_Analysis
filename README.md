# 🍫 Chocolate Product Data Analysis — Power BI & SQL Dashboard

A complete **data analysis and visualization project** exploring the nutritional composition of chocolate and related products using **Python (Pandas, SQLAlchemy, MySQL)** and **Power BI**.  
This project performs **data cleaning**, **feature engineering**, and **exploratory data analysis (EDA)** to uncover insights into product health metrics, brand behavior, and nutritional classifications.

---

## 📘 Project Overview
This project aims to:
- Clean and preprocess a real-world chocolate product dataset.
- Analyze nutritional data (energy, sugar, fat, carbohydrates, sodium, etc.).
- Derive meaningful metrics such as calorie and sugar categories.
- Visualize brand and nutrition insights interactively in **Power BI**.
- Build SQL queries for trend analysis and aggregation.

---

## 🧩 Tech Stack
| Category | Tools Used |
|-----------|-------------|
| **Programming Language** | Python (Pandas, NumPy, Matplotlib, Seaborn) |
| **Database** | MySQL (via SQLAlchemy + PyMySQL) |
| **Data Visualization** | Power BI |
| **Data Cleaning** | Pandas, Regex, Unicode Normalization |
| **Version Control** | Git & GitHub |

---

## 🧹 Data Cleaning & Preprocessing
The dataset included inconsistencies such as:
- Mixed-language text (French, German, etc.)
- Unicode encoding issues (`√©`, `ŸÉ` etc.)
- Brand name variations (e.g., *Sainsbury's*, *Sainsburys*, *By Sainsbury's*)
- Missing or malformed product codes
- Scientific notation in product codes (`6.11E+12`)
- Null or inconsistent nutrition fields

### ✅ Key Cleaning Steps
- Removed prefix numbers from product names.  
- Standardized and padded product codes (e.g., `0006111035000430`).  
- Normalized brand names (e.g., all variants → `Sainsbury's`).  
- Replaced `NaN` and infinite values with appropriate defaults.  
- Translated or normalized non-English brand names.  
- Derived additional features like:
  - `sugar_to_carb_ratio`
  - `calorie_category` (Low / Moderate / High)
  - `sugar_category` (Low / Moderate / High)
  - `is_ultra_processed` (based on NOVA group classification)

---

## 🧮 SQL Integration

All cleaned data was uploaded to **MySQL** under three tables:
1. **`product_info`** → Product name, brand, and code  
2. **`nutrient_info`** → Nutritional attributes per 100g  
3. **`derived_metrics`** → Computed categories and ratios  

### 🔍 Example Queries
```sql
-- Count products per brand
SELECT brand, COUNT(*) AS product_count
FROM product_info
GROUP BY brand;

-- Top 10 products by energy value
SELECT product_name, energy_kcal_value
FROM nutrient_info
ORDER BY energy_kcal_value DESC
LIMIT 10;

-- Average sugar_to_carb_ratio for High Calorie products
SELECT ROUND(AVG(sugar_to_carb_ratio), 3)
FROM derived_metrics
WHERE calorie_category = 'High';
```

---

## 📊 Power BI Dashboard

An interactive **Power BI dashboard** was built to visualize:
- Product distribution by calorie and sugar category  
- NOVA group proportions (pie chart)  
- Top brands by product count  
- Sugar-to-carb ratio distribution  
- Ultra-processed vs. minimally processed food ratios  
- Relationships between energy and sugar values  

### 📈 Visual Components
- **Bar charts** → Products per calorie/sugar category  
- **Pie chart** → NOVA group proportion  
- **Histogram** → Energy & sugar distribution  
- **Box plot** → Calories per brand  
- **Scatter plot** → Energy vs. Sugar correlation  
- **Heatmap** → Correlation among nutritional features  

---

## 🧠 Key Insights
- Several brands (e.g., *Sainsbury’s*, *Favorina*) had duplicate or inconsistent labeling.  
- A noticeable proportion of products are classified as **Ultra-Processed (NOVA 4)**.  
- Products high in calories often showed strong correlation with higher sugar ratios.  
- Certain brands produce both low- and high-calorie ranges across categories.  
- Sodium and fat levels varied significantly across similar product lines.  

---

## 📂 Repository Structure
```
chocolate-analysis/
│
├── data/
│   └── cleaned_product_info.csv
│
├── notebooks/
│   └── chocolate_data_cleaning.ipynb
│
├── sql/
│   └── analysis_queries.sql
│
├── dashboard/
│   └── chocolate_dashboard.pbix
│
├── visuals/
│   └── dashboard_preview.png
│
├── requirements.txt
└── README.md
```

---

## ⚙️ How to Run Locally
1. Clone the repository:
   ```bash
   git clone https://github.com/yourusername/chocolate-data-analysis.git
   cd chocolate-data-analysis
   ```
2. Install dependencies:
   ```bash
   pip install -r requirements.txt
   ```
3. Run the Jupyter Notebook:
   ```bash
   jupyter notebook notebooks/chocolate_data_cleaning.ipynb
   ```
4. Set up the MySQL database using scripts in `/sql/`.
5. Open the Power BI file (`.pbix`) and connect it to your MySQL database.

---

## 🧭 Future Enhancements
- Automate ETL pipeline for daily product updates.  
- Deploy dashboard to Power BI Service for online access.  
- Add advanced nutritional scoring using machine learning.  
- Integrate data from additional product categories.  

---

## 🧑‍💻 Author
**[Your Name]**  
Data Analyst | Python | SQL | Power BI  
📧 your.email@example.com  
🔗 [LinkedIn Profile](https://www.linkedin.com/in/yourprofile)

---

## 🪪 License
This project is licensed under the MIT License — feel free to use and modify with attribution.

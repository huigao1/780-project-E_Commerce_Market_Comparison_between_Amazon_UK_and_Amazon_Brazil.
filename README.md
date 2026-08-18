## E-Commerce Market Comparison: Amazon UK vs. Amazon Brazil

A cross-market e-commerce analytics project comparing product demand, pricing, customer engagement, category performance, and consumer behavior on Amazon UK and Amazon Brazil.

## Project Overview

Expanding an e-commerce business into a new country requires more than applying the same product and pricing strategy everywhere. Differences in purchasing power, category preferences, review behavior, language, and price sensitivity can substantially change how a product performs.

This project analyzes millions of Amazon listings from the UK and Brazil to help sellers localize their product selection, pricing, marketing, and recommendation strategies. It combines exploratory analysis, clustering, predictive modeling, Google Trends, product similarity, and generative AI.

## Business Questions

- How do pricing and consumer engagement differ between the UK and Brazil?
- Do best-selling products receive more reviews or higher ratings?
- Which categories offer the strongest market opportunities in each country?
- How does the same product perform across markets?
- Which products can support moderate price increases without losing substantial demand?
- Can product data support localized titles and product recommendations?

## Data

The project uses product listings scraped in 2023:

| Market | Original scale | Processed scale | Source |
| --- | ---: | ---: | --- |
| Amazon UK | 2.2M products | 1.05M products | [Kaggle](https://www.kaggle.com/datasets/asaniczkaamazon-uk-products-dataset-2023) |
| Amazon Brazil | 1.3M products | 387K products | [Kaggle](https://www.kaggle.com/datasets/asaniczka/amazon-brazil-products-2023-1-3m-products) |

Key fields include:

- ASIN and product title
- Product category
- Price and list price
- Star rating and review count
- Best-seller status
- Estimated purchases in the previous month, when available

## Data Preparation

- Translated Portuguese titles and category names with Google Cloud Translation
- Converted Brazilian real and British pound prices into U.S. dollars using September 27, 2024 exchange rates
- Removed unreliable image URLs and unclear or unusable fields
- Removed 19,664 Brazilian listings with a zero price because they were likely unavailable for sale
- Preserved products with zero ratings or reviews to retain less-popular listings
- Used ASIN to match identical products across countries
- Standardized similar category names across languages for direct comparisons

## Analytical Workflow

1. Compared prices, ratings, reviews, and best-seller status
2. Measured relationships between price and customer engagement
3. Matched products by ASIN for cross-country performance analysis
4. Compared category-level best-seller counts and rates
5. Integrated Google Trends to assess external search interest
6. Clustered products by price, reviews, ratings, and demand
7. Simulated dynamic pricing scenarios for high-demand clusters
8. Built a Random Forest demand model and analyzed feature importance
9. Created a market-specific trendy-title generator with GPT-4o
10. Built a cosine-similarity product recommendation system

## Key Findings

### Ratings and reviews

- Ratings in both markets were concentrated between 4.0 and 5.0 stars.
- Products with more reviews generally had higher ratings, although the relationship was nonlinear.
- Higher-priced products tended to receive fewer reviews in both markets.
- The negative price-review relationship was stronger in the UK, suggesting greater caution around expensive purchases.
- Brazilian customers showed comparatively more engagement with premium products.

### Cross-market product performance

- Identical products generally received similar star ratings in both countries.
- Review counts often differed substantially, with many products receiving more reviews in the UK.
- Products and categories with large cross-market differences require localized marketing, while consistently performing categories may support a more standardized strategy.

### Category preferences

**Amazon UK**

- Strong categories included Health & Personal Care, specialized tools, medical supplies, and recreational products.
- Sports, outdoor, arts, crafts, and DIY categories showed opportunities for broader premium offerings.
- UK customers had access to more affordable alternatives and appeared more value-conscious.

**Amazon Brazil**

- Strong categories included language-learning products, fashion, electronics, home entertainment, and religion and spirituality.
- Electronics demonstrated substantial consumer interest and a broad range from budget to premium products.
- Premium products could attract meaningful engagement, particularly when supported by brand loyalty or product necessity.

### Clustering and dynamic pricing

- Low-price, high-demand products formed a small but valuable opportunity cluster in both markets.
- The Brazilian high-demand cluster appeared less price-sensitive than its UK counterpart.
- Scenario analysis suggested that a **15% price increase** could maximize revenue if demand decreased by only about 2%.
- Moderate increases should be tested carefully rather than applied to every product.

### Demand drivers

A Random Forest model was used to predict estimated purchases in the previous month. The model achieved an R² of approximately **0.30**, indicating that the available listing data explained some, but not all, variation in demand.

The most influential features were:

| Feature | Importance |
| --- | ---: |
| Reviews | 0.36 |
| Price | 0.18 |
| Star rating | 0.07 |
| List price | 0.06 |
| Discount percentage | 0.05 |

Customer-generated content and price were more informative than discounts alone. High discount rates did not consistently produce more purchases or reviews.

## Seller Recommendations

- Use localized product and pricing strategies instead of treating both markets identically.
- Expand premium electronics selectively in Brazil while maintaining value-oriented entry options.
- Target sports, outdoor, and DIY customers with broader premium ranges in the UK.
- Encourage authentic customer reviews because review volume is a strong indicator of visibility and demand.
- Test moderate price increases on low-price, high-demand products before broader implementation.
- Do not rely on large discounts alone; product quality, positioning, category fit, and marketing remain important.
- Use ASIN-level comparisons to identify products that require country-specific messaging.

## Trendy Product Title Generator

The project calculates a custom trendy score using:

- Purchases in the previous month: 40%
- Star rating: 30%
- Best-seller status: 20%
- Review count: 10%

Products above the selected threshold were used as market-specific examples for GPT-4o. A user can provide a product description, select Brazil or the UK, and generate a title informed by successful listings in that market. Brazilian results can also be translated into English.

## Product Recommendation System

A content-based recommendation system uses standardized product-category features and cosine similarity to return related ASINs. This supports product discovery, assortment planning, and cross-selling opportunities.

## Technology

`Python` `Pandas` `NumPy` `scikit-learn` `Random Forest` `K-Means` `Cosine Similarity` `Matplotlib` `Seaborn` `Google Trends` `Google Cloud Translation` `OpenAI API` `Jupyter Notebook`


## Limitations

- Review count was used as a proxy for popularity when direct sales data was unavailable.
- The available `boughtInLastMonth` field did not have a fully documented collection period and was unavailable for parts of the analysis.
- Differences in language and category naming required manual mapping for some comparisons.
- Translation and full-dataset processing were computationally expensive.
- The demand model's moderate R² suggests that inventory, advertising, competition, seasonality, and other omitted factors also influence sales.
- Dynamic pricing findings are scenario-based and should be validated through controlled market tests.

## Project Context

This project was completed for **BA780** in 2024. It demonstrates large-scale data preparation, international market analysis, unsupervised learning, predictive modeling, recommendation systems, and applied generative AI for e-commerce strategy.


# StockRescue — AI-Powered B2B Inventory Rescue Platform

StockRescue is an AI-powered B2B platform designed to help businesses identify, manage, and rescue surplus or at-risk inventory by connecting sellers with potential buyers.

The platform uses inventory analytics, demand forecasting, risk scoring, and AI-based buyer matching to help businesses make better decisions about excess, slow-moving, and near-expiry stock.

---

## 🚀 Project Overview

Businesses often have inventory that becomes difficult to sell because of:

* Overstocking
* Slow sales
* Product expiry
* Changing demand
* Stale inventory
* Price mismatch
* Lack of suitable buyers

StockRescue addresses this problem by analyzing inventory data and connecting businesses that have surplus stock with businesses that need those products.

### Main Workflow

```text
Business Owner
      ↓
Upload Inventory / Manage Stock
      ↓
Inventory & Sales Analysis
      ↓
AI Risk Scoring
      ↓
Identify At-Risk Inventory
      ↓
Buyer Matching
      ↓
Marketplace / Buyer Enquiries
      ↓
Recommended Action
```

---

## 🎯 Key Features

### 1. Seller Dashboard

Business owners can:

* View inventory
* Monitor important KPIs
* Upload inventory through CSV
* Preview uploaded data
* View at-risk products
* Manage marketplace listings
* View potential buyer matches

### 2. Buyer Portal

Buyers can:

* Add their product requirements
* Browse available listings
* View suggested products
* Find suitable sellers
* Send enquiries
* View match-score explanations

### 3. Inventory Management

The system manages:

* Products
* Batch-level inventory
* Expiry dates
* Sales records
* Stock quantities

CSV upload is supported with column mapping and preview.

### 4. AI-Based Risk Scoring

Inventory is assigned a score from **0–100** based on factors such as:

* Overstock
* Inventory staleness
* Expiry risk
* Sales trends

Products are classified into:

```text
Healthy
Watch
Excess
Dead
```

The system also provides reason codes explaining why an item is considered at risk.

### 5. Demand Forecasting

StockRescue uses historical sales information to estimate future demand.

The system uses:

* Historical sales
* Rolling windows
* Average daily sales
* Days of inventory cover
* Product-level trends

The demand forecasting model uses a **HistGradientBoosting Regressor**.

A 7-day moving average can be used as a cold-start approach when sufficient historical data is unavailable.

### 6. AI Buyer Matching

The platform matches available inventory with buyer requirements.

The matching system considers:

| Factor          | Weight |
| --------------- | -----: |
| Text similarity |    40% |
| Category        |    20% |
| Quantity fit    |    15% |
| Distance        |    15% |
| Price           |    10% |

The system uses **MiniLM embeddings** and cosine similarity for text-based matching.

### 7. Action Recommendations

Based on inventory risk and available buyer matches, StockRescue can recommend actions such as:

* Offer stock to potential buyers
* List products on the marketplace
* Apply a local discount
* Liquidate inventory
* Hold inventory
* Suggest a discount percentage

---

## 🏗️ System Architecture

The project follows a simple architecture with:

```text
React Frontend
       │
       │ HTTPS + JWT
       ↓
FastAPI Backend
       │
       ├── Authentication & RBAC
       ├── Inventory & Sales API
       ├── Analytics API
       ├── Marketplace API
       │
       └── In-process ML Engine
                │
                ├── Feature Builder
                ├── Demand Forecasting
                ├── Risk Scoring
                └── Buyer Matching
                       │
                       ↓
                 PostgreSQL
```

### Architecture Components

#### Frontend

* React 18
* Vite
* Tailwind CSS
* Recharts
* Vercel

#### Backend

* FastAPI
* Uvicorn
* SQLAlchemy
* Pydantic
* Render

#### Database

PostgreSQL hosted using:

* Neon or
* Supabase

#### AI / ML

* Python
* Scikit-learn
* Sentence Transformers
* MiniLM
* CPU-based processing

---


## ⏰ Automated Processing

The platform includes a scheduler for automatic ML processing.

The scheduler can periodically recompute:

```text
Feature Engineering
       ↓
Demand Forecast
       ↓
Risk Score
       ↓
Recommended Actions
```

The system also supports on-demand matching through:

```text
POST /matching/run
```

New marketplace listings or buyer needs can trigger matching for the relevant records.

---



## 📁 Suggested Project Structure

```text
StockRescue/
│
├── frontend/
│   ├── src/
│   ├── public/
│   ├── package.json
│   └── vite.config.js
│
├── backend/
│   ├── app/
│   │   ├── api/
│   │   ├── models/
│   │   ├── schemas/
│   │   ├── services/
│   │   ├── ml/
│   │   └── main.py
│   │
│   ├── requirements.txt
│   └── README.md
│
├── docs/
│   └── architecture.svg
│
└── README.md
```

---


---

## 💡 Why StockRescue?

Traditional inventory systems mainly show businesses **what stock they have**.

StockRescue focuses on helping businesses understand:

```text
What stock is at risk?
        ↓
Why is it at risk?
        ↓
How much demand is expected?
        ↓
Which buyers may need it?
        ↓
What action should the business take?
```

This makes the platform focused on **inventory rescue and B2B matching**, rather than only inventory tracking.

---



---

## 🔄 Overall System Flow

```text
                    ┌───────────────────┐
                    │  Business Owner   │
                    └─────────┬─────────┘
                              │
                              ↓
                    ┌───────────────────┐
                    │ Seller Dashboard  │
                    └─────────┬─────────┘
                              │
                              ↓
                    ┌───────────────────┐
                    │ Inventory & Sales │
                    └─────────┬─────────┘
                              │
                              ↓
                    ┌───────────────────┐
                    │ Feature Builder   │
                    └─────────┬─────────┘
                              │
                    ┌─────────┴─────────┐
                    ↓                   ↓
             Demand Forecast       Risk Scoring
                    │                   │
                    └─────────┬─────────┘
                              ↓
                    ┌───────────────────┐
                    │ Buyer Matching    │
                    └─────────┬─────────┘
                              │
                              ↓
                    ┌───────────────────┐
                    │ Recommendations   │
                    └─────────┬─────────┘
                              │
                              ↓
                    ┌───────────────────┐
                    │   B2B Marketplace │
                    └─────────┬─────────┘
                              │
                              ↓
                    ┌───────────────────┐
                    │   Business Buyer  │
                    └───────────────────┘
```

---

## 📌 Project Goals

The main goals of StockRescue are to:

1. Detect surplus and at-risk inventory.
2. Estimate future product demand.
3. Explain inventory risk using understandable factors.
4. Match surplus inventory with potential buyers.
5. Provide actionable recommendations.
6. Create a simple B2B marketplace for inventory rescue.
7. Reduce inventory waste and improve stock utilization.

---

## 📜 License

This project is developed for academic/educational purposes.

---

## 👩‍💻 Project

**StockRescue — AI-Powered B2B Inventory Rescue Platform**



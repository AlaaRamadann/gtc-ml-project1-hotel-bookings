# 🏨 GTC ML Project 1 - Data Cleaning & Preprocessing Challenge

## 📌 Objective
The goal of this project is **not** to build a final model, but to **prepare raw hotel booking data** for a future **cancellation prediction model**.  
High-quality data preprocessing is critical for ensuring that the future model can learn effectively without being biased by data issues.

---

## 📊 Business Problem
The **Revenue Team** identified that **last-minute cancellations** severely impact profitability.  
This project focuses on **cleaning, preprocessing, and feature engineering** the raw data to make it **machine-learning ready**.

---

## 🚀 Project Workflow

### **Phase 1: Exploratory Data Analysis (EDA) & Data Quality Report**
- Loaded dataset (`hotel_bookings.csv`) and generated:
  - `.describe()`
  - `.info()`
- Identified **missing values** and visualized them using:
  - Heatmap (`seaborn`)
- Detected **outliers** in key numerical columns (`adr`, `lead_time`, etc.) using:
  - **Boxplots**
  - **IQR method**
- **Findings:**
  - Many missing values in `company`, `agent`, `country`, `children`.
  - Extreme outliers in `adr` (values > 5000) and `lead_time` (> 300 days).
  - Duplicated rows were detected.

---

### **Phase 2: Data Cleaning (Core of the Project)**
- **Handling Missing Values**
  - `company`, `agent` → replaced with **0**.
  - `country` → imputed with  **"Unknown"**.
  - `children` → imputed with **mode**.
- **Duplicates**
  - Removed **exact duplicate rows**.
- **Outliers**
  - Capped `adr` at **1000** to reduce skew.
  - Similar treatment for `lead_time` and `days_in_waiting_list`.
- **Data Types**
  - Converted date-related columns to **datetime** format.
  - Converted children column to integer.

---

### **Phase 3: Feature Engineering & Preprocessing**
- **New Features**
  - `total_guests = adults + children + babies`
  - `total_nights = stays_in_weekend_nights + stays_in_week_nights`
  - `is_family` = binary flag (`Yes`/`No`) if booking includes children or babies.
- **Encoding Categorical Variables**
  - Low-cardinality (nominal categories) → **One-Hot Encoding** (e.g., `meal`, `market_segment`).
  - Multiple Categories → **Frequency Encoding** (e.g., `country`).
  - Label Encoder  → Ordinal Categories (e.g, reserved_room_type, assigned_room_type).
  - Mapping month as numbers instead of string
- **Critical Step:**
  - Dropped `reservation_status` and `reservation_status_date` to prevent **data leakage**.
- **Final Preparation**
  - Split dataset into **train (80%)** and **test (20%)** with `random_state=42`.

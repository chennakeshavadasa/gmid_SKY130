
# **gmid_SKY130**  
This repository contains **GM/ID extraction data** and related Interactive scripts to get started with gm/id based design using the **SKY130 PDK**. It enables users to perform circuit simulations, extract key transistor parameters, and generate insightful plots quickly and efficiently.  

🔗 **Interactive gm/ID tool:** Explore this data in the browser — no install needed — at **[nithinpuru.github.io/gmid/sky130a](https://nithinpuru.github.io/gmid/sky130a/)** (part of the [gm/ID Explorer](https://nithinpuru.github.io/gmid/) for SKY130A, GF180MCU-D and IHP SG13G2).

---

## **Installation**

1. **Clone the repository**:  
   ```bash
   git clone https://github.com/chennakeshavadasa/gmid_SKY130.git
   ```

2. **Navigate into the cloned directory**:  
   ```bash
   cd gmid_SKY130
   ```

3. **Install dependencies**:  
   ```bash
   pip install matplotlib numpy pandas
   ```
4. **Define the File Path in python Scripts**:
    For Example,
   ```
   path = r"C:\Users\USERNAME\Downloads\SKY130\nfet3_01v8_lvt\\"

   ```   

---

## **Quick Start**

1. **Run the GM/ID scripts**:  
   Use the following command to generate the plots:  
   ```bash
   python gmid Python Scipts/gmid_python scripts/sky130/NMOS-LVT.py
   ```

2. **View the data**:  
   Check the `gmid Data/` folder for extracted GM/ID values and plots.

---

## **Usage**
1. **To run a specific extraction**:  
   Run the `NMOS-LVT.py` script for example and execute:  
   ```bash
   python gmid Python Scipts/gmid_python scripts/sky130/NMOS-LVT.py
   ```

---


- Special Thanks to [**Soumya Kanta Rana**](https://www.linkedin.com/in/soumya-rana/) for the Test Bench.

---

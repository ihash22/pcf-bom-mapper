# pcf-bom-mapper

# AI-Assisted PCF BOM Mapper
**Status:** 🚧 In Active Development (Architecture Phase)

## The Problem
To calculate a Product Carbon Footprint (PCF), sustainability analysts must map every raw material in a product's Bill of Materials (BOM) to a Lifecycle Assessment (LCA) database (like Ecoinvent or the EPA). This is a complex semantic matching problem. A BOM might list a part as "3mm raw unbleached cotton fabric," but the database requires it to match "Textile, woven cotton, at plant/GLO." Manual mapping is a massive operational bottleneck for hardware and retail enterprises.

## The Solution
An intelligent mapping agent that automatically translates fuzzy, human-written product material text from a CSV BOM into rigid LCA emission factor nomenclature. By leveraging semantic search (vector embeddings) and an LLM validation step, this tool automates the PCF calculation process, outputting a clear, audit-ready footprint breakdown.

## Proposed Architecture & Tech Stack
* **Frontend UI:** `Streamlit` (for rapid, interactive CSV upload and visualization)
* **Data Processing:** `Python`, `Pandas`
* **Semantic Search / Embeddings:** `HuggingFace (sentence-transformers)` or `OpenAI Embeddings`
* **Vector Store:** `ChromaDB` or `FAISS` (to index the mock LCA database)
* **LLM Validator:** `OpenAI API (GPT-4o-mini)` 

## System Data Flow
1. **Database Indexing:** A mock database of standard emission factors is embedded into a vector space (ChromaDB).
2. **User Input:** The user uploads a standard BOM CSV via the Streamlit interface (Columns: `Part Name`, `Material Description`, `Weight (kg)`).
3. **Semantic Matching:** For each row in the BOM, the system generates an embedding for the `Material Description` and performs a cosine similarity search against the vector database to find the top 3 closest emission factors.
4. **LLM Validation (The "Agent" Step):** The LLM acts as an automated sustainability analyst. It looks at the BOM description and the top 3 matches, selecting the most scientifically accurate factor based on LCA principles.
5. **Calculation:** The script multiplies the `Weight (kg)` by the selected `Emission Factor (kgCO2e/kg)`.
6. **Visualization:** Streamlit generates a dynamic pie chart showing the carbon hotspots of the product and an exportable, audit-ready CSV mapping ledger.

## Project Roadmap
- [x] Phase 1: System architecture and UI wireframing.
- [ ] Phase 2: Create the mock BOM and mock LCA emission factor datasets.
- [ ] Phase 3: Set up FAISS/ChromaDB and generate initial vector embeddings.
- [ ] Phase 4: Build the LLM validation prompt and Pandas calculation logic.
- [ ] Phase 5: Develop the Streamlit dashboard and deploy to Streamlit Community Cloud.

---
*Developed by [Ian Hash](https://ianhash.com)

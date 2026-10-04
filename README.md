# Maldives Islands & Resorts Dataset

This repository provides a clean, open, and machine-readable dataset of the islands, resorts, and administrative atolls of the Republic of Maldives. 

Finding reliable, structured geographical and administrative data for the Maldives with standardized Thaana (Dhivehi) script, English romanization, geographic coordinates, cadastral land area, operational ministry allocations, and tourism facility registrations is often challenging due to records being scattered across historical print publications and government portals. The goal of publishing this dataset is to eliminate that friction, making accurate, baseline data freely accessible for developers, researchers, spatial analysts, and anyone building projects, tools, or applications related to the Maldives.

---

## Repository Structure

```text
maldives-islands-dataset/
│
├── 📂 Master Datasets (Root Level — Primary Deliverables)
│   ├── maldives_islands_master.csv      # Complete 1,577 records unified master
│   ├── inhabited_islands_master.csv     # 188 council & city inhabited islands (2026 LGA standard)
│   ├── resorts_master.csv               # 373 operational & proposed resort islands (177 verified MoT operating)
│   └── uninhabited_islands_master.csv   # 1,016 uninhabited, industrial & sandbanks
│
├── 📂 reference/ (Source Gazetteers, Historical Surveys & External Registries)
│   ├── mot_resorts_oct_2026.csv         # Ministry of Tourism registered facilities (Oct 2026, 177 operating)
│   ├── lga_councils_2026.csv            # Cleaned 183 LGA council registry (2026)
│   ├── onemap_islands_2021.csv          # MLSA OneMap cadastral GIS dataset (2021)
│   ├── islands_index_2008.csv           # Official Atlas digitized gazetteer (2008)
│   ├── resorts_by_trade_name.csv        # Atlas commercial resort brand directory (2008)
│   └── atoll_names.csv                  # 21 administrative atolls, capitals & letters
│
└── 📂 scripts/                          # Ingestion, OCR parsing, and merge pipelines
```

---

## Quick Access to Datasets

### Master Datasets (Root)

| Dataset | File | Year | Records | Description |
| :--- | :--- | :--- | :--- | :--- |
| **Inhabited Islands Master** | [`inhabited_islands_master.csv`](inhabited_islands_master.csv) | **2026** | **188** | **Authoritative Inhabited Registry.** Islands strictly governed by Island and City Councils. Harmonized to 2026 LGA official spellings, with council names, council types, capital status, land area, and Decimal Degree coordinates. |
| **Resorts Master** | [`resorts_master.csv`](resorts_master.csv) | **2026/2021** | **373** | **Dedicated Resorts Directory.** All operational tourist resorts (**177 verified operating** from Ministry of Tourism, Oct 2026) and proposed pipeline developments with commercial trade names, operating status, land area, and Decimal Degree coordinates. |
| **Uninhabited Islands Master** | [`uninhabited_islands_master.csv`](uninhabited_islands_master.csv) | **2021** | **1,016** | **Uninhabited & Sandbanks Registry.** Agricultural leases, industrial islands (e.g. Thilafushi), institutional islands, sandbanks, and reefs, with categories, land area, and Decimal Degree coordinates. |
| **Unified Master Dataset** | [`maldives_islands_master.csv`](maldives_islands_master.csv) | **2026** | **1,577** | **All-in-One Master.** Complete flat master dataset combining MLSA OneMap, 2026 LGA Councils, and 2026 Ministry of Tourism operational data into a unified modern GIS schema. |

### Reference & Source Datasets (`reference/`)

| Dataset | File | Year | Records | Description |
| :--- | :--- | :--- | :--- | :--- |
| **MoT Registered Resorts** | [`reference/mot_resorts_oct_2026.csv`](reference/mot_resorts_oct_2026.csv) | **2026 (Oct)** | **177** | Official registered operational facilities directory from the Ministry of Tourism. Filtered to geographical resort identifiers (`Name`, `Atoll`, `Island`, `State`) with contact and capacity details removed. |
| **LGA Councils Directory** | [`reference/lga_councils_2026.csv`](reference/lga_councils_2026.csv) | **2026** | **183** | Official administrative list of all 183 Island and City Councils from the Local Government Authority (LGA). Stripped of personal data. |
| **OneMap MLSA Dataset** | [`reference/onemap_islands_2021.csv`](reference/onemap_islands_2021.csv) | **2021** | **1,560** | Direct public cadastral GIS dataset from the Maldives Land and Survey Authority (MLSA) with official Land Feature Codes (`FCODE`). |
| **Atlas Island Index** | [`reference/islands_index_2008.csv`](reference/islands_index_2008.csv) | **2008** | **1,037** | Complete gazetteer of all surveyed islands from the *Official Atlas of the Maldives* with historical map grid references (`Map_Ref`), Thaana script, and linked `FCODE`. |
| **Resorts Directory (Atlas)** | [`reference/resorts_by_trade_name.csv`](reference/resorts_by_trade_name.csv) | **2008** | **98** | Historic tourist resorts cataloged by commercial brand/trade name from the Official Atlas. |
| **Atoll Names & Capitals** | [`reference/atoll_names.csv`](reference/atoll_names.csv) | **—** | **21** | Official atoll designations, English names, short names, administrative capitals, and Thaana script. |

---

## 1. Domain-Specific Master Datasets

To make analysis straightforward without requiring heavy filtering, the master data is partitioned into three domain-specific tables and one unified master table. All master datasets are streamlined to modern GIS standards (Decimal Degrees, single high-accuracy land area in hectares, and canonical names), keeping historical 2008 physical book artifacts safely in `reference/`.

### A. Inhabited Islands Master (`inhabited_islands_master.csv`)
* **Total Records:** **188 inhabited islands**
* **Scope:** Every island governed by a local government council under the Decentralization Act.
* **Modernized Names:** All island names are harmonized to the **2026 Local Government Authority (LGA)** official Latin spelling standard.
* **Administrative Groupings:**
  * **City Councils:** Malé City (Malé, Villimalé, Hulhumalé), Addu City (Hithadhoo, Maradhoo, Maradhoo-Feydhoo, Feydhoo), Fuvahmulah City, Kulhudhuffushi City, and Thinadhoo City.
  * **Island Councils:** 176 individual island councils plus the two distinct Addu constituency councils (`S. Addu Hulhudhoo Council` and `S. Addu Meedhoo Council`).
* **Columns:** `FCODE`, `Atl`, `Atoll_Name`, `Island_Name`, `Island_Dhivehi`, `Council_Name`, `Council_Type`, `Is_Capital`, `Area_Ha`, `Lat_DD`, `Lon_DD`.

### B. Resorts Master (`resorts_master.csv`)
* **Total Records:** **373 resort islands**
  * **177 Operating Resorts:** Verified against the Ministry of Tourism (MoT) October 2026 registered facilities directory. Includes current trade name, operational status (`Operating`), and geographic coordinates.
  * **196 Proposed / Pipeline Developments:** Allocated tourism islands from OneMap GIS and ministry records under planning or construction.
* **Columns Schema:**
  | Column | Type | Description | Example |
  | :--- | :--- | :--- | :--- |
  | `FCODE` | String | Official cadastral Land Feature Code (MLSA) | `LD0170`, `LD0283` |
  | `Atl` | String | Administrative Atoll code | `ADh`, `K`, `B` |
  | `Atoll_Name` | String | English popular atoll name | `Alifu Dhaalu`, `Kaafu` |
  | `Island_Name` | String | Canonical Romanized island name | `Rangaleefinolhu`, `Kohdhipparufinolhu` |
  | `Island_Dhivehi` | String | Island name in Dhivehi (Thaana script) | `ރަންގަލީފިނޮޅު` |
  | `Resort_Trade_Name` | String | Official commercial resort trade / brand name | `Conrad Maldives Rangali Island` |
  | `Operating_Status` | String | `Operating` or `Proposed / Pipeline` | `Operating`, `Proposed / Pipeline` |
  | `Area_Ha` | Float | High-precision polygon land area in hectares (MLSA GIS) | `14.84319` |
  | `Lat_DD`, `Lon_DD` | Float | Coordinates in WGS84 Decimal Degrees | `4.377503`, `73.663571` |

### C. Uninhabited Islands Master (`uninhabited_islands_master.csv`)
* **Total Records:** **1,016 islands and geographic features**
* **Scope:** Uninhabited islands, agricultural leases (`Varuva`), industrial islands (e.g. Thilafushi, Gulhifalhu, Maafilaafushi), institutional islands, sandbanks, and reefs.
* **Historical Transitions:** Islands verified as operating resorts (e.g. V. Vashugiri, Lh. Fushifaru) have been transitioned to `resorts_master.csv`.
* **Columns:** `FCODE`, `Atl`, `Atoll_Name`, `Island_Name`, `Island_Dhivehi`, `Category`, `Area_Ha`, `Lat_DD`, `Lon_DD`.

### D. Unified Master Dataset (`maldives_islands_master.csv`)
* **Total Records:** **1,577 records**
* Enriched flat dataset combining all categories above with cross-references, modern GIS land areas, Decimal Degree coordinates, administrative council metadata, and Ministry of Tourism operational resort status.
* **Columns:** `FCODE`, `Atl`, `Atoll_Name`, `Island_Name`, `Island_Dhivehi`, `Category`, `Council_Name`, `Council_Type`, `Resort_Trade_Name`, `Operating_Status`, `Is_Capital`, `Area_Ha`, `Lat_DD`, `Lon_DD`.

---

## 2. Ministry of Tourism Operating Facilities (`reference/mot_resorts_oct_2026.csv`)

Downloaded directly from the **Ministry of Tourism Registered Facilities Portal** ([https://www.tourism.gov.mv/en/registered/facilities/filter-t1](https://www.tourism.gov.mv/en/registered/facilities/filter-t1)), updated **October 2026**.

* **Total Records:** **177 operational tourist resorts**
* **Data Sanitization & RFC 4180 Compliance:**
  * Cleaned broken quotes and unescaped quote delimiters present in the portal's raw export.
  * Dropped non-geographic operational and contact columns (`Rooms`, `Beds`, `Phone`, `Fax`, `Email`, `Resort Phone`, `Resort Fax`, `Resort Email`, `Operator`, `Owner/Lesse`, `Management`) to focus strictly on geographic and island identity.
* **Fields:** `Name`, `Atoll`, `Island`, `State`.

---

## 3. 2026 LGA Councils Directory (`reference/lga_councils_2026.csv`)

Extracted and cleaned from the **2026 Local Government Authority (LGA)** councils register ([https://www.lga.gov.mv/en/councils](https://www.lga.gov.mv/en/councils)).

* **Total Councils:** **183 councils**
  * **5 City Councils:** Malé City, Addu City, Fuvammulah City, Kulhudhuffushi City, Thinadhoo City.
  * **178 Island Councils:** Standard administrative atoll councils + Addu constituency councils.
* **Privacy & Cleanliness:** Councilor personal data (names, contact numbers, political party affiliations) has been completely removed to preserve privacy and geographic utility.
* **Fields:** `Atoll`, `Council_Name`, `Council_Type`, `Island_Name`.

---

## 4. Latin Spelling Harmonization (2026 LGA Standard)

Historical datasets and older printed atlases often relied on inconsistent phonetic romanization (such as apostrophes to represent nasalization like `'b` or `'d`). The 2026 update modernizes primary `Island_Name` across inhabited records while retaining the historical names in `Island_Name_Atlas` and `Island_Name_OneMap`.

| Atoll | Historical Atlas / OneMap | 2026 LGA Official Standard | Council Name |
| :--- | :--- | :--- | :--- |
| `HA` | `Dhihdhoo` | **`Dhidhdhoo`** | `HA. Dhidhdhoo Council` |
| `HA` | `Uligamu` | **`Uligan`** | `HA. Uligan Council` |
| `HDh` | `Kurin'bee` | **`Kurinbee`** | `HDh. Kurinbee Council` |
| `Sh` | `Kan'ditheemu` | **`Kanditheemu`** | `Sh. Kanditheemu Council` |
| `Sh` | `Maaun'goodhoo` | **`Maaungoodhoo`** | `Sh. Maaungoodhoo Council` |
| `N` | `Hen'badhoo` | **`Henbadhoo`** | `N. Henbadhoo Council` |
| `N` | `Ken'dhikulhudhoo` | **`Kendhikulhudhoo`** | `N. Kendhikulhudhoo Council` |
| `R` | `An'golithitheemu` | **`Angolhitheemu`** | `R. Angolhitheemu Council` |
| `R` | `In'guraidhoo` | **`Inguraidhoo`** | `R. Inguraidhoo Council` |
| `R` | `Un'goofaaru` | **`Ungoofaaru`** | `R. Ungoofaaru Council` |
| `K` | `Hinmafushi` | **`Himmafushi`** | `K. Himmafushi Council` |
| `AA` | `Bodufulhadhoo` | **`Bodufolhudhoo`** | `AA. Bodufolhudhoo Council` |
| `ADh` | `Dhihdhoo` | **`Dhidhdhoo`** | `ADh. Dhidhdhoo Council` |
| `ADh` | `Dhan'gethi` | **`Dhangethi`** | `ADh. Dhangethi Council` |
| `ADh` | `Kun'burudhoo` | **`Kunburudhoo`** | `ADh. Kunburudhoo Council` |
| `Dh` | `Ban'didhoo` | **`Bandidhoo`** | `Dh. Bandidhoo Council` |
| `Dh` | `Maaen'boodhoo` | **`Maaenboodoo`** | `Dh. Maaenboodoo Council` |
| `Dh` | `Rin'budhoo` | **`Rinbudhoo`** | `Dh. Rinbudhoo Council` |
| `Th` | `Burunee` | **`Buruni`** | `Th. Buruni Council` |
| `Th` | `Kan'doodhoo` | **`Kandoodhoo`** | `Th. Kandoodhoo Council` |
| `Th` | `Kin'bidhoo` | **`Kinbidhoo`** | `Th. Kinbidhoo Council` |
| `L` | `Dhan'bidhoo` | **`Dhanbidhoo`** | `L. Dhanbidhoo Council` |
| `GA` | `Kan'duhulhudhoo` | **`Kanduhulhuhdoo`** | `GA. Kanduhulhuhdoo Council` |
| `GA` | `Kon'dey` | **`Kondey`** | `GA. Kondey Council` |
| `GA` | `Vilin'gili` | **`Vilingili`** | `GA. Vilingili Council` |
| `GDh` | `Hoan'dehdhoo` | **`Hoadedhdhoo`** | `GDh. Hoadedhdhoo Council` |
| `GDh` | `Nadellaa` | **`Nadella`** | `GDh. Nadella Council` |

---

## 5. Source Gazetteers & Specialized Tables (`reference/`)

### A. Main Island Index (`reference/islands_index_2008.csv`)
* **Total Records:** **1,037 islands** (from `Aarah` to `Ziyaaraiyfushi`)
* **Key Added Feature:** Includes `FCODE` column to allow 1:1 relational joins with external MLSA systems.
* **Fields:** `FCODE`, `Atl`, `Island`, `Island_Clean`, `Category`, `Area_Ha`, `Map_Ref`, `Lat`, `Lon`, `Island_Dhivehi`, `Atl_Dhivehi`.

### B. OneMap MLSA 2021 Reference (`reference/onemap_islands_2021.csv`)
* **Total Records:** **1,560 features**
* Sourced directly from the official GIS database of the Maldives Land and Survey Authority (MLSA).
* **Fields:** `FCODE`, `atoll`, `islandName`, `capital`, `islandNa_1`, `longitude`, `latitude`, `Area_ha`, `category`, `Sector`, `Usage`, `PrimAgency`.

### C. Resorts Directory by Trade Name (`reference/resorts_by_trade_name.csv`)
* **Total Records:** **98 resort entries**
* Links commercial brand names (e.g. *Adaaran Club Bathala*, *Kurumba Maldives*) to geographical island names and coordinates.

### D. Atoll Names & Administrative Subdivisions (`reference/atoll_names.csv`)
* **Total Records:** **21 entries** (20 administrative atolls + capital city Malé).
* Details administrative codes, colloquial short names, official administrative designations, and capital islands.

---

## 6. Category Code Legend

| Code | Meaning |
| :--- | :--- |
| **I** | Inhabited / Residential Island |
| **U** | Uninhabited Island |
| **R** | Operational Tourist Resort |
| **PR** | Proposed Resort / Under Development |
| **H** | City Hotel / Guest Facility |
| **IND** | Industrial Island |
| **ADE** | Domestic Airport |
| **ADF** | Future Domestic Airport |
| **AIE** | International Airport |
| **YM** | Yacht Marina |

---

## 7. Administrative Atoll Code Mapping

| Code | Atoll Name | Dhivehi Letter |
| :--- | :--- | :--- |
| `HA` | Haa Alif (Thiladhunmathi Uthuruburi) | ހއ |
| `HDh` | Haa Dhaalu (Thiladhunmathi Dhekunuburi) | ހދ |
| `Sh` | Shaviyani (Miladhunmadulu Uthuruburi) | ށ |
| `N` | Noonu (Miladhunmadulu Dhekunuburi) | ނ |
| `R` | Raa (Maalhosmadulu Uthuruburi) | ރ |
| `B` | Baa (Maalhosmadulu Dhekunuburi) | ބ |
| `Lh` | Lhaviyani (Faadhippolhu) | ޅ |
| `K` | Kaafu (Malé Atoll / Kaafu) | ކ |
| `AA` | Alif Alif (Ari Atoll Uthuruburi) | އއ |
| `ADh` | Alif Dhaal (Ari Atoll Dhekunuburi) | އދ |
| `V` | Vaavu (Felidhu Atoll) | ވ |
| `M` | Meemu (Mulakatholhu) | މ |
| `F` | Faafu (Nilandhe Atoll Uthuruburi) | ފ |
| `Dh` | Dhaalu (Nilandhe Atoll Dhekunuburi) | ދ |
| `Th` | Thaa (Kolhumadulu) | ތ |
| `L` | Laamu (Hadhdhunmathi) | ލ |
| `GA` | Gaafu Alif (Huvadhu Atoll Uthuruburi) | ގއ |
| `GDh` | Gaafu Dhaalu (Huvadhu Atoll Dhekunuburi) | ގދ |
| `GN` | Gnaviyani (Fuvahmulah) | ޏ |
| `S` | Seenu (Addu Atoll) | ސ |

---

## 8. Sources & Documentation References

This repository synthesizes data from four primary official government publications and portals:

1. **Ministry of Tourism, Republic of Maldives (October 2026)**
   * **Portal:** [https://www.tourism.gov.mv/en/registered/facilities/filter-t1](https://www.tourism.gov.mv/en/registered/facilities/filter-t1)
   * **Scope:** 2026 official register of all 177 operating tourist resorts, commercial trade names, operating status, and registered island facilities.

2. **Local Government Authority (LGA) Maldives (2026)**
   * **Portal:** [https://www.lga.gov.mv/en/councils](https://www.lga.gov.mv/en/councils)
   * **Scope:** 2026 official register of all 183 Island Councils and City Councils, active administrative divisions, and jurisdictions under the Decentralization Act.

3. **OneMap Maldives (2021)**
   * **Authority:** Maldives Land and Survey Authority (MLSA), Ministry of National Planning, Housing and Infrastructure.
   * **Dataset Portal:** [https://readme.onemap.mv/](https://readme.onemap.mv/)
   * **Raw Dataset:** [https://readme.onemap.mv/csv/IslandList_20211101.csv](https://readme.onemap.mv/csv/IslandList_20211101.csv)
   * **Scope:** Cadastral GIS database including Land Feature Codes (`FCODE`), satellite-calculated land area polygon measurements, and administrative assignments.

4. **Official Atlas of the Maldives (2008)**
   * **Publisher:** Ministry of Planning and National Development (MPND), Republic of Maldives.
   * **Scope:** Physical cadastral map survey covering surveyed permanent landmasses, atlas map plates (1–22), historical land areas, and inhabited registry.

# Maldives Islands & Resorts Dataset

This repository provides a clean, open, and machine-readable dataset of the islands, resorts, and administrative atolls of the Republic of Maldives. 

Finding reliable, structured geographical and administrative data for the Maldives with standardized Thaana (Dhivehi) script, English romanization, geographic coordinates, cadastral land area, and operational ministry allocations is often challenging due to records being scattered across historical print publications and government portals. The goal of publishing this dataset is to eliminate that friction, making accurate, baseline data freely accessible for developers, researchers, spatial analysts, and anyone building projects, tools, or applications related to the Maldives.

---

## Quick Access to Datasets

| Dataset | File | Records | Description |
| :--- | :--- | :--- | :--- |
| **Unified Master Dataset** | [`maldives_islands_master.csv`](maldives_islands_master.csv) | **1,577** | **Recommended.** Enriched flat master dataset combining the Official Atlas and MLSA OneMap. Includes `FCODE`, dual land areas, decimal degree coords (`Lat_DD`, `Lon_DD`), ministry allocations, and resort trade names. |
| **Atlas Island Index** | [`islands_index.csv`](islands_index.csv) | **1,037** | Complete gazetteer of all surveyed islands from the Official Atlas with map grid references (`Map_Ref`), Thaana script, and linked `FCODE`. |
| **OneMap MLSA Dataset** | [`onemap_islands_2021.csv`](onemap_islands_2021.csv) | **1,560** | Direct public cadastral GIS dataset from the Maldives Land and Survey Authority (MLSA) with official Land Feature Codes (`FCODE`). |
| **Resorts Directory** | [`resorts_by_trade_name.csv`](resorts_by_trade_name.csv) | **98** | Existing and proposed tourist resorts cataloged by commercial brand/trade name with island links. |
| **Atoll Names & Capitals** | [`atoll_names.csv`](atoll_names.csv) | **21** | Official atoll designations, English names, short names, administrative capitals, and Thaana script. |

---

## 1. Unified Master Dataset (`maldives_islands_master.csv`)

The unified master dataset merges the historical cadastral survey from the *Official Atlas of the Maldives* with the modern GIS survey from **OneMap** (Maldives Land and Survey Authority).

* **Total Records:** **1,577 records**
  * **1,153 Named Islands & Geographical Features**
  * **424 Unnamed Sandbanks & Reef Features** (identifiable via official `FCODE`, easily filterable via `Is_Unnamed = 'N'`)
* **Encoding:** `UTF-8 with BOM` (`utf-8-sig`) for display of Thaana (Dhivehi) script in Microsoft Excel, LibreOffice Calc, and data-related workflows.

### Columns Schema:
| Column | Type | Description | Example |
| :--- | :--- | :--- | :--- |
| `FCODE` | String | Official cadastral Land Feature Code (MLSA) | `LD1033`, `LD0268` |
| `Atl` | String | Administrative Atoll code (Latin) | `HA`, `K`, `S` |
| `Atoll_Name` | String | English popular / alphabet atoll name | `Haa Alifu`, `Kaafu` |
| `Island_Name` | String | Canonical Romanized island name | `Alidhoo`, `Malé` |
| `Island_Dhivehi` | String | Official island name in Dhivehi (Thaana script) | `އަލިދޫ`, `މާލެ` |
| `Island_Name_Atlas` | String | Island designation as printed in the Official Atlas | `Alidhoo (R)` |
| `Island_Name_OneMap` | String | Island designation as recorded in OneMap MLSA | `Alidhoo` |
| `Category_Atlas` | String | Atlas category code (`I`, `U`, `R`, `PR`, `H`, `IND`, `ADE`, `ADF`, `AIE`, `YM`) | `R`, `I, ADF, H` |
| `Category_OneMap` | String | MLSA functional categorization | `Tourism Island`, `Residential Island`, `Uninhabited Island` |
| `Sector` | String | Economic / government sector | `Tourism`, `Fisheries`, `Agriculture` |
| `Usage` | String | Specific operational usage | `Resort`, `Varuva`, `Fish Processing`, `Poultry` |
| `PrimAgency` | String | Responsible ministry or government agency | `MoT`, `MoFMRA`, `Council`, `MoECCT` |
| `Resort_Trade_Name` | String | Commercial resort trade / brand name | `Cinnamon Island Alidhoo`, `Kurumba Maldives` |
| `Is_Capital` | String | `Y` if island is an atoll capital or national capital, else `N` | `Y`, `N` |
| `Is_Unnamed` | String | `Y` for unnamed sandbanks/reefs (filter `N` for named islands only) | `N`, `Y` |
| `Area_Ha_Atlas` | String | Land area in hectares from historical Atlas | `17.2`, `<3.0` |
| `Area_Ha_GIS` | Float | High-precision polygon land area in hectares (MLSA GIS) | `14.84319` |
| `Map_Ref` | String | Map plate grid coordinate reference from Atlas (1 to 22) | `1.E5`, `18.D6` |
| `Lat_DMS` | String | Latitude in Degrees, Minutes, Seconds format | `6° 50' 56.488" N` |
| `Lon_DMS` | String | Longitude in Degrees, Minutes, Seconds format | `73° 9' 8.265" E` |
| `Lat_DD` | Float | Latitude in Decimal Degrees (WGS84, 6 decimal places) | `6.849024` |
| `Lon_DD` | Float | Longitude in Decimal Degrees (WGS84, 6 decimal places) | `73.152296` |
| `Source` | String | Data provenance: `Both` (matched in both), `Atlas`, or `OneMap` | `Both`, `Atlas`, `OneMap` |

> [!TIP]
> **GIS & Web Mapping Ready:** The fields `Lat_DD` and `Lon_DD` are pre-converted to decimal degrees, allowing instant drag-and-drop into QGIS, ArcGIS, Mapbox, Leaflet, or GeoPandas without needing DMS conversion.

---

## 2. Source Gazetteers & Specialized Tables

### A. Main Island Index (`islands_index.csv`)
* **Total Records:** **1,037 islands** (from `Aarah` to `Ziyaaraiyfushi`)
* **Key Added Feature:** Includes `FCODE` column to allow 1:1 relational joins with external MLSA systems.
* **Fields:** `FCODE`, `Atl`, `Island`, `Island_Clean`, `Category`, `Area_Ha`, `Map_Ref`, `Lat`, `Lon`, `Island_Dhivehi`, `Atl_Dhivehi`.

### B. OneMap MLSA 2021 Reference (`onemap_islands_2021.csv`)
* **Total Records:** **1,560 features**
* Sourced directly from the official GIS database of the Maldives Land and Survey Authority (MLSA).
* **Fields:** `FCODE`, `atoll`, `islandName`, `capital`, `islandNa_1`, `longitude`, `latitude`, `Area_ha`, `category`, `Sector`, `Usage`, `PrimAgency`.

### C. Resorts Directory by Trade Name (`resorts_by_trade_name.csv`)
* **Total Records:** **98 resort entries**
* Links commercial brand names (e.g. *Adaaran Club Bathala*, *Kurumba Maldives*) to geographical island names and coordinates.

### D. Atoll Names & Administrative Subdivisions (`atoll_names.csv`)
* **Total Records:** **21 entries** (20 administrative atolls + capital city Malé).
* Details administrative codes, colloquial short names, official administrative designations, and capital islands.

---

## 3. Category Code Legend

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

## 4. Administrative Atoll Code Mapping

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
| `Gn` | Gnaviyani (Fuvahmulah) | ޏ |
| `S` | Seenu (Addu Atoll) | ސ |

---

## 5. Sources & Documentation References

This repository cross-verifies and synthesizes data from two primary official government publications:

1. **Official Atlas of the Maldives (2008)**
   * **Publisher:** Ministry of Planning and National Development (MPND), Republic of Maldives.
   * **Scope:** Physical cadastral map survey covering surveyed permanent landmasses, atlas map plates (1–22), historical land areas, and inhabited registry.

2. **OneMap Maldives (2021)**
   * **Authority:** Maldives Land and Survey Authority (MLSA), Ministry of National Planning, Housing and Infrastructure.
   * **Dataset Portal:** [https://readme.onemap.mv/](https://readme.onemap.mv/)
   * **Raw Dataset:** [https://readme.onemap.mv/csv/IslandList_20211101.csv](https://readme.onemap.mv/csv/IslandList_20211101.csv)
   * **Scope:** Cadastral GIS database including Land Feature Codes (`FCODE`), satellite-calculated land area polygon measurements, and administrative assignments (Ministries of Tourism, Fisheries, Environment, and Local Councils).

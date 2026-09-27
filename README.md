# Maldives Islands & Resorts Dataset

This repository provides a clean, open, and machine-readable dataset of the islands, resorts, and administrative atolls of the Maldives. 

Finding reliable, structured geographical and administrative data for the Maldives with standardized Thaana (Dhivehi) script, English romanization, geographic coordinates, and cadastral land area is often challenging due to records remaining trapped in physical publications. The goal of publishing this dataset is to eliminate that friction, making accurate, baseline data freely accessible for developers, researchers, spatial analysts, and anyone building projects, tools, or applications related to the Maldives.

---

## Quick Access to Extracted CSVs

| Dataset | File | Records | Description |
| :--- | :--- | :--- | :--- |
| **Main Island Index** | [`islands_index.csv`](islands_index.csv) | **1,037** | Complete gazetteer of all surveyed islands with coordinates, land area, status codes, and Dhivehi names. |
| **Resorts Directory** | [`resorts_by_trade_name.csv`](resorts_by_trade_name.csv) | **98** | Existing and proposed tourist resorts cataloged by commercial brand/trade name with island links. |
| **Atoll Names & Capitals** | [`atoll_names.csv`](atoll_names.csv) | **21** | Official atoll designations, English names, short names, administrative capitals, and Thaana script. |

---

## 1. Overview of Datasets

### A. Main Island Index (`islands_index.csv`)
* **Total Records:** **1,037 islands** (from `Aarah` to `Ziyaaraiyfushi`)
* **Encoding:** `UTF-8 with BOM` (`utf-8-sig`) for native display of Thaana (Dhivehi) script in Microsoft Excel and LibreOffice Calc.

#### Columns:
| Column | Description | Example |
| :--- | :--- | :--- |
| `Atl` | Administrative Atoll code (Latin) | `HA`, `K`, `S` |
| `Island` | Full original designation with status code | `Thimarafushi (I) [ADF, H]` |
| `Island_Clean` | Island name without category tags | `Thimarafushi` |
| `Category` | Categorization code(s) | `I, ADF, H` |
| `Area_Ha` | Land area in hectares | `20.5` or `<3.0` |
| `Map_Ref` | Map plate grid coordinate reference (1 to 22) | `18.D6` |
| `Lat` | Latitude (DMS format) | `2°12'20"N` |
| `Lon` | Longitude (DMS format) | `73°08'34"E` |
| `Island_Dhivehi` | Official island name in Dhivehi (Thaana script) | `ތިމަރަފުށި` |
| `Atl_Dhivehi` | Atoll code in Thaana script | `ތ` |

---

### B. Resorts Directory by Trade Name (`resorts_by_trade_name.csv`)
* **Title:** *Existing and Proposed Resorts Listed by Trade Names*
* **Total Records:** **98 resort entries**
* **Encoding:** `UTF-8 with BOM` (`utf-8-sig`)

#### Columns:
| Column | Description | Example |
| :--- | :--- | :--- |
| `Page` | Page number in the Official Atlas | `60` |
| `Atl` | Administrative Atoll code | `K` |
| `Trade_Name` | Commercial / trade name of the resort | `Kurumba Maldives` |
| `Island_Name` | Official geographical island name | `Vihamanaafushi` |
| `Category` | Facility status code (`R`, `PR`, `YM`) | `R` |
| `Area_Ha` | Island land area in hectares | `13.7` |
| `Map_Ref` | Map grid reference | `10.D7` |
| `Lat` | Latitude | `4°13'36"N` |
| `Lon` | Longitude | `73°31'11"E` |
| `Island_Dhivehi` | Island name in Thaana script | `ވިހަމަނާފުށި` |
| `Atl_Dhivehi` | Atoll abbreviation in Thaana script | `ކ` |

---

### C. Atoll Names & Administrative Subdivisions (`atoll_names.csv`)
* **Title:** *Different Versions of Atoll Names*
* **Total Records:** **21 entries** (20 administrative atolls + capital city Malé)
* **Encoding:** `UTF-8 with BOM` (`utf-8-sig`)

#### Columns:
| Column | Description | Example |
| :--- | :--- | :--- |
| `Page` | Page number in the Official Atlas | `18` |
| `Table` | Table reference | `Table 1.2` |
| `Atl` | Administrative Atoll code | `HA`, `K`, `S` |
| `English_Name` | English descriptive name | `North Thiladhunmathi`, `Male' (capital)` |
| `Official_Name` | Official administrative atoll designation | `Thiladhunmathi Uthuruburi`, `Male'` |
| `Atoll_Short` | Popular colloquial / alphabet short name | `Haa Alifu`, `Kaafu` |
| `Capital` | Administrative capital island | `Dhihdhoo`, `Male'` |
| `Atl_Dhivehi` | Atoll abbreviation in Thaana script | `ހއ`, `ކ` |
| `Capital_Dhivehi` | Capital island name in Thaana script | `ދިއްދޫ`, `މާލެ` |
| `Official_Name_Dhivehi` | Official atoll name in Thaana script | `ތިލަދުންމަތީ އުތުރުބުރި` |
| `Notes` | Administrative classification | `Administrative Atoll`, `National Capital` |

---

## 2. Category Code Legend

| Code | Meaning |
| :--- | :--- |
| **I** | Inhabited Island |
| **U** | Uninhabited Island |
| **R** | Operational Resort |
| **PR** | Proposed Resort / Under Development |
| **H** | City Hotel |
| **IND** | Industrial Island |
| **ADE** | Domestic Airport |
| **ADF** | Future Domestic Airport |
| **AIE** | International Airport |
| **YM** | Yacht Marina |

---

## 3. Atoll Code Mapping

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

## 4. Verification & Validation Summary
* **Record Integrity:** 100% of records from the official cadastral survey have been verified and digitized.
* **Inhabited Islands:** Contains all 195 inhabited islands recognized at the time of the publication (100% match against national registries).
* **Geographical Scope:** Covers surveyed permanent landmasses; ephemeral shifting sandbanks and historically eroded/disappeared islands from previous centuries are excluded in this official cadastral atlas.

---

## 5. Source Reference
* **Original Book:** *Official Atlas of the Maldives*
* **Publisher:** Ministry of Planning and National Development (MPND), Republic of Maldives
* **Year Published:** 2008

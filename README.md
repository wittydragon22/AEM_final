# AEM 5840 Final Project: Chicago Crime Patterns and Public Safety

This repository contains a Python-based final project for **AEM 5840 Python Programming**. The project analyzes 2024 Chicago crime incidents using the City of Chicago Data Portal and supporting public safety datasets.

The main goal is to understand how crime varies by **time**, **place**, and **crime type**, then connect those findings to a simple public-safety decision-support framing.

## Research Question

How do crime incidents in Chicago vary by time, place, and crime type in 2024, and which district-time-crime combinations appear to need the most public safety attention?

## Project Contents

| File | Description |
| --- | --- |
| `aem_final.ipynb` | Main Jupyter notebook with data collection, cleaning, analysis, charts, maps, and written insights. |
| `chicago_crimes_2024_clean.csv` | Cleaned full-year 2024 Chicago crime dataset. |
| `crimes_map_ready.csv` | Map-ready crime dataset with rows missing latitude/longitude removed. |
| `data_dictionary.csv` | Column-level data dictionary for the cleaned dataset. |
| `crime_heatmap_police_stations.html` | Enhanced interactive Folium map with tile controls, community-area choropleth, heatmap, district hotspot circles, sampled incident popups, and police station markers. |
| `polished_four_person_plan.html` | Team coordination plan, responsibilities, AI-use guidance, and remaining next steps. |

## Data Sources

The project uses public datasets from the City of Chicago Data Portal:

| Dataset | Dataset ID | Use |
| --- | --- | --- |
| Crimes - 2001 to Present | [`ijzp-q8t2`](https://data.cityofchicago.org/d/ijzp-q8t2) | Main 2024 crime incident data. |
| Police Stations | [`z8bn-74gv`](https://data.cityofchicago.org/d/z8bn-74gv) | Police station locations and map markers. |
| COPA Cases - Summary | [`mft5-nfa8`](https://data.cityofchicago.org/d/mft5-nfa8) | High-level accountability supplement. |

The notebook retrieves the main crime dataset through the Socrata API with pagination. The final cleaned dataset covers:

- **Date range:** `2024-01-01 00:00:00` to `2024-12-31 23:58:00`
- **Cleaned rows:** `259,111`
- **Map-ready rows:** `257,531`
- **Columns:** `20`

## Analysis Sections

### A. Data Foundation and Integration

- Pulls full-year 2024 Chicago crime data through the Socrata API.
- Uses pagination instead of a fixed 50,000-row API limit.
- Cleans data types, text fields, booleans, coordinates, and dates.
- Creates derived time variables such as hour, day of week, month, and weekend indicator.
- Exports clean data, map-ready data, and a data dictionary.

### B. Temporal Analysis

- Crime incidents by hour.
- Crime incidents by day of week.
- Crime incidents by month.
- Hour by day-of-week heatmap.
- Top crime types over time.
- Arrest rate over time.
- Normalized weekday and monthly comparisons where calendar length matters.

### C. Spatial Analysis and Map

- Crime count by police district.
- Arrest rate by district.
- Top and bottom community areas by incident count.
- Folium heatmap using mapped crime incidents.
- Community-area choropleth using Chicago boundary GeoJSON.
- District hotspot circle markers sized by incident volume and colored by arrest-rate range.
- Sampled incident popup markers with date, crime type, district, location, arrest outcome, and case number.
- Police station marker cluster.
- Multiple map tile layers and a LayerControl, following the class Folium module.
- Approximate nearest-station distance for mapped crime incidents.

Station distance is used only as geographic context. It does not measure police response time, staffing, patrol coverage, or causality.

### D. Crime Type, Arrest Outcome, and COPA Supplement

- Top 15 crime types.
- Arrest rate by crime type.
- Domestic vs non-domestic comparison.
- Top location descriptions.
- Plotly interactive crime type chart.
- COPA complaint status and category supplement.

COPA is used only as a high-level supplement because most 2024 COPA records have unknown or missing beat information. The notebook avoids strong district-level claims from COPA.

### E. Final Synthesis and Limitations

- Integrated decision-support priority table by police district.
- Priority score combining incident volume, lower arrest outcome rate, and nearest-station distance context.
- Final takeaways connecting temporal, spatial, crime-type, and COPA findings.
- Explicit limitations for missing coordinates, station-distance interpretation, arrest outcome interpretation, COPA beat coverage, and live data updates.

The priority score is a transparent ranking for discussion, not a causal model or a measure of police performance.

## Environment Setup

The project was run in a Conda environment named `cv_hw`.

```bash
conda activate cv_hw
```

Required Python packages include:

```bash
conda install -n cv_hw -y pandas matplotlib seaborn requests folium plotly geopy nbformat nbclient ipykernel
```

The notebook has been executed end to end in this environment with zero code-cell errors.

## How to Run

1. Clone the repository.

```bash
git clone https://github.com/wittydragon22/AEM_final.git
cd AEM_final
```

2. Activate the Conda environment.

```bash
conda activate cv_hw
```

3. Open and run the notebook.

```bash
jupyter notebook aem_final.ipynb
```

If Jupyter is not installed in the active environment, install it or run the notebook from an IDE that supports the `cv_hw` kernel.

The notebook downloads data from the City of Chicago API, so an internet connection is required if rerunning the data-collection cells.

## Generated Outputs

Running the notebook creates or refreshes:

- `chicago_crimes_2024_clean.csv`
- `crimes_map_ready.csv`
- `data_dictionary.csv`
- `crime_heatmap_police_stations.html`

The interactive map can be opened directly in a browser. It includes the course-style Folium features used in the notebook: tile layers, layer controls, marker clusters, popups, tooltips, choropleth shading, and heatmap overlays.

```bash
open crime_heatmap_police_stations.html
```

## Team Members

- Chenghao Liu
- Xinyue Pan
- Ryan Shelley
- Yonglin Zhang

## Course and AI-Use Note

This project was prepared for AEM 5840 Python Programming. The course permits AI-assisted code work, but the team is responsible for understanding, modifying, and rewriting code as needed. Final written interpretation and the final project summary should be written by the team in their own words, following the course AI-use policy.

## Remaining Next Steps

The current notebook includes the main A-E analysis sections. The strongest remaining improvements are:

- Write the final project summary manually in the last notebook cell.
- Prepare presentation slides and recording with all four members speaking.
- Confirm AI-use citations/comments are included where required by the course instructions.

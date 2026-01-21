# PlanetScope AOI-based Mosaic Ordering (Surface Reflectance)

This repository provides a reproducible Python workflow for **searching, selecting, and ordering PlanetScope Surface Reflectance imagery** using the Planet Data API and Orders API v2.  
The workflow is designed for **agricultural, phenology, and time-series studies**
---

## Key Features

- AOI-based PlanetScope scene search using GeoJSON inputs  
- Scene filtering by:
  - Area of interest (AOI)
  - Acquisition date range
  - Scene-level cloud cover
- Verification of **geometric AOI coverage** using scene footprints
- Automated ordering of **Surface Reflectance products**:
  - `analytic_sr_udm2`
- Mosaic (composite) + clip operations using Planet Orders v2
- Order status polling until completion

---

## Workflow Overview

1. **Set Planet API key** as an environment variable  
2. **Load AOI GeoJSON** and convert to MultiPolygon (For feature collection) 
3. **Search PlanetScope scenes** using AOI, date, and cloud filters  
4. **Inspect available assets** to confirm Surface Reflectance availability  
5. **Check AOI coverage** using the union of scene footprints  
6. **Submit an order** with:
   - Surface Reflectance (`analytic_sr_udm2`)
   - Composite (mosaic)
   - Clip to AOI  
7. **Poll order status** until success or failure  

> ⚠️ Scene-level cloud filtering reduces but does **not guarantee** pixel-level cloud-free coverage.  
> Use the provided **UDM2 masks** after download for cloud/shadow masking.

---

## Requirements

- Python ≥ 3.9
- A valid Planet account (Education / Research license supported)

### Python dependencies
```bash
pip install planet requests shapely

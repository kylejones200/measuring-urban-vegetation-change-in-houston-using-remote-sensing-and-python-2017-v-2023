---
author: "Kyle Jones"
date_published: "April 21, 2025"
date_exported_from_medium: "November 10, 2025"
canonical_link: "https://medium.com/@kyle-t-jones/measuring-urban-vegetation-change-in-houston-using-remote-sensing-and-python-2017-v-2023-60b711f33da7"
---

# Measuring Urban Vegetation Change in Houston using Remote Sensing and Python (2017 v 2023) We often talk about urban growth in terms of zoning, housing starts, or
population density. But there's another way to see it --- from space...

### Measuring Urban Vegetation Change in Houston using Remote Sensing and Python (2017 v 2023)
We often talk about urban growth in terms of zoning, housing starts, or population density. But there's another way to see it --- from space. Using open satellite imagery, we can observe how vegetation --- our city's green cover --- has changed over time. And we can do it with math.

In this post, I use Sentinel-2 satellite data to compare vegetation in Houston, Texas between 2017 and 2023. The metric I use is NDVI (Normalized Difference Vegetation Index), a well-established indicator for live green vegetation. I also apply a statistical test called Cohen's Kappa to measure how much vegetation classification has changed --- or stayed the same --- over time.

This isn't just an exercise in geospatial analysis. Understanding where greenness is lost or retained has serious implications for heat vulnerability, air quality, equitable infrastructure investment, and flood resilience. This is about visibility --- making it easier for urban policy, planning, and public debate to track how a city breathes.


### Generate the NDVI Time Series
Using Sentinel-2 Level-2A imagery via the Copernicus Data Space Ecosystem, I collected cloud-filtered satellite images for downtown Houston --- one per month for the years 2017 and 2023.

I then calculated NDVI using the near-infrared and red bands. Each frame represents vegetation density for a particular month. Values close to 1 are dense, healthy vegetation. Values near 0 are bare soil or built-up surfaces.

The result: a monthly NDVI animation for each year.

From the GIF alone, you can see the seasonal rhythm of greenness --- and perhaps subtle changes across the years. But animation isn't analysis. So I quantified it.

### Quantify Monthly Greenness
For each month, I computed the mean NDVI across the entire area of interest. This gives a simple 12-point time series per year.

Then I compared the two years:

``` 
2017 mean NDVI: 0.156  
2023 mean NDVI: 0.163  
Change: +0.007
```

Not a huge difference --- and on its own, not very informative. That's where classification comes in.


### Categorize and Compare with Cohen's Kappa
Next, I converted the NDVI maps into categorical land cover types Low vegetation (NDVI \< 0.1), Medium (0.1 ≤ NDVI \< 0.3), and High (NDVI ≥ 0.3).

This turned every pixel into a simple class. Then, for each month, I compared the 2017 and 2023 classifications pixel by pixel using Cohen's Kappa, a statistical measure of agreement beyond chance.


### What This Means
Cohen's Kappa tells us how well vegetation class agrees between 2017 and 2023.

1.  [In April and May: Kappa values were above 0.65, indicating substantial agreement. Vegetation in these months --- during peak spring --- has been relatively stable. Parks, medians, yards, and greenways appear to be consistently green.]
2.  [In Winter and Fall: January, February, October, and December show very low or no agreement. This could be a real sign of vegetation loss or land cover change or due to seasonal NDVI collapse (i.e., everything is dormant or brown).]
3.  [In Summer: Kappa hovers around 0.2--0.3 --- suggesting partial agreement. Some areas maintained their vegetation status, others likely shifted due to land use change.]

### Policy Recommendations
This kind of satellite-based vegetation monitoring can --- and should --- support local policy.

1.  [Focus on Retention Zones: Where vegetation has persisted over six years, policies that protect those areas should be maintained. Think zoning overlays, park preservation, or targeted shade programs.]
2.  [Identify Change Hotspots: Cohen's Kappa can highlight where NDVI class has changed. These are your red flags --- neighborhoods where vegetation loss may increase heat vulnerability or worsen stormwater runoff.]
3.  [Build It into Permitting: Integrate NDVI change detection into environmental impact assessments. If a development results in a meaningful class change over time (e.g., high to low NDVI), mitigation should be required.]
4.  [Use Seasonal Windows: NDVI comparisons are most reliable in spring and summer. Avoid relying on winter imagery for planning or compliance --- the signals are too noisy.]

### What's Next
The same workflow can be extended to:

- Detect water body shrinkage using NDWI
- Monitor urban forest canopy loss
- Analyze green equity across neighborhoods

Houston's story is not unique. Every city has NDVI footprints. Every city can be seen from space. And every city can --- and should --- be measured.

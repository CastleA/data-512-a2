# data-512-a2
Human Centered Design - Bias in Data - Assignment 2

# The goal of the project
The goal of this assignment was to explore the concept of bias through data on Wikipedia articles on political figures from a variety of countries. 

The purpose was to analyze how the coverage of politicians on Wikipedia and the quality of articles about politicians as estimated by machine learning service, ORES, varies between countries. 

# Data sources, services
Articles on politicians per country were sourced from the dataset [Politicians by Country from the English-language Wikipedia](https://figshare.com/articles/dataset/Untitled_Item/5513449), which is made availabel under a [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/) license. This data is also included in the file page_data.csv and in its original structure within country.zip.

Population data per countries and regions were sourced from the 2020 World Population Data Sheet from the [Population Reference Bureau](https://www.prb.org/international/indicator/population/table/) and is available within this repo in WPDS_2020_data.csv.

Additionally, the service for scoring the quality of wikipedia articles was leveraged via the [ORES scoring interface](https://ores.wikimedia.org/v3/#!/scoring/get_v3_scores_context_revid_model) API. It's useful to note that API works in batches of at most 50 articles at a time.  

# Processed data
The final data file, wp_wpds_politicians_by_country.csv, is both available in the repo and fully reproducible via the included Jupyter Notebook, hcds-a2-bias.ipynb. To run the notebook you will need a computer with python, jupyter notebook, pandas, and seaborn (optionally) installed. 

## Data contains 
The csv, wp_wpds_politicians_by_country.csv, contains 5 columns: country,	article_name,	revision_id,	article_quality_est, and	population. 
- article_name, the name of an article about a politician, generally their name
- country, the country corresponding to the politican subject of the article
- revision_id, an id used by wikipedia to track articles, utilized with ORES scoring service
- article_quality_est, the score estimated by ORES include the options below, further described by [Wikipedia:Content assessment](https://en.wikipedia.org/wiki/Wikipedia:Content_assessment).
 - FA - Featured article
 - GA - Good article
 - B - B-class article
 - C - C-class article
 - Start - Start-class article
 - Stub - Stub-class article
- population, of the country corresponding to the politician subject of the article

Two additional data files are included of excluded data. Articles that could not be scored by ORES had their revision_id and the resultant message stored in wp_wpds_pages_no_score.csv. Countries that could not be joined across the Politicians by Country from the English-language Wikipedia dataset and 2020 World Population Data Sheet were written to wp_wpds_countries-no_match.csv.

## Data quirks
The 2020 World Population Data Sheet contains regions in all caps, excluding the Channel Islands which are not technically a country, but also do not correspond to following rows as is the established pattern. This analysis aligns to the hierarchical structure of the data and treats the Channel Islands as it would a country.

The Politicians by Country from the English-language Wikipedia dataset contains articles beginning with "Template:" that do not correspond to actual articles and should be removed.

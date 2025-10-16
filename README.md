# GoFundMe Success Scraper
Web scraper designed to pull various attributes from GoFundMe posts, which then are analyzed to understand what makes a campaign "successful" (funding over the median value).

**Summary:** This project scrapes and analyzes ~1,000 GoFundMe campaigns to identify the text, imagery, and timing factors that predict fundraising success. We build features from campaign descriptions, image labels, and campaign duration, then train lightweight models to classify campaigns into performance tiers. 

## Goal

Determine which narrative elements, visual cues, and campaign logistics most strongly correlate with higher dollars raised—and turn those signals into simple, interpretable predictors. 

## Data Context

* **Source:** Public GoFundMe campaign pages (scraped for title, description, images, amount raised, duration).
* **Unit:** Campaign-level records with engineered text and image features.
* **Tools:** Python, Jupyter, pandas, scikit-learn, BeautifulSoup, nltk/spaCy (optional), Google Vision or similar image labeling API (Claude vision was used here).

## What This Repo Does

* **Scraping:** Collects campaign metadata, descriptions, images, and timelines.
* **Feature Engineering:**

  * Text: tokenization/lemmatization, n-grams, TF-IDF, topic weights.
  * Images: label extraction through Claude vision (e.g., “outdoor,” “celebration,” “basketball court”).
  * Duration: days active as a core temporal feature.

* **Modeling:** Compares text-only, image-only, and combined models to predict top- vs bottom-quartile outcomes. **Text + duration** performs best; **images + duration** help but add less signal than text alone. 
* **Interpretation:** Surfaces high-lift words/themes and image labels tied to better performance, plus practical guidance for campaign creators. 

## Key Findings (Quick Hits)

* **Duration matters:** High-earning campaigns ran ~31 days on average vs ~8 days for low-earning—longer visibility correlates with more donations. 
* **Words beat pictures (but both help):**

  * Image-only + duration → strong baseline accuracy.
  * Text-only + duration → much higher accuracy.
  * **Text + images + duration → best overall performance** (highest accuracy in our tests). 
* **Language that wins:** Action- and team-oriented narratives (e.g., *team, support, goal, fundraiser*) associate with higher funds; vague or transactional language (*expenses, equipment, training*) correlates with lower funds. 
* **Images that help:** Photos depicting people in action (outdoor, celebration, coaches) outperform static/empty scenes. 

# Anime Character RAG Summarization System

## Overview

This system retrieves and summarizes information about anime characters from the MyAnimeList dataset, providing descriptions (from synopses), fan reviews, anime titles, context, similarity scores, token usage, latency, and an optional image. It’s built using Python, Sentence Transformers, FAISS, and BART, optimized for Kaggle’s environment.

## Prerequisites

- **Kaggle Notebook**: Free tier with GPU T4 x2 enabled (Settings &gt; Accelerator).
- **Dataset**: Upload `myanimelist-dataset-animes-profiles-reviews` to `/kaggle/input/`.
- **Packages**: Install required libraries (run the following in a code cell):

  ```bash
  !pip install sentence-transformers faiss-cpu transformers torch pandas beautifulsoup4
  ```

## Setup

1. Clone or copy the main script (`anime-character-rag.ipynb.py`) into a Kaggle code cell.
2. Ensure the dataset files (`animes.csv`, `reviews.csv`) are in `/kaggle/input/myanimelist-dataset-animes-profiles-reviews/`.
3. Run the script to preprocess three popular characters: Naruto Uzumaki, Luffy Monkey D., and Edward Elric.

## Usage

1. **Run the Script**: Execute the main script to preprocess the three characters and save results to `/kaggle/working/precomputed_data.json`.
2. **Query a Character**: Use the `display_character_output` function to view results for any character. For example:

   ```python
   display_character_output("Naruto Uzumaki", merged_df)
   ```
   - Precomputed characters (Naruto,ichigo, Edward) are instant.
   - New characters (e.g., "Ichigo Kurosaki") are processed on-demand (\~20–40 seconds).
3. **Output**: Results are displayed in a boxed format with:
   - Character name
   - Anime titles
   - Description (synopsis-based)
   - Reviews (fan opinions)
   - Combined summary
   - Context (synopsis/review snippets, similarity scores)
   - Token usage and latency
   - Image (if available)

## Example Output

```
=== RAG Summarization Output for Naruto Uzumaki ===
┌────────────────────────────────────────────────────────────────────────────────────────────────────┐
│ Character: Naruto Uzumaki                                                                                  │
├────────────────────────────────────────────────────────────────────────────────────────────────────┤
│ Anime Titles: Naruto: Shippuuden, Boruto: Naruto the Movie, Naruto...                                      │
├────────────────────────────────────────────────────────────────────────────────────────────────────┤
│ Description: Naruto Uzumaki, a ninja from Konohagakure with the Nine-Tailed Fox sealed inside him...     │
├────────────────────────────────────────────────────────────────────────────────────────────────────┤
│ Reviews: Fans praise Naruto’s inspiring determination and epic battles in Shippuuden...                  │
├────────────────────────────────────────────────────────────────────────────────────────────────────┤
│ Combined Summary: Naruto Uzumaki, a ninja from Konohagakure with the Nine-Tailed Fox sealed inside him...│
│                                                                                                           │
│   Fans praise Naruto’s inspiring determination and epic battles in Shippuuden...                        │
├────────────────────────────────────────────────────────────────────────────────────────────────────┤
│ Context:                                                                                                  │
│   Naruto: Shippuuden: Synopsis: It has been two and a half years... Review: If you want to be hung... (Score: 0.6966) │
├────────────────────────────────────────────────────────────────────────────────────────────────────┤
│ Token Usage: 600                                                                                          │
│ Latency: 2.50 seconds                                                                                     │
│ Image URL: https://cdn.myanimelist.net/images/anime/5/17407.jpg                                          │
└────────────────────────────────────────────────────────────────────────────────────────────────────┘
[Image displayed]
```

## Notes

- Precomputed characters are fast; new characters take \~20–40 seconds.
- Output is saved to `/kaggle/working/precomputed_data.json`.
- GPU acceleration (T4 x2) is recommended for speed.

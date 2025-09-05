# Hinglish Sarcasm Detection Dataset

This repository contains curated datasets for **sarcasm detection in Hindi–English (Hinglish) code-mixed text**.  
The data has been collected, cleaned, and annotated through a combination of **human labelling** and **AI-based labelling**, augmented with derived linguistic features (emoji presence, percentage of Hindi tokens, etc.).

---

## 📂 Dataset Files

Two main CSV files are provided:

### 1. `human_labelled_features.csv`
- Contains comments annotated by **human annotators** for sarcasm detection.
- Includes additional features such as AI-labelled predictions, emoji flags, and the percentage of Hindi tokens.

**Columns:**
| Column           | Description                                                                 |
|------------------|-----------------------------------------------------------------------------|
| `comment`        | The text of the Hinglish comment (Roman script, sometimes with Devanagari). |
| `human_labelled` | Gold label provided by human annotators: `sarcastic` / `non-sarcastic`.     |
| `ai_labelled`    | AI-generated label (baseline model output), left blank for model evaluation.|
| `emoji_present`  | `"yes"` if emojis or emoji placeholders (e.g., `face_with_tears_of_joy`) appear, else `"no"`. |
| `hindi_pct`      | Percentage of tokens in the comment identified as Hindi (0–100).            |

---

### 2. `ai_labelled_features.csv`
- Contains comments labelled by **AI models** (no human annotations).
- Features for emoji and Hindi percentage are also provided.

**Columns:**
| Column          | Description                                                                 |
|-----------------|-----------------------------------------------------------------------------|
| `comment`       | The text of the Hinglish comment.                                           |
| `ai_labelled`   | AI-generated sarcasm label (`sarcastic` / `non-sarcastic`).                 |
| `emoji_present` | Emoji flag as described above.                                              |
| `hindi_pct`     | Percentage of Hindi tokens in the comment.                                  |

---

## 🔍 Data Samples

### From `human_labelled_features.csv`:
```csv
comment,human_labelled,ai_labelled,emoji_present,hindi_pct
Lo or kro Rahul Gandhi face_with_tears_of_joy cross_mark,sarcastic,sarcastic,yes,19.05
eesko krte time kitno ne condom nhi lagaya,non-sarcastic,sarcastic,no,78.57
"kaam kam, dialogues zyada",sarcastic,sarcastic,no,57.14
Finally nayi job mili hai. Offer letter aaya toh maa ke aankhon mein khushi dekh ke alag hi feel hua. 🥺❤️,non-sarcastic,non-sarcastic,yes,73.53
```

### From `ai_labelled_features.csv`:

```csv
comment,ai_labelled,emoji_present,hindi_pct
yadi us rat iske bap ne protection use kiya hota to aj ye paida na hoti,non-sarcastic,no,86.96
kya chutiya pah h yee media,sarcastic,no,90.91
face_with_tears_of_joy face_with_tears_of_joy ky ki ky baat banate ho yr face_with_tears_of_joy face_with_tears_of_joy,sarcastic,yes,16.98
jay siya ram hindu_temple raising_hands or sun jada ni bolte h ok,non-sarcastic,no,57.14
```

---

## 📝 Annotation Details

* **Human Labels:**
  Annotators labelled comments as either `sarcastic` or `non-sarcastic` based on context, tone, and linguistic cues.
  These serve as **gold standard** for evaluation.

* **AI Labels:**
  Obtained via gpt api.
  The AI labels are useful for:

  * Pre-training / bootstrapping models
  * Semi-supervised learning
  * Benchmark comparison with human annotations

* **Emoji Presence (`emoji_present`):**

  * Automatically detected using [emoji](https://pypi.org/project/emoji/) Python package and regex.
  * Captures explicit emojis (`😂`, `🥺`) and textual placeholders (`face_with_tears_of_joy`, `rolling_on_the_floor_laughing`).

* **Hindi Percentage (`hindi_pct`):**

  * Computed using two pipelines:

    1. **FastText + Roman-Hindi Lexicon** for token-level detection.
    2. **BERT Language Identification model** (`sagorsarker/codeswitch-hineng-lid-lince`) for higher accuracy.
  * Represents the fraction of words that are Hindi (in Roman or Devanagari script).

---

## ⚙️ Preprocessing

* **Normalization:**

  * Converted some mojis into text placeholders.
  * Stripped special characters, normalized whitespace.
* **Deduplication:**

  * Removed duplicate entries and accidental header rows.
* **Script Handling:**

  * contains both **Romanized Hindi** and **Devanagari** characters.

---

## 📊 Statistics (approx.)

* **Total Entries:** \~22,000
* **Human-labelled subset:** \~8886 (gold standard, manually annotated)
* **AI-labelled subset:** \~22,000 (pseudo-labels for training augmentation)
* **Label Distribution:** Balanced but slightly skewed towards sarcasm.
* **Emoji Coverage:** \~20–25% of samples contain at least one emoji.
* **Average Hindi %:** 40–70% (varies widely per sample).

---

### Example Tasks:

* Train sarcasm detection models (SVM, BiLSTM, Hing-BERT, etc.)
* Study code-mixing patterns in Hinglish
* Explore emoji impact on sentiment & sarcasm
* Compare AI vs human labelling quality

---

## 📌 Potential Applications

* **Academic Research** in NLP for low-resource languages
* **Sarcasm Detection** in multilingual, code-mixed settings
* **Sentiment Analysis** improvement with emoji & code-mix features
* **Conversational AI** systems (chatbots, moderation tools, etc.)

---

## ⚠️ Limitations & Ethical Considerations

* **Sensitive Content:**
  Comments include profanity, political bias, and offensive language.
  Use responsibly in academic/research contexts.

* **Cultural Context:**
  Sarcasm detection heavily depends on cultural and contextual cues, which may not always be captured by standalone comments.

* **Annotation Bias:**  
  Human labels were created with the help of multiple annotators.  
  Any disagreements were resolved through discussion, and the **final human label** was confirmed jointly by the two authors to ensure consistency.  
  AI labels, meanwhile, are subject to the limitations and biases of the underlying models used to generate them.


* **Not Suitable for Production Deployment** without further cleaning, bias mitigation, and ethical review.

---

## 📚 Citation

If you use this dataset in your work, please cite this repository:

```bibtex
@misc{hinglish_sarcasm_2025,
  author       = {Manan Jain, Hemanth Nagulapalli},
  title        = {Hinglish Sarcasm Detection Dataset},
  year         = {2025},
  howpublished = {\url{https://github.com/<your-repo>}},
  note         = {Code-mixed Hindi-English sarcasm detection dataset with human and AI labels}
}
```

---

## 👩‍💻 Contributors

* **\[Manan, Hemanth]** – Dataset creation, cleaning, labelling pipeline
* Collaborators / Faculty: Prof. Natalie Parde (University of Illinois Chicago) 

---

```

---
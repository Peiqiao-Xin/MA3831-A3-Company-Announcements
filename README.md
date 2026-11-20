# MA3831 Assessment 3: Classifying company announcements

This notebook tests whether a model can assign a category to an extract from a US company's
Form 8-K after the official item heading is removed. The categories are material agreements
(1.01), financial results (2.02), and management or pay (5.02).

## Run the notebook

1. Open `MA3831_A3_Peiqiao_Xin.ipynb` in Jupyter or Colab. Python 3.11 or 3.12 is recommended
   for local use. Code 0 installs the packages needed for each mode.
2. Code 1: leave `MODE = "preview"` to verify the parser on six saved SEC filings.
   Preview runs offline after the basic packages are installed; it does not train a model.
3. Set `MODE = "collect"`, run from Code 0, and enter a contact email when asked.
   The SEC Submissions API gives dates, filing identifiers and HTML filenames. The crawler
   reads the original EDGAR HTML and follows a linked results release when needed.
   Use the same work folder for all stages. Do not bypass access restrictions.
4. Review `study/manual_audit.csv` using the supplied source links. Check collection
   counts and exclusions. The targets are quotas; the output reports actual attainment.
5. Set `MODE = "train"`, run from Code 0 and keep the same working folder. A GPU is
   helpful for DistilBERT. Models share a piece of text capped at 512 tokens including
   special tokens. Companies never cross split boundaries. Validation chooses the TF-IDF
   setting and the DistilBERT checkpoint before the held-out test.
6. The results are in `study/` under the working folder, with CSV tables and PNG figures.
   Compare `training_summary.json` and `collection_summary.json` to tie results to a
   corpus checksum and runtime. New SEC downloads can differ from the original run.

## Sources and repository contents

- [SEC Submissions API](https://www.sec.gov/edgar/sec-api-documentation)
- [SEC EDGAR access guidance](https://www.sec.gov/search-filings/edgar-search-assistance/accessing-edgar-data)
- [Form 8-K](https://www.sec.gov/files/form8-k.pdf)
- [DistilBERT model](https://huggingface.co/distilbert/distilbert-base-uncased)

The notebook contains a small, attributed preview from saved SEC responses. Keep repositories
private unless course instructions allow public sharing and you have checked reuse terms.
Share harvested text or copies of source documents only when permitted. The notebook and
this README are sufficient to run the pipeline; metrics, a URL-only source manifest, and plots
can be shared separately. Do not commit raw caches, credentials, or model weights.

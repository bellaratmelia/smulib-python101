# Slido Questions — Python 101: Pandas DataFrame

Two checkpoints, 4 questions each. All are single-answer **Multiple choice** polls.
The correct option is marked ✅ and each question has a short teaching point for the presenter.

---

## Checkpoint 1 → Q1–Q4 (after `.loc` filtering)

### Q1. You want a per-column count of missing values. Which line gives it most directly?

- A) `data.describe()`
- B) `data.info()`
- C) `data.isna().sum()` ✅
- D) `data.columns`

> Teaching point: `.info()` shows non-null counts (you'd have to subtract), `.describe()` ignores missingness entirely — `.isna().sum()` counts gaps per column directly.

### Q2. What's the difference between `data["age"]` and `data[["age"]]`?

- A) No difference
- B) `data["age"]` returns a Series (1-D); `data[["age"]]` returns a DataFrame (2-D) ✅
- C) `data[["age"]]` throws an error
- D) `data["age"]` returns a DataFrame

> Teaching point: single bracket → Series, double bracket → DataFrame. The double-bracket form is also how you grab several columns at once (`data[["marital_status","age"]]`).

### Q3. Which line correctly selects participants who value work AND are male?

- A) `data[data["work_importance"] >= 2 and data["sex"] == "Male"]`
- B) `data[(data["work_importance"] >= 2) & (data["sex"] == "Male")]` ✅
- C) `data[data["work_importance"] >= 2 & data["sex"] == "Male"]`
- D) `data[data["work_importance"] >= 2, data["sex"] == "Male"]`

> Teaching point: the classic trap. Option A raises an error on a Series; option C **runs but returns the wrong rows** because `&` binds tighter than `>=` without parentheses — exactly the "AI code that runs but lies" case.

### Q4. `data.loc[criteria, "life_satisfaction"]` does what?

- A) Returns only the `life_satisfaction` column, for the rows where `criteria` is True ✅
- B) Returns the row labelled `"life_satisfaction"`
- C) Returns rows 0 through `life_satisfaction`
- D) Filters columns only, keeping all rows

> Teaching point: `.loc[rows, columns]` filters both at once, by label — rows via the boolean mask, column by name.

---

## Checkpoint 2 → Q5–Q8 (before the Time Series section)

### Q5. You have missing values in a column. Which statement is true?

- A) `fillna()` and `dropna()` give the same result
- B) Filling keeps every row but can skew summaries; dropping loses rows but avoids inventing data — it's an analytical choice ✅
- C) You should always drop missing values
- D) pandas ignores missing values everywhere automatically

> Teaching point: reinforces that `fillna("Unknown")` vs `dropna()` is a decision about your analysis, not a syntax detail.

### Q6. You want the average `life_satisfaction` for EACH country. Which line?

- A) `data["life_satisfaction"].mean()`
- B) `data.groupby("country_code")["life_satisfaction"].mean()` ✅
- C) `data["life_satisfaction"].value_counts()`
- D) `data.sort_values("life_satisfaction")`

> Teaching point: the word "**each**" is the signal for `groupby`. Option A gives one overall number, not one per country.

### Q7. `data = data.drop(columns=["employment_marital"])` — why reassign to `data =` instead of just `data.drop(...)`?

- A) `drop()` returns a *new* DataFrame and leaves the original unchanged, so you must reassign (or use `inplace=True`) ✅
- B) `drop()` always changes `data` in place; the reassignment does nothing
- C) It deletes the entire DataFrame
- D) `columns` must be a string, never a list

> Teaching point: same "returns a copy" idea you flag for `sort_values` — most pandas methods hand back a new object rather than mutating in place.

### Q8. In `data.to_csv("wvs-edited.csv", index=False)`, what does `index=False` do?

- A) Skips the header row
- B) Stops pandas writing the row-number index as an extra leftover column ✅
- C) Saves only the first column
- D) Drops missing values before saving

> Teaching point: without it, reloading the CSV gives you a stray `Unnamed: 0` column — the same "stray unnamed column" pattern they hit again in the time-series section.

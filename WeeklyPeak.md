# 📈 WeeklyPeak DAX Measure

This DAX measure calculates the **maximum number of cars present** in a parking lot during any time of the **current week** (based on ISO standard, Monday to Sunday).

---

## 🧠 Logic Explanation

- `CurrDate`: Current date in context from the Calendar table.
- `CurrYear` and `CurrWeek`: Extract year and ISO week number.
- A temporary table is created with:
  - `__Count`: the cumulative active car count.
  - `__EvtYear` and `__EvtWeek`: extracted year and week number from each event date.
- The result is the **maximum number of active cars during the current week**.

---

## 🧾 DAX Code

```DAX
WeeklyPeak =
VAR CurrDate = MAX(Calendar[Date])
VAR CurrYear = YEAR(CurrDate)
VAR CurrWeek = WEEKNUM(CurrDate, 2)    // ISO week (Mon–Sun); use 1 for Sun–Sat
RETURN
MAXX(
    FILTER(
        ADDCOLUMNS(
            ALL(Events),
            "__Count", [CumulativeActive],
            "__EvtYear", YEAR(Events[EventDate]),
            "__EvtWeek", WEEKNUM(Events[EventDate], 2)
        ),
        [__EvtYear] = CurrYear &&
        [__EvtWeek] = CurrWeek
    ),
    [__Count]
)

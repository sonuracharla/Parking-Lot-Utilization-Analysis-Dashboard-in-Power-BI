
# 📅 MonthlyPeak DAX Measure

This DAX measure calculates the **peak number of active cars** present in the parking lot for each **calendar month**.

---

## 🧠 Logic Explanation

- Uses `VALUES(Calendar[Month])` to evaluate for each visible month.
- `CALCULATE(MAX(...))` ensures the highest cumulative count within that month.
- Relies on previously calculated measure `CumulativeActive`.

---

## 🧾 DAX Code

```DAX
MonthlyPeak = 
MAXX(
  VALUES(Calendar[Month]),
  CALCULATE(MAX([CumulativeActive]))
)

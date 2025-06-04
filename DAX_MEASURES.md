# 📐 DAX Measures Used in the Parking Dashboard

## 🚗 Cumulative Active Cars
```DAX
CumulativeActive = 
VAR SortedEvents = 
  SUMMARIZE(
    'Events',
    'Events'[EventTime],
    "NetDelta", SUM('Events'[Delta])
  )
RETURN
  CALCULATE(
    SUMX(SortedEvents, [NetDelta]),
    FILTER(
      ALLSELECTED('Events'),
      'Events'[EventTime] <= MAX('Events'[EventTime])
    )
  )

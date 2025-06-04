DailyPeak =
VAR CurrDate = MAX(Calendar[Date])
RETURN
MAXX(
  FILTER(
    ADDCOLUMNS(
      ALL(Events),
      "__Count", [CumulativeActive]
    ),
    Events[EventDate] = CurrDate
  ),
  [__Count]
)

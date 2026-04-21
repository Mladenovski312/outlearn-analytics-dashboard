# DAX Measures

Full measure library authored for the Outlearn dashboard. Grouped by analytical area.

## Ratings

```dax
Average Course Rating =
    AVERAGEX(
        VALUES(Courses_Reviews[course_id]),
        CALCULATE(AVERAGE(Courses_Reviews[rating]))
    )

Average Rating =
    DIVIDE(
        SUM(Courses_Reviews[rating]),
        COUNTROWS(Courses_Reviews)
    )
```

## Views — volume

```dax
Total Views = COUNTROWS(Views)

Year to Date Views = TOTALYTD([Total Views], 'Calendar'[Date])

Last 7 Days Views =
    CALCULATE(
        [Total Views],
        DATESINPERIOD('Calendar'[Date], MAX('Calendar'[Date]), -7, DAY)
    )

Last 30 Days Views =
    CALCULATE(
        [Total Views],
        DATESINPERIOD('Calendar'[Date], MAX('Calendar'[Date]), -30, DAY)
    )
```

## Views — period over period

```dax
Previous 7 Days Views =
    CALCULATE(
        [Total Views],
        DATESINPERIOD('Calendar'[Date], MAX('Calendar'[Date]) - 7, -7, DAY)
    )

Previous 30 Days Views =
    CALCULATE(
        [Total Views],
        DATESINPERIOD('Calendar'[Date], MAX('Calendar'[Date]) - 30, -30, DAY)
    )

Last 7 Days vs Previous 7 Days =
    VAR Previous7 = [Previous 7 Days Views]
    VAR Current7  = [Last 7 Days Views]
    RETURN DIVIDE(Current7 - Previous7, Current7, 0)

Last 30 Days vs Previous 30 Days =
    VAR Previous30 = [Previous 30 Days Views]
    VAR Current30  = [Last 30 Days Views]
    RETURN DIVIDE(Current30 - Previous30, Current30, 0)
```

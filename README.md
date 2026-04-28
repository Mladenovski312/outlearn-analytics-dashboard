# Outlearn — Engagement Analytics

PowerBI engagement analytics dashboard delivered for **Outlearn (Nu High School)**, an online education platform, in a 48-hour delivery window. The dashboard tracks course performance, review sentiment, and learner view patterns across the platform. The Outlearn team issued a letter of recommendation for the submission. PDF under `recommendation/`.

## Stack

| Layer | Tools |
|---|---|
| Modeling | SQL source tables, star schema with a dedicated Calendar dimension |
| Calculations | DAX measures, M language for the Calendar table |
| Visualization | PowerBI Desktop |

## What the dashboard answers

- Which courses perform best by rating and view volume
- How views trend year-to-date, last 7 days, last 30 days, with period-over-period growth
- Which professors and subjects drive the most engagement
- Where the platform loses users (newsletter unsubscribes, drop-off in review activity)

## Dataset

- Course catalog with subject, professor, and pricing metadata
- Review log with per-course rating history
- View log with timestamps for time-series analysis
- Enrollment and progress tables for learner activity
- Newsletter unsubscribe events
- Data model documented in `docs/schema.svg`

## Key measures

Sample DAX from the dashboard:

```dax
Average Rating =
    DIVIDE(
        SUM(Courses_Reviews[rating]),
        COUNTROWS(Courses_Reviews)
    )

Last 7 Days Views =
    CALCULATE(
        [Total Views],
        DATESINPERIOD('Calendar'[Date], MAX('Calendar'[Date]), -7, DAY)
    )

Last 7 Days vs Previous 7 Days =
    VAR Previous7 = [Previous 7 Days Views]
    VAR Current7  = [Last 7 Days Views]
    RETURN DIVIDE(Current7 - Previous7, Current7, 0)
```

Full measure library in `docs/MEASURES.md`.

## Repository structure

```
Solution_FINAL.pbix      # open in PowerBI Desktop
Solution_FINAL.pdf       # pre-exported report, opens anywhere
recommendation/
  letter_of_recommendation.pdf
docs/
  schema.svg             # data model diagram
  MEASURES.md            # DAX measure catalog
screenshots/             # dashboard views
```

## Role and timeline

48 hours, team of four. I worked on data modeling, measure authoring, and dashboard layout.

## Notes

- Raw platform data excluded from the repository. Dashboard file contains an embedded extract for reproducibility.
- Outlearn branding assets are property of Nu High School and included here only in the recommendation document.

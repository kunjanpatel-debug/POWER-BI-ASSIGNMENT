Session 9

Task 1: Utility of Inactive Relationships in Sports Analytics

Implementation: The primary relationship links `s9_teams[TeamID]` to `s9_matches[Team1ID]` (Active), while a secondary relationship connects `s9_teams[TeamID]` to `s9_matches[Team2ID]` (Inactive).
Justification: In sports modeling, a single match involves two entities from the same lookup dimension table acting in distinct capacities (e.g., Home Team vs. Away Team). If both relationships were active simultaneously, it would introduce ambiguity into the filtering path, causing Power BI to freeze the model to avoid circular dependency errors. 
Utility: Keeping the secondary lane inactive allows the model to map clean primary dashboards based on home-team parameters. When away-team insights or granular head-to-head metrics are required, developers can invoke the inactive line dynamically within specific DAX measures using the `USERELATIONSHIP()` function (e.g., `AwayRuns = CALCULATE(SUM(s9_matches[TotalRuns]), USERELATIONSHIP(s9_teams[TeamID], s9_matches[Team2ID]))`).

Task 2: Impact of Bi-Directional Cross-Filtering (Single vs. Both)
Single Cross-Filter Direction**: Filters only flow downstream from the 1-side (`Teams`) to the Many-side (`Players` or `Matches`). Selecting a match in a report canvas slicer filters the `Matches` table, but the filter context cannot travel upstream back into the `Teams` table to filter down into the `Players` list. As a result, the player stats table remains completely unfiltered.
Bi-Directional Cross-Filter Direction (Both)**: Activating "Both" permits filter context to travel backward up the path. Selecting a specific `MatchID` filters the `Matches` row, which propagates upward to isolate the specific `TeamID` participants, and flows down into the `Players` table. This instantly filters your report canvas cards to display exclusively the active players who participated in that specific match.

Task 3: Data Masking and Security
Implementation: Hidden the structural fields `PlayerEmail` and `PlayerPhone` from the report canvas environment.
Justification: Protects end-user dashboard viewers from interacting with sensitive PII (Personally Identifiable Information), maintaining a clean, clutter-free fields design workspace while keeping the backend data fully accessible for calculation logic.

Task 4: Calculated Columns vs. Measures Behavior
1. Calculated Column (`MatchClassification`)**:
   Evaluation: Evaluated row-by-row during the manual data model refresh cycle.
   Storage: Appended permanently to the table rows in RAM, increasing model file size.
   Use Case: Best used for slicing, grouping, or segmenting visual categories (e.g., filtering a report by "High Scoring" vs. "Regular" matches).
2. Calculated Measure (`AverageRunsPerMatch`)**:
   Evaluation: Calculated dynamically on-the-fly when a visual is rendered on screen.
   Storage: Consumes zero permanent storage memory; acts strictly as a dynamic formula.
   Use Case: Best used for dynamic quantitative summaries that change automatically based on what slicers or filters a user clicks on the report canvas.

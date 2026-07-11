Query Dependencies Explanation

Boxes: The rectangular boxes represent individual data nodes in your report workflow. The top boxes (with folder icons) show the raw physical file paths or folder sources on your system, while the lower boxes represent the individual staging or final query tables inside your model (such as the merged Restaurants table, the appended Zomato_Current_Orders table, and the folder-ingested ipl_files_session7 query with its automatically generated helper files).

Arrows: The directed arrows indicate data lineage and transformation paths, tracking the flow from origin to target. They explicitly show how target queries inherit dependencies from upstream sources—revealing exactly how your Merge and Append processes pull from multiple root nodes to construct unified final tables.

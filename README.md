# Evolution-Database
Created by Dorothy Carmichael
## Purpose
An Access database created to help organize unit costs and requirements to "evolve" characters in the game One Piece Treasure Cruise.
## Contents
### Tables
#### evolvers
ID: Primary key, identifies evolver in database.  
evo_name: Human-readable name of evolver.  
owned: How many of the evolver are currently owned.  
Sorted by ID.
#### units
ID: Primary key, identifies unit in databse.  
unit_name: Human-readable name of unit. May include identifier for variant versions.  
level: Current level of unit.  
max_level: Level at which unit may evolve.  
color: Color of unit.  
evo*: Evolvers needed to evolve unit.  
Sorted by level, ID.
### Queries
#### can_do
Returns ID and unit_name of any units at the required level for evolution for which all evolvers listed in evo* columns are owned.
#### need_evos
Returns unit_name of any units at the required level for evolution for which all evolvers listed in evo* columns are not owned.
#### need_levels
Returns unit_name, color, and levels to max of any units not at the required level for evolution for which all evolvers listed in evo* columns are owned.
#### need_levels_and_evos
Returns unit_name, color, and levels to max of any units not at the requried level for evolution for which all evolvers listed in evo* columns are not owned.
#### required_evos
Returns ID as evo and the number of times which that ID appears in the evo* columns of the units table for every evolver in the evolvers table.
#### required_evos_readable
Returns evo_name, number needed, and whether or not all required are currently owned for all evolvers listed in at least one of the evo* columns in the units table. need_more will have a value of 0 of all required are owned, and -1 otherwise.
#### unneeded_evos
Returns ID, evo_name, and owned for all evolvers which are not required for any current unit's evolution and for which the number owned is greater than ten. Excludes rare units with the name "rainbow".
#### TO_GET
Returns evo_name and the difference between owned and needed for every evolver currently required for a unit evolution where the difference is greater than 0.
#### TO_GET_*
Returns evo_name and the difference between owned and needed for every evolver currently required for a unit evolution where the difference is greater than 0 and the evolver belongs to the specified subset.
#### color_mistakes
Returns unit_name, evo_name, and the ID of the evolver for every evolver whose color differs from the color of the unit. Excludes evolvers with the name "rainbow", seahorse evolvers, and one specific skull evolver.
#### rm_unit
Deletes a unit specified by the form EVOLVE from the units table.
#### rm*
Updates the evolvers table to decrease the number of the evolver in the respective evo* column of the unit specified by the form EVOLVE.
### Forms
#### EVOLVE
Takes a unit ID for the units table and runs a macro to update the database and process that unit's evolution.
### Macros
#### evolve
Runs rm* and rm_unit queries.

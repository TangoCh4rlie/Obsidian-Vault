Locations.csv

LOAD CSV WITH HEADERS FROM 'file:///location.csv' AS row
FIELDTERMINATOR ';'
MERGE (l:Location {locationID: row.locationID})
SET l.name = row.locationName;

Sponsor1.csv

LOAD CSV WITH HEADERS FROM 'file:///sponsor1.csv' AS row
FIELDTERMINATOR ';'
MERGE (:Sponsor {id: row.sponsorID, name: row.sponsorName});


observation.csv

LOAD CSV WITH HEADERS FROM 'file:///observation.csv' AS row
FIELDTERMINATOR ';'
MERGE (:Observation {id: row.observationOMOPID, name: row.observationOMOPName});
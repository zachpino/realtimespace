###Scoping Data

-----

A fundamental aspect of working with D3 is the idea of *domains* and *ranges*. 

- A *domain* is the boundaries of our data. For instance, if our dataset comprised timestamps collected all day, our domain might be -12 to 12.
- A *range* is the boundaries of our data's intended representation. If we wanted those timestamps to fit into a 100px graphic, our range would be 0 to 100.

D3 uses domains and ranges to map our data to our screen's coordinates.

___
- tags: #burp_suite #intruder 
___
## Sniper
Is default commonly used option. It cycles through the payloads, inserting one payload at a time into each position defined in the request.
## Battering ram
It sends all payloads simultaneosly, each payload inserted into is respective position. This attack type is useful when testing for race conditions or when payloads need to be sent concurrently.
## Pitchfork
Enables the simultaneous testing of multiple positions with different payloads. It allows the tester to define multiple payload sets, each associated with a specific position in the request. Pitchfork attacks are effective when there are distinct parameters that need separate testing.
## Cluster bomb
Attack type combine the Sniper and Pitchfork approaches. It performs a Sniper-like attack on each position but simultaneously tests all payloads from each set. This attack type is useful when multiple positions have different payloads, and we want to test them all together.

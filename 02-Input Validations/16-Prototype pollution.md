# Prototype pollution (NodeJS application)

|ID          |
|------------|
|GTRT-INPV-16|

## Summary

Prototype Pollution attacks, as the name suggests, is about polluting the prototype of a base object which can sometimes lead to RCE.

## How to Test

According to the [research paper](https://github.com/HoLyVieR/prototype-pollution-nsec18/blob/master/paper/JavaScript_prototype_pollution_attack_in_NodeJS.pdf), Prototype pollution is exploitable only if any of the following 3 happens:

1. Object recursive merge
2. Property definition by path
3. Object clone

## References

Application Development Security 1.1/S1(b) Validate all inputs from external data sources, such as web forms submissions and API services provided by other systems

Application Development Security 1.1/S1(e) Encode output for all data returned to the requester

https://blog.0daylabs.com/2019/02/15/prototype-pollution-javascript/
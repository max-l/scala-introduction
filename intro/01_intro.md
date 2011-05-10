!SLIDE smbullets
# Scala
## a Scalable Language

!SLIDE small
# 2006
# Dynamic Languages Peak in popularity
## Ruby, Groovy, Python, PHP
## High expressivity / Low verbosity
## Write less code, less time to code

!SLIDE small
# *BUT* 
# Absence of compilation means
## Code time savings are offset by more time spent debugging !
## Hard to refactor
## Need to write test cases to ensure basic sanity (...like type abuse !)


!SLIDE small
# Can we have it both ways ?
## Low verbosity _and_ High compile time validation 

!SLIDE small
# Scala
## Almost as succinct as a dynamic language
## With a powerfull type system that incurs low conceptual overhead (*)

    @@@ Scala
	class Person(name: String, age: Int)
	
	val crowd = ...
	
    val (children, adults) = crowd.partition(_.age < 18)
	
	
<!-- //## (*) for library users -->
!SLIDE small	
# Pattern Matching

	@@@ Scala
	case class Address(
	  streetName: String, 
	  appartmentNumber: Option[Int], 
	  postalCode: String, city: String)
	case class Person(name: String, address: Option[Address])
	case class Dog(name: String, owner: Person)

	for(p <- beings) 
	  p match {
		case Dog(n,Person(nameOfOwner)) 
		  => println(n +" is the dog of " + nameOfOwner)
		case Person(n,None) 
		  => println("Adress of " + n + " is unknown")
		case p:Person(_,Some(Address(_,_,"H0H-0H0",_))) 
		  => println(p.name + " is Santa Clauss !")
		case a:Any => println(a + " is neither a dog or a person !")		
	  }

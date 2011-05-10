!SLIDE	
# Nullability exposed to the type system

##I call it my billion-dollar mistake. It was the invention of the null reference in 1965. At that time, I was designing the first comprehensive type system for references in an object oriented language (ALGOL W).I couldn't resist the temptation to put in a null reference, simply because it was so easy to implement. 

!SLIDE small	
# Nullability exposed to the type system
## Option[A] vs null

	@@@ Scala
	//for starters, Option[A] is self documenting
    class Person(val name: String, val age: Option[Int])
	
	// Will not compile :
	val avgAge  = crowd.map(_.age).sum
	//error: could not find implicit value for parameter num: Numeric[Option[Int]]
    //val avgAge  = crowd.map(_.age).sum
	
	// you are forced to deal with null, or 'unknown' values
	crowd.map(_.age.getOrElse(0)).sum
	
	//another way to deal with 'unknowns' :
	crowd.filter(_ != None).map(_.age.get).sum

	trait Map[K,V] {
	  def get(k: K): Option[V]
	}

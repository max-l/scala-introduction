!SLIDE	
# Nullability exposed to the type system

###I call it my billion-dollar mistake. It was the invention of the null reference in 1965. At that time, I was designing the first comprehensive type system for references in an object oriented language (ALGOL W).I couldn't resist the temptation to put in a null reference, simply because it was so easy to implement. 

###This has led to innumerable errors, vulnerabilities, and system crashes, which have probably caused a billion dollars of pain and damage in the last forty years.

###More recent programming languages like Spec# have introduced declarations for non-null references. This is the solution, which I rejected in 1965.

### _Tony Hoare_

!SLIDE small	
# Option[A] 
## a type safe alternative to null

	@@@ Scala
	//for starters, Option[A] is self documenting
    class Person(val name: String, val age: Option[Int])
	
	val p = List(
	 new Person("Xiao",Some(45)), 
	 new Person("Zong", None)
	)

!SLIDE small	
	@@@ Scala	
	
	val crowd = List(
	 new Person("Xiao",Some(45)), 
	 new Person("Zong", None)
	)
	
	// Will not compile :
	val avgAge  = crowd.map(_.age).sum
	//error: could not find implicit value for parameter num: Numeric[Option[Int]]
    //val avgAge  = crowd.map(_.age).sum
	
	// you are forced to deal with null, or 'unknown' values
	crowd.map(_.age.getOrElse(0)).sum
	
	//another way to deal with 'unknowns' :
	crowd.filter(_.age != None).map(_.age.get).sum
	
!SLIDE small	

## scala.collection.Map

	@@@ Scala		
	trait Map[K,V] {
	  ...
	  def get(k: K): Option[V]
	  ...
	}

## java.util.Map

	@@@ Java
	public interface Map<K,V> {
	  ...
	  public V get(k: K);
	  ...
	}
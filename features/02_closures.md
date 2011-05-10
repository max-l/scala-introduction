!SLIDE smbullets  small
# Closures
## A powerfull mechanism for code reuse, ...from the 50s

    @@@ Scala
	class Person(val name: val String, age: Int)

	val ageSum  = crowd.map(_.age).sum
	// lets not deal with div by 0 for now....
    val ageAvg = ageSum / crowd.size 
	val belowAvgAge  = 
	  crowd.filter(_.age < avgAge)

	val ageGroups = crowd.groupBy(_.age)
	
	//the type of ageGroups is : Map[Int,Iterable[Person]]

!SLIDE smbullets small
# More closures
	
    @@@ Scala	
	val ageGroups = crowd.groupBy(_.age)
	
	println("Age distribution :")
	
    ageGroups //ageGroup is a Map[Int,Iterable[Person]]
	.map((age,group)=>(age,group.size)) //now a Map[Int,Int]	
	.toSeq
	.sortBy(_._1)
	.foreach(println(_._1 + " : " + _._2))

	//What if we did .map((age,group) => age) instead ?

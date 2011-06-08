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
	val ageDistribution = 
	 crowd.groupBy(_.age) //Map[Int,Iterable[Person]]
	 .map((age,group)=>(age,group.size)) //Map[Int,Int]	
	 .toSeq //Seq[(Int,Int)]
	 .sortBy(_._1)

	val largestAgeGroup = 
	  ageDistribution.maxBy(_._2)
	  
	val youngestAgeGroup = 
	  ageDistribution.minBy(_._1)	  
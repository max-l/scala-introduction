!SLIDE smbullets  small
# Tuples
    @@@ Scala

	val things  = (3, "hello world", new Date)

	println(things._1 + " times 5 is " + things._1 * 5)
	println(things._2.toUpperCase)
	println("Now : " + things._3)

	class Rectangle(val x: Float, val y: Float) {
	  def coordinate = (x,y)
	}


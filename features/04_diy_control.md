!SLIDE small	
# DIY control structures

	@@@ Scala
	object TxUtils {
	  def transaction[A](a: =>A) = {
	    val c = createConnection
	    try {
	      val r = a
		  c.commit
		  r
	    }
	    catch {
	      case e:Exception => {c.rollback; throw e}
	    }
	  }
	}
	
	import TxUtils._
	val result = transaction { 
	  //db code here...
	}

!SLIDE small	
# Another DIY control structure
## Suppose Scala did not have a "do while" loop
	
	@@@ Scala
	
	class DoWhile(wBlock: ()=>Unit) {
	  def While(condition: =>Boolean) {
	    wBlock()
		val c = condition _
		while(c())
		  wBlock()
	  }
	}

	object MyDoWhile {
	  def Do(wBlock: =>Unit) = 	  
	    new DoWhile(wBlock _)
	}

!SLIDE small		
	@@@ Scala
	
	import MyDoWhile._
	
	var i = 0
	Do {
	  println(i);
	  i = i + 1
	} While(i < 10)
	
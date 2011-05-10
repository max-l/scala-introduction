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
	      case e:Exception => {
		    c.rollback
			throw e
		  }
	    }
	  }
	}
	
	import TxUtils._
	val result = transaction { 
	  //db code here...
	}

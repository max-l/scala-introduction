!SLIDE small	
#Lazyness

	@@@ Scala
	
	class HugeObject(val hugeString: String) {
	  
	  lazy val md5 = 
	    MD5.compute(hugeString)
	}
	
	
!SLIDE small	
#Lazyness

	@@@ Scala
	
	object Logger {
	  
	  var logLevel: LogLevel
	  
	  protected def doLog(msg: String) = {...}
	  
	  def logDebug(msg:  =>String) = 
	    if(logLevel > LogLevel.Debug)
		  doLog(msg())
	}

	// What's wrong with this : 
	logDebug(" : " + loadHugeChunkOfContextualInfo().toString + 
	         ", " + moreContextualInfo)
	// ?
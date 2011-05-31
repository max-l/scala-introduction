!SLIDE small	
#Lazyness
##The Java way

	@@@ Java	
	public class HugeObjectJava {	  
	  private String hugeString;	  
	  private String _md5;	  	
	  public HugeObjectJava(String s) {this.hugeString = s;}
	  public String md5() {
	    synchronized {
		  if(_md5 == null) {
			_md5 = MD5.compute(hugeString)
		  }
		}
		return _md5;
	  }
	}

!SLIDE small	
#Lazyness
## Scala works hard to be lazy
	
	@@@ Scala	
	class HugeObjectScala(val hugeString: String) {	  
	  lazy val md5 = MD5.compute(hugeString)
	}

!SLIDE small	
##In reality, Java's verbosity is much worse if you want to implement a "lazy val"

	@@@ Java	
	public class HugeObjectJava {	  
	  private String hugeString;	  
	  private volatile String _md5;	  	
	  public HugeObjectJava(String s) {this.hugeString = s;}
	  public String md5() {
	    if(_md5 == null) {
		  synchronized {
			if(_md5 == null) {
			  _md5 = MD5.compute(hugeString)
			}
		  }
		  return _md5;
		}
		return _md5;
	  }
	}
	
!SLIDE small	
#More Lazyness

## What's wrong with this ? 

	@@@ Scala
	
	def doSomething = {
	   doOneThing(1)
	   logDebug("While doing a thing : " + 
	         loadHugeChunkOfContextualInfo().toString + 
	         ", " + moreContextualInfo)
	   anotherThing(2)
	}

!SLIDE small	
#Lazyness to the rescue

	@@@ Scala	
	object Logger {
	  
	  var logLevel: LogLevel
	  
	  protected def doLog(msg: String) = {...}
	  
	  def logDebug(msg:  =>String) = 
	    if(logLevel >= LogLevel.Debug)
		  doLog(msg())
	}
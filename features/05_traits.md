!SLIDE small	
# Traits and Mixins
## Dependency injection with static validation
	@@@ Scala
	
	trait KeyedEntity[K] {

	  def id: K
	}

	trait Optimistic {
	  self: KeyedEntity[_] =>

	  protected val occVersionNumber = 0
	}

	class Book(val id: Long, title: String)
	  extends KeyedEntity[Long] with Optimistic

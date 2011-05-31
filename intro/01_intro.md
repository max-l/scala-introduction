!SLIDE smbullets
# Scala
## a Scalable Language

!SLIDE small
# 2006
# Dynamic Languages Peak in popularity
## Ruby, Groovy, Python, PHP
## High expressivity / Low verbosity
## Write less code, less time to code

!SLIDE small
# *BUT* 
## No compilation means
# _No type checking_ !

!SLIDE small
# ... No type checking means
## Code time savings are offset by more time spent debugging !
## Hard to refactor
## Need to write test cases to ensure basic sanity (...like type abuse !)


!SLIDE small
# Can we have it both ways ?
## Low verbosity _and_ High compile time validation ?

!SLIDE small
    @@@ Scala
	object HelloWorld {

	  val hello = "Hello"
	
	  def world = "World"
	  
	  def say(msg: String) = println(msg)
	  
	  def main(args: Array[String]) = {
	     say(hello + " " + world)
	  }
	}

!SLIDE small
#Java
    @@@ Java
	public class Person {
	  private String name;
	  private Int age;
	  public Person(String name, int age) {
	    this.name = name;
		this.age = age;
	  }
	  public Int getAge() {return age;}
	  public void setAge(int age) {this.age = age}
	  public Int getName() {return name;}
	  public void setName(String name) {this.name = name}
	}

#Scala	
    @@@ Scala
	class Person(var name: String, var age: Int)
	
!SLIDE small
# Scala
## Almost as succinct as a dynamic language
## With a powerfull type system

    @@@ Scala
	class Person(name: String, age: Int)
	
	val crowd = ...
	
    val (children, adults) = crowd.partition(_.age < 18)
!SLIDE smbullets incremental
# DSLs 
## Domain Specific Languages
* Domain experts know all about the what
* Programmers know about the how
* What if a Domain expert could understand the code ?


!SLIDE small

## A Java DSL for physics

	@@@Java	
	Speed s = 
	  new Speed(
	    new Distance(5.3, DistanceUnits.KM), 
		new Time(15, TimeUnits.MINUTES).minus(
		 new Time(5, TimeUnits.SECONDS))
	  )

## We could do a little better 
	  
	@@@Java	
	class TurboInfraRetroMagnetor extends Units {
	//...	
  	  Speed s = 
	    speed(
	      kms(5.3), 
		  minutes(15).minus(seconds(5))
	    )
		
	  
!SLIDE small	
## The same DSL in Scala

	@@@Scala
	
	import DSL._
	
	val vitesse = 5.3.km / (15.minutes - 5.seconds)	 
	
!SLIDE small	
## Under the Hood : Implicit conversions and a bit of syntactic sugar

	@@@Scala
	object DSL {
	 implicit def int2Time(i: Int) = new TimeUnit(i)
	 implicit def float2Distance(f: float) = new Distance(f)

	 class TimeUnit(val milliseconds: Long) {
	   def seconds(i: Int) = new TimeUnit(i * 1000)
	   def minutes(i: Int) = new TimeUnit(i * 1000 * 60)
	   def -(t: TimeUnit) = 
	     new TimeUnit(this.milisseconds = t.milliseconds)
	 }
	 class Speed(val d: Distance, val t: TimeUnit)
	 class Distance(val millimeters: Float) {
	   def km(f: Float) = new Distance(f * 1000^2)
	   def / (t: TimeUnit) = new Speed(d, t)
	 }
	}
	
	import DSL._
	
	val vitesse = 5.3.km / (15.minutes - 5.seconds)	 

	
!SLIDE xml_swamp
#Maven, an XML DSL
	@@@XML
	<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" 
	 xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
	  <modelVersion>4.0.0</modelVersion>
	  <groupId>emb</groupId>
	  <artifactId>emb</artifactId>
	  <version>0.0.1-SNAPSHOT</version>
	   <properties>
		   <jetty.version>7.3.0.v20110203</jetty.version>
		   <bayeux.version>2.1.1</bayeux.version>
	   </properties>
	   <repositories>
		   <repository>
			   <id>repo2_maven_org</id>
			   <url>http://repo2.maven.org/maven2</url>
		   </repository>
	   </repositories>
	   <dependencies>
		   <dependency>
			   <groupId>org.eclipse.jetty</groupId>
			   <artifactId>jetty-server</artifactId>
			   <version>${jetty.version}</version>
		   </dependency>
		   <dependency>
			   <groupId>org.eclipse.jetty</groupId>
			   <artifactId>jetty-util</artifactId>
			   <version>${jetty.version}</version>
		   </dependency>
		   <dependency>
			   <groupId>org.eclipse.jetty</groupId>
			   <artifactId>jetty-servlet</artifactId>
			   <version>${jetty.version}</version>
		   </dependency>		   
		   <!-- Bayeux Jars -->
		   <dependency>
				<groupId>org.cometd.java</groupId>
				<artifactId>cometd-java-server</artifactId>
				<version>${bayeux.version}</version>
			</dependency>		   
		   <dependency>
				<groupId>org.cometd.java</groupId>
				<artifactId>cometd-java-common</artifactId>
				<version>${bayeux.version}</version>
			</dependency>
			<dependency>
				<groupId>org.cometd.java</groupId>
				<artifactId>bayeux-api</artifactId>
				<version>${bayeux.version}</version>
			</dependency>		
	   </dependencies>	  
	</project>	
	
	
!SLIDE xml_swamp small
#SBT (Simple Build Tool)

## A Scala DSL for dependency management and build

	@@@Scala
	import sbt._


	class SquerylProject(info: ProjectInfo) extends DefaultProject(info) {
	  
	  val snapshot = systemOptional("snapshot", false).value
	  
	  override def version = {
		super.version match{
		  case BasicVersion(major, minor, micro, extra) if snapshot =>
			BasicVersion(major, minor, micro, Some("SNAPSHOT"))
		  case other => other
		}
	  }
	  
	  val publishTo = 
		if(snapshot)
		  "Scala Tools Snapshots" at "http://nexus.scala-tools.org/content/repositories/snapshots/"
		else
		  "Scala Tools Release" at "http://nexus.scala-tools.org/content/repositories/releases/"
	  
	  override def managedStyle = ManagedStyle.Maven
	  
	  override def packageSrcJar = defaultJarPath("-sources.jar")
	  
	  val sourceArtifact = Artifact.sources(artifactID)
	  
	  override def packageToPublishActions = super.packageToPublishActions ++ Seq(packageSrc)
		
	  Credentials(Path.userHome / ".ivy2" / ".credentials", log)
	  
	  override def pomExtra =
		<licenses>
		  <license>
		  <name>Apache 2</name>
		  <url>http://www.apache.org/licenses/LICENSE-2.0.txt</url>
		  <distribution>repo</distribution>
		  </license>
		</licenses>
			  
	  val cglib = "cglib" % "cglib-nodep" % "2.2"
	  
	  // The following jars are for running the automated tests	  
	  val junit = "junit" % "junit" % "4.8.2" % "provided"
	  val h2 = "com.h2database" % "h2" % "1.2.127" % "provided"  
	  val mysqlDriver = "mysql" % "mysql-connector-java" % "5.1.10" % "provided"
	  val posgresDriver = "postgresql" % "postgresql" % "8.4-701.jdbc4" % "provided"
	  val msSqlDriver = "net.sourceforge.jtds" % "jtds" % "1.2.4" % "provided"
	  val derbyDriver = "org.apache.derby" % "derby" % "10.7.1.1" % "provided"
	  val snapshotsRepo = "snapshots-repo" at "http://www.scala-tools.org/repo-snapshots"			  
	  
	  val scalatest = 
		if(!crossScalaVersionString.startsWith("2.8")) 
		  "org.scalatest" %% "scalatest" % "1.4.1" % "provided"
		else
		  "org.scalatest" % "scalatest_2.8.0" % "1.3.1.RC2" % "provided"

	}
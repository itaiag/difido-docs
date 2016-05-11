# Running with TestNG

Difido can use with the TestNG framework to create flexible reports that can be viewed at run-time.


## Adding the Difido to the project

### Maven

Since Difido is not yet available in the central Maven repositories, you will need to add JSystem as a repository in your project POM file
~~~~ xml
<repositories>
	<repository>
		<id>topq</id>
		<url>http://maven.top-q.co.il/content/groups/public</url>
	</repository>
</repositories>
~~~~~

The Difido project

~~~~~ XML
<dependency>
	<groupId>il.co.topq.difido</groupId>
	<artifactId>difido-reports-common</artifactId>
	<version>1.3</version>
</dependency>
~~~~~


## Adding the Difido as listener
You can register the Difido in any standard TestNG registration method. The recommended way is to use *@Listeners* annotation


~~~~~ Java
@Listeners(il.co.topq.difido.ReportManagerHook.class)
public abstract class AbstractTestCase {
	
	protected ReportDispatcher report = ReportManager.getInstance();

}

~~~~~
After registration, the report dispatcher object is available for your use.

## Output
When running from an IDE the reports are generated in *<project root>/test-output/difido/current*. When running directly from Maven the reports a generated in the *target/difido/current* folder

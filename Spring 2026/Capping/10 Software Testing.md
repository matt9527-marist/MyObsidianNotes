● What is software testing?

> “An investigation conducted to provide stakeholders with
   information about the quality of the product or service under test.”

● What properties are under test?
	– Meets the design and development requirements
	– Responds correctly to all kinds of inputs
	– Performs functions within an acceptable time
	– Is sufficiently usable
	– Can be installed and run in its intended environments
	– Achieves the general result its stakeholders desire

● Too many variations to completely test  
software  
● Proper testing identifies what’s important  
to ensure software quality  
● Choose wisely to fit within project deadlines  
● Testing is an iterative process  
	– Fixing a bug can reveal other, deeper bugs

**Testing Lifecycle**
Testing on a software project can have  
multiple phases  
	– Unit test  
	– Function test  
	– System test / Solution test  
	– Performance test  
	– Integration test  
	– Customer test

**Unit Test**
● Performed by the developer writing the code  
● Simple tests, narrow in scope  
● Does the code pass the “smell test”?  
	– Does it minimally perform what it’s supposed  
	to do?  
● True “white box” testing, since developer  
has full knowledge of code internals

**Function Test**
● Performed by a dedicated tester  
	– Sometimes a developer pressed into test duty  
	– Usually has close relationships to development team  
● More complex tests, larger in scope  
● Do project pieces fit together?  
● Does software perform tasks it’s supposed to?  
● Can be either white-box or black-box testing  
● Should not be finding unit test level bugs  
	– These are considered “escapes”, and indicate the developer did  
	not test adquately

**System/Solution Test**
● Performed by dedicated test team  
	– Independent of development team  
	– Ideally a different management structure  
● Can communicate with development to set and understand  
expectation  
● Acts as the “first customer” for the software  
	– Has real hardware  
	– Uses product documentation  
● Very complex tests  
● Black box testing only  
● Should not be finding simple function test escapes

**Performance Test**
● Performed by a dedicated test team  
	– Need access to dedicated hardware in a controlled environment  
	– A system busy with other work will spoil the results!  
● Can run synthetic benchmark software to look for performance bottlenecks  
● Can run real workloads to ensure customers have adequate performance  
● Works with legal team to make a real performance claim  
	– 12% improvement in transaction rate  
	– 33% less memory usage  
	– 99.999% uptime  
	– Hard number claims must be backed by valid data, as customers can and will  
	sue if the claims turn out to be false or misleading!  
		● (This is why the lawyers are involved)

**Test Approach Document**
● Written by testing group as a guide to testing a product  
	– Explains what will be tested...  
	– and how that testing will be accomplished  
● Should be reviewed by test team, as well as developers  
	– A good developer can suggest fragile or suspect areas of  
code to focus test efforts on  
● Shows how to setup the test environment  
	– How tests will be run  
	– How test results will be recorded

**What to test?**
● Depends on the product  
● Does it have APIs?  
	– Then the tester needs to program to them  
● Does it have a CLI?  
	– Then all the commands need exercising  
● Does it have a GUI?  
	– Then all the widgets need clicking

**Potential Problems**
● Is the software deterministic?  
	– Does identical input lead to identical output?  
	– It’s simpler to test code that has a direct mapping from inputs to  
outputs.  
● Complex systems with multiple interacting components are more  
difficult to test  
	– How do you know if you are hitting edge cases?  
	– What if a component fails?  
	– Netflix has Chaos Monkey that automatically terminates production  
	instances.  
		● If your service can survive being randomly killed, then it’s probably pretty robust

**Tests Burn Down Chart**
● Shows overall progress with test execution  
	– Easy to understand at a glance  
	– Goal is to “burn down” to zero remaining test cases by the scheduled date  
	– Different test categories  
	– Not yet run  
● Blocked  
● Not yet scheduled  
● Not enough time  
	– Run but failed  
● Missing function  
● Broken function  
● Broken test case  
	– Successfully run

![[Pasted image 20260302220217.png]]

**Creative Testing**
● It’s not enough to test mainline code  
● You also need to test for boundary and edge  
cases  
● If there is concurrency, then test for race  
conditions  
● Try to get the code to go down unexpected  
paths  
● Also try to cause error situations

**Fuzz Testing**
● This is using tooling to automatically thrash  
interfaces with garbage data  
	– Can cause crashes, unexpected behavior, or worse  
	– It can be a great way to ensure that code behaves  
in a deterministic fashion  
● Exercises code in ways that the developer didn’t  
expect  
	– If you only test your parser with 7-bit ASCII, a fuzzer  
	will generate interesting results!

**Regression Testing**
Ensures that a product has not “regressed”  
any functionality due to code changes  
● Usually performed at least once per release  
cycle  
● Can be a large, involved bucket of tests  
	– Tests are accrued over many releases  
	– Passing this test gives you confidence that the  
	product is at least as good at the prior version

**Test Coverage**
● Test coverage  
	– How much of your code is covered by tests?  
	– If your code is in an infrequently used path, how do you know it works?  
	– Little-used error paths that are broken can cause problems when you  
	least expect it  
	– Test coverage is a percentage value of the amount of code that is  
	executed by test statements  
	– A static analyzer tool like FindBugs or SonarQube can calculate this  
	value  
		● FindBugs example for Java  
			– List of bugs detected  
		● Splint example for C

**Test Automation**
● Automating test cases frees up tester time to  
pursue other work  
	– Manual testing is tedious and error prone  
	– This can be ideal work for a computer!  
● Example: Command line interface  
	– Have test cases that call commands, and parse  
the output  
	– If there is a direct relationship between input and  
	output, this can be checked for programmatically

● Example: API testing  
	– Write a program that calls the API in question  
	– Pass a variety of values, and check for  
	appropriate return codes  
	– Verify that API worked by calling other APIs,  
	or checking external interfaces


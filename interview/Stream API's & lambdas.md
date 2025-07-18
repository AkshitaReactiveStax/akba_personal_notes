#interview-prep 

#Note if Interface I and Interface J have same abstract method  and a class C implements both I, J , then class C  can also provide it's own implementation for show .
 
#Note if Interface I and Interface J have same default  method  and a class C implements both I, J , then class C has to provide it's own implementation for show  , otherwise it will create a diamond problem and java will be confused again which interface's implementation class C should execute at runtime . 

#Note  if Interface I and Interface J have same default  method  and  Class A is a class with same method  (not extending or implementing any other class/ interface ) , and a class C implements Interface I and extends class A  , then class C will execute Class A 's  implementation because class has higher priority over interface's default methods. 

#Note If you have an interface with a default method which is also a method in Object class then you cannot make define it as a default method inside that interface . 

#Note Static Methods -> in an interface we can define static methods as well from java 8 . 
we can directly call the method . 

#Note Functional programming ->
Lambdas -> you can only write lambdas of interfaces that are functional interfaces which have a single abstract method only . That interface can have default methods and static methods but it can only have a single abstract method to be able to write a lambda / method referrence of it .   
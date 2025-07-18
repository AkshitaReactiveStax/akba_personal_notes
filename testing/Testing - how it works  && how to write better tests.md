
##### how do i think while writing a test in AAA

When writing a test using the AAA (Arrange, Act, Assert) approach, your thought process should be methodical and focused on isolating the behavior you’re testing. Here’s a step-by-step guide to help you think through writing a test:

#### **1. Arrange (Setup the Stage)**

**What to Think About:**

• **What is being tested?** Identify the method or functionality you want to test.
• **What inputs are needed?** Determine the parameters, mocks, or objects that are required.
• **What dependencies exist?** If the method relies on external services, database calls, or other components, mock or prepare them appropriately.


**Action Steps:**

• Create mock objects or real objects depending on the test type (unit vs integration).
• Define input data and expected outcomes.
• Stub/mock dependencies with tools like Mockito.


**Example Thought:**

_“I need to test_ _calculateTotalPrice()_ _for an order with a discount. I’ll mock the discount service and prepare a sample order object.”_




#### **2. Act (Execute the Action)**

**What to Think About:**

• **What is the exact action I’m testing?** Focus on the single method or action under test.
• **How do I trigger this action?** Identify how to invoke the behavior, whether it’s a method call, HTTP request, or query.

  
**Action Steps:**

• Call the method under test with the prepared inputs.
• Avoid performing multiple actions in a single test; each test should validate one behavior.

  

**Example Thought:**

_“I’ll call_ _calculateTotalPrice(order)_ _and store the result for validation.”_


#### **3. Assert (Verify the Outcome)**

  
**What to Think About:**

• **What is the expected outcome?** Consider both the return value and any side effects (e.g., database updates, interactions with other components).
• **How do I verify the outcome?** Use assertions to check that the actual results match expectations.

  

**Action Steps:**

• Use assertions (assertEquals, assertTrue, etc.) to validate the output.
• Verify interactions with mocks using Mockito’s verify().
• Validate edge cases like exceptions, empty inputs, or boundary conditions.


**Example Thought:**

_“The total price should be $90 after applying the 10% discount. I also need to verify that_ _DiscountService_ _was called once.”_


#### **Practical Example**


Let’s walk through the thought process for testing a service method:


**Code to Test**
```
public double calculateTotalPrice(Order order) {
    double discount = discountService.getDiscount(order.getId());
    return order.getPrice() - discount;
}
```


**Test in AAA**
```
@Test
void testCalculateTotalPrice_WithDiscount() {
    // Arrange
    Order order = new Order(1, 100.0);
    when(discountService.getDiscount(1)).thenReturn(10.0);  // Mock behavior
    
    // Act
    double totalPrice = orderService.calculateTotalPrice(order);
    
    // Assert
    assertEquals(90.0, totalPrice, 0.01);  // Assert result
    verify(discountService, times(1)).getDiscount(1);  // Verify interaction
}
```

**Final Thought Process**

• **Clarity:** Ensure each section is concise and focused.
• **One Responsibility:** A single test should validate one behavior.
• **Edge Cases:** What happens if the input is null or empty? What if an exception is thrown?
• **Readability:** Write tests so they’re easy to understand for someone unfamiliar with the code.



# Part 1

Week 4 Lab Bug: 

Failure inducing input:

    @Test 
    public void testReverseInPlace2(){
      int[] input={1,2,3,4};
      ArrayExamples.reverseInPlace(input);
      assertArrayEquals(new int[]{4,3,2,1}, input);
    }

  was expected to reverse in place the input array to the array {4,3,2,1} but instead changed the array to {4,3,3,4}.
  
Non-failure input:

    @Test 
  	public void testReverseInPlace() {
      int[] input1 = { 3 };
      ArrayExamples.reverseInPlace(input1);
      assertArrayEquals(new int[]{ 3 }, input1);
  	}

 did not change the input array, which was the expected behavior.

# Part 1: Week 4 Lab Bug

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

 Symptom:
 <img width="614" alt="image" src="https://github.com/wangharold001/cse15l-report3/assets/60553459/c5249d79-eaef-42b3-b87b-daa419822cd2">

 Shows that the program failed the test with array of size 4, while passing the test with array of size 1. I also printed the contents of the failed test to the terminal, which resulted in the output "4334".

 The bug:
 
 Original code: 

      static void reverseInPlace(int[] arr) {
        for(int i = 0; i < arr.length; i += 1) {
          arr[i] = arr[arr.length - i - 1];
        }
      }

Fixed code: 

      static void reverseInPlace(int[] arr) {
        for(int i = 0; i < arr.length/2; i += 1) {
          int temp=arr[i];
          arr[i] = arr[arr.length - i - 1];
          arr[arr.length-i-1]=temp;
        }
      }

Explanation:
The first reason the code was buggy was that the initial values in the array were being replaced without a swapping. As a result, the values for the first half of the array were lost and did not appear in the resultant array. The other reason is that the for-loop was traversing through the entire list. So, even if the code swapped the values correctly, they would have been swapped back in the second half of the array. I changed the code so that it only traverses half of the array, swapping the first half of the array with its "mirror" in the second half.

# Part 2: Researching Commands

The grep command returns the results of a search for a RegEx pattern in a directory.

The -h command prints out the lines from a document or a directory that match the RegEx expression. This can be used as a "Ctrl+F" to find expressions and sentences containing relevant words in a document.

    root@DESKTOP-HTAG1J5:/mnt/d/ucsd/y2q1/cse 15l/technical/911report# grep -h "documents" chapter-5.txt
                    to use Yemeni documents to fly to Malaysia, then proceed to the United States using
                        evidenced by documents and diskettes seized by German authorities after
                Once again, the need for travel documents dictated al Qaeda's plans.
                    schemes to keep the pipeline of fraudulent documents flowing. To this end, al Qaeda
                The operational mission training course taught operatives how to forge documents.

    root@DESKTOP-HTAG1J5:/mnt/d/ucsd/y2q1/cse 15l/technical/911report# grep -h -r "fraudulent"
                2002. Al Qaeda also relied on outside travel facilitators, including fraudulent
                operatives around the world by obtaining fraudulent documents, arranging visas (real
                marking suggests the need for further inquiry, it is not the kind of fraudulent
                Suqami and Abdul Aziz al Omari) presented passports manipulated in a fraudulent
                fraudulent features, but their passports have not been found so we cannot be sure.
                also entered with fraudulent documents but claimed political asylum and was
                and other benefits systems did not effectively deter fraudulent applicants.
                schemes to keep the pipeline of fraudulent documents flowing. To this end, al Qaeda
            Following a familiar terrorist pattern, Ressam and his associates used fraudulent
                name. Under questioning, Ressam admitted the passport was fraudulent and claimed
                Haouari provided fraudulent passports and visas to assist Ressam and Meskini's
                Ressam presented officials with his genuine but fraudulently obtained Canadian
                to Jordan, having been convicted after 9/11 in a fraudulent driver's license
                plane ticket to Malaysia and a fraudulent Saudi passport to use for the trip. KSM

In this second example, we used the -r command in conjunction to traverse the entire directory.


The -l command returns a list of relevant files containing the ReGex. This can be useful if we'd like to traverse file names for specific content, or just read the entire file if it contains a certain string.

    root@DESKTOP-HTAG1J5:/mnt/d/ucsd/y2q1/cse 15l/technical/911report# grep -l -r "fraudulent"
    chapter-13.4.txt
    chapter-13.5.txt
    chapter-3.txt
    chapter-5.txt
    chapter-6.txt
    chapter-7.txt
    
    root@DESKTOP-HTAG1J5:/mnt/d/ucsd/y2q1/cse 15l/technical/911report# grep -l -r "Ladin"
    chapter-10.txt
    chapter-11.txt
    chapter-12.txt
    chapter-13.2.txt
    chapter-13.3.txt
    chapter-13.4.txt
    chapter-13.5.txt
    chapter-2.txt
    chapter-3.txt
    chapter-5.txt
    chapter-6.txt
    chapter-7.txt
    chapter-8.txt

The -A n, where n is a number, command prints both the matching line and n lines after. This command can be useful if we are also interested in the contents of a file after a certain expression appears.

    root@DESKTOP-HTAG1J5:/mnt/d/ucsd/y2q1/cse 15l/technical/911report# grep -A 3 -r "flight schools in"
    chapter-5.txt:                also researched flight schools in Europe, and in the Netherlands he met a flight
    chapter-5.txt:                school director who recommended flight schools in the United States because they
    chapter-5.txt-                were less expensive and required shorter training periods.
    chapter-5.txt-
    chapter-5.txt-            In March 2000, Atta emailed 31 different U.S. flight schools on behalf of a small
    --
    chapter-7.txt:                rejected by a Saudi flight school. He checked out flight schools in Florida,
    chapter-7.txt-                California, and Arizona; and he briefly started at a couple of them before returning
    chapter-7.txt-                to Saudi Arabia. In 1997, he returned to Florida and then, along with two friends,
    chapter-7.txt-                went back to Arizona and began his flight training there in earnest. After about

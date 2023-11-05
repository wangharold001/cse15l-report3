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

The -h command prints out the lines from a document or a directory that match the RegEx expression without displaying the file name. This option is useful if all of the files in a directory are from a similar source, or if we are only traversing through one file. This can be used as a "Ctrl+F" to find expressions and sentences containing relevant words in a document. I read about this option for the grep command from the geeksforgeeks webpage https://www.geeksforgeeks.org/grep-command-in-unixlinux/#.

    root@DESKTOP-HTAG1J5:/mnt/d/ucsd/y2q1/cse 15l/technical/911report# grep -h "documents" chapter-5.txt
                    to use Yemeni documents to fly to Malaysia, then proceed to the United States using
                        evidenced by documents and diskettes seized by German authorities after
                Once again, the need for travel documents dictated al Qaeda's plans.
                    schemes to keep the pipeline of fraudulent documents flowing. To this end, al Qaeda
                The operational mission training course taught operatives how to forge documents.

In  this first example, we used grep on the chapter-5 file to look for what it discusses about "documents". The -h command is useful since we already know what the file name will be.

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

In this second example, we used the -r command in conjunction to traverse the entire directory. This command was useful since we were interested in what the 911report files had to say about fraudulent activities.


The -l command returns a list of relevant files containing the ReGex. This can be useful if we'd like to traverse file names for specific content, or just read the entire file if it contains a certain string. I read about this option for the grep command from the geeksforgeeks webpage https://www.geeksforgeeks.org/grep-command-in-unixlinux/#.

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

The -A n, where n is a number, command prints both the matching line and n lines after. This command can be useful if we are also interested in the contents of a file after a certain expression appears. I read about this option for the grep command from the geeksforgeeks webpage https://www.geeksforgeeks.org/grep-command-in-unixlinux/#.


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


    root@DESKTOP-HTAG1J5:/mnt/d/ucsd/y2q1/cse 15l/technical/911report# grep -A 5 -r "NSLU"
    chapter-13.5.txt:            81. FBI email, Jane to Steve, NSLU Response, Aug. 29, 2001." Jane" says she only
    chapter-13.5.txt-                asked whether there was sufficient probable cause to open the matter as a criminal
    chapter-13.5.txt-                case and whether the criminal agent could attend any interview if Mihdhar was found.
    chapter-13.5.txt-                She said the answer she received to both questions was no. She did not ask whether
    chapter-13.5.txt-                the underlying information could have been shared. Jane interview ( July 13, 2004).
    chapter-13.5.txt:                The NSLU attorney denies advising that the agent could not participate in an
    chapter-13.5.txt-                interview and notes that she would not have given such inaccurate advice. The
    chapter-13.5.txt-                attorney told investigators that the NSA caveats would not have precluded criminal
    chapter-13.5.txt-                agents from joining in any search for Mihdhar or from participating in any
    chapter-13.5.txt-                interview. Moreover, she said that she could have gone to the NSA and obtained a
    chapter-13.5.txt-                waiver of any such caveat because there was no FISA information involved in this
    --
    chapter-13.5.txt:            82. FBI emails between Steve B. and Jane, re: NSLU Response, Aug. 29, 2001. While the
    chapter-13.5.txt-                agent expressed his frustration with the situation to "Jane," he made no effort to
    chapter-13.5.txt-                press the matter further by discussing his concerns with either his supervisor or
    chapter-13.5.txt-                the chief division counsel in New York.
    chapter-13.5.txt-            83. Attorney General Ashcroft testified to us that this and similar
    chapter-13.5.txt-                information-sharing issues arose from Attorney General Reno's 1995 guidelines,
    --
    chapter-8.txt:                (NSLU) on whether he could open a criminal case on Mihdhar.
    chapter-8.txt-
    chapter-8.txt:                "Jane" sent an email to the Cole case agent explaining that according to the NSLU,
    chapter-8.txt-                the case could be opened only as an intelligence matter, and that if Mihdhar was
    chapter-8.txt-                found, only designated intelligence agents could conduct or even be present at any
    chapter-8.txt-                interview. She appears to have misunderstood the complex rules that could apply to
    chapter-8.txt-                this situation.

The -n line includes the line numbers when printing out matching lines. This can be useful if we are interested in a pattern exhibited by the frequency of words in a line. Another use case could be if a secret message is sent through the line numbers of a certain word! I read about this option for the grep command from the geeksforgeeks webpage https://www.geeksforgeeks.org/grep-command-in-unixlinux/#.


    root@DESKTOP-HTAG1J5:/mnt/d/ucsd/y2q1/cse 15l/technical/911report# grep -n -r "NSLU"
    chapter-13.5.txt:1008:            81. FBI email, Jane to Steve, NSLU Response, Aug. 29, 2001." Jane" says she only
    chapter-13.5.txt:1013:                The NSLU attorney denies advising that the agent could not participate in an
    chapter-13.5.txt:1033:            82. FBI emails between Steve B. and Jane, re: NSLU Response, Aug. 29, 2001. While the
    chapter-8.txt:733:                (NSLU) on whether he could open a criminal case on Mihdhar.
    chapter-8.txt:735:            "Jane" sent an email to the Cole case agent explaining that according to the NSLU

        root@DESKTOP-HTAG1J5:/mnt/d/ucsd/y2q1/cse 15l/technical# grep -n -r "regulatory action"
    government/Gen_Account_Office/d03419sp.txt:146:Sarbanes-Oxley Act of 2002 and other related regulatory actions
    government/Gen_Account_Office/d03419sp.txt:1155:their ability to take appropriate regulatory actions because
    government/Gen_Account_Office/June30-2000_gg00135r.txt:73:are, in general, those expected to have a regulatory action within
    government/Gen_Account_Office/June30-2000_gg00135r.txt:837:or organizations about impending regulatory actions. Passive
    government/Gen_Account_Office/og96011.txt:281:"significant regulatory action" within the meaning of Executive
    government/Gen_Account_Office/og96020.txt:120:planned regulatory action document that described the reason for
    government/Gen_Account_Office/og96022.txt:77:"significant regulatory action" under Executive Order 12866. Since
    government/Gen_Account_Office/og96022.txt:243:regulatory action." HUD staff advised that, after submission to
    government/Gen_Account_Office/og96023.txt:170:The rule was determined to be a "significant regulatory action"
    government/Gen_Account_Office/og96023.txt:175:supplied by the Departments, including a planned regulatory action
    government/Gen_Account_Office/og96026.txt:52:significant regulatory action" under terms of Executive Order
    government/Gen_Account_Office/og96026.txt:216:"economically significant regulatory action" within the meaning of
    government/Gen_Account_Office/og96027.txt:191:"significant regulatory action" within the meaning of Executive
    government/Gen_Account_Office/og96038.txt:237:The rule was determined to be a "significant regulatory action"
    government/Gen_Account_Office/og96038.txt:242:information supplied by FDA, including a planned regulatory action
    government/Gen_Account_Office/og96038.txt:259:Federal agencies to examine regulatory actions to determine if they
    government/Gen_Account_Office/og96041.txt:291:an economically significant regulatory action under Executive Order
    government/Gen_Account_Office/og96042.txt:164:"significant regulatory action." The Office of Information and
    government/Gen_Account_Office/og96042.txt:167:EPA, including a planned regulatory action document describing the
    government/Gen_Account_Office/og96045.txt:184:"significant regulatory action." The Office of Information and
    government/Gen_Account_Office/og97003.txt:129:regulatory action for an additional year on the design control
    government/Gen_Account_Office/og97003.txt:192:regulatory action" under Executive Order No. 12866 requiring review
    government/Gen_Account_Office/og97003.txt:196:supplied by the FDA, including a planned regulatory action document
    government/Gen_Account_Office/og97023.txt:125:regulatory action" by OMB under Executive Order No. 12866 and was
    government/Gen_Account_Office/og97023.txt:128:information supplied by SSA, including a planned regulatory action
    government/Gen_Account_Office/og97032.txt:141:The interim rule is considered a "significant regulatory action"
    government/Gen_Account_Office/og97032.txt:147:supplied by INS, including a planned regulatory action document
    government/Gen_Account_Office/og97038.txt:145:significant" regulatory action by OMB under Executive Order No.
    government/Gen_Account_Office/og97038.txt:147:supplied by HHS, including a planned regulatory action document
    government/Gen_Account_Office/og97039.txt:182:regulatory actions by OMB under Executive Order No. 12866. As such,
    government/Gen_Account_Office/og97039.txt:184:Departments, which included planned regulatory action documents
    government/Gen_Account_Office/og97041.txt:201:"significant regulatory action." The agency reports that any
    government/Gen_Account_Office/og97043.txt:179:regulatory action" under Executive Order 12866 and was reviewed by
    government/Gen_Account_Office/og97045.txt:148:Order 12866 as a "significant regulatory action." The agency
    government/Gen_Account_Office/og97050.txt:102:that this was an "economically significant regulatory action" under
    government/Gen_Account_Office/og97050.txt:162:regulatory action under Executive Order 12866 because it could
    government/Gen_Account_Office/og97051.txt:159:regulatory action" under Executive Order 12866. In accordance with
    government/Gen_Account_Office/og97052.txt:168:regulatory action" under Executive Order No. 12866 and was reviewed
    government/Gen_Account_Office/og98022.txt:191:regulatory actions by OMB under Executive Order No. 12866. As such,
    government/Gen_Account_Office/og98022.txt:193:Departments, which included planned regulatory action documents
    government/Gen_Account_Office/og98024.txt:132:significant" regulatory action under the Executive Order and was
    government/Gen_Account_Office/og98030.txt:127:significant" regulatory action by the Office of Management and
    government/Gen_Account_Office/og98032.txt:143:significant" regulatory action by the Office of Management and
    government/Gen_Account_Office/og98041.txt:129:significant" regulatory action under Executive Order No. 12866 and
    government/Gen_Account_Office/og98044.txt:127:significant" regulatory action by the Office of Management and
    government/Gen_Account_Office/og98045.txt:168:significant" regulatory action by the Office of Management and
    government/Gen_Account_Office/og98046.txt:136:significant" regulatory action under the Order. It was reviewed by




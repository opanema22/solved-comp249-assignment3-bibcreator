Download Link: https://assignmentchef.com/product/solved-comp249-assignment3-bibcreator
<br>
The purpose of this assignment is to allow you practice Exception Handling, and File I/O, as well as other previous object-oriented concepts.

<strong>J</strong>ava<strong>S</strong>cript <strong>O</strong>bject <strong>N</strong>otation or <strong>JSON</strong> is a well-known, lightweight data-interchange format, which is easily readable/writable by humans [<a href="https://www.json.org/">1</a><a href="https://www.json.org/">]</a><a href="https://en.wikipedia.org/wiki/JSON">[</a><a href="https://en.wikipedia.org/wiki/JSON">2</a><a href="https://en.wikipedia.org/wiki/JSON">]</a>. It is also easy for machines to parse and generate. JSON is based on data objects consisting of attribute–value pairs and array data types. It is widely used for asynchronous browser–server communication, including as a replacement for XML in some AJAX-style systems. As such,  many journals and scientific servers are supporting this format. This format is easily extendable. The following is a typical sample (modified from an existing IEEE paper).

@ARTICLE{

8247289,

author={J. Park and J. N. James and Q. Li and Y. Xu and W. Huang},  journal={IEEE Transactions on Vehicular Technology},  title={Optimal DASH-Multicasting over LTE},  year={2018},  volume={PP},  number={99},  pages={15-27},  keywords={Forward error correction;Long Term Evolution;Maintenance engineering;Multicast communication;Resource management;Static VAr compensators;Streaming media;DASH;LTE;convex optimization;eMBMS;multicasting},  doi={10.1109/TVT.2018.2789899},  ISSN={0018-9545},

month={January},

}




In JSON, the fields however do not need to be placed in specific order. For example, in the above example, you can have the “number” filed for instance, be written above the “year” field, and so on.




There are many parsers available for JSON developed in may programming language as library, API, etc. Mendeley [<a href="https://www.elsevier.com/solutions/mendeley">3</a><a href="https://www.elsevier.com/solutions/mendeley">]</a> is one example that uses this format. With Mendeley you can create your own library from all articles that you have read so far and you can use them when you want to write an article. Consequently, this is very good for inserting the needed references on a published paper and managing them afterwards. In particular, such tools can import the article(s) information from a bibliography file (.bib) and generate the reference(s) in particular format according to the conference or journal publisher standard.




For example, the representation of this file in IEEE format would be (this is a slightly simplified version than the actual one; however you need to follow this format for the scope of this assignment):

<ol start="2018">

 <li>Park, J. N. James, Q. Li, Y. Xu, W. Huang. “Optimal DASH-Multicasting over LTE”, IEEE Transactions on Vehicular Technology, vol. PP, no. 99, p. 15-27, January 2018.</li>

</ol>




Or in <strong>ACM</strong> format would be:




[1] J. Park et al. 2018. Optimal DASH-Multicasting over LTE. IEEE Transactions on Vehicular Technology. PP, 99 (2018), 15-27. DOI:https://doi.org/10.1109/TVT.2018.2789899.




And finally, in <strong>Nature Journal (NJ)</strong>, which is one of the most famous journals in natural science, would be

<ol>

 <li>Park &amp; J. N. James &amp; Q. Li &amp; Y. Xu &amp; W. Huang. Optimal DASH-Multicasting over LTE. IEEE Transactions on Vehicular Technology. PP, 15-27(2018).</li>

</ol>




You should have a “<u>very</u>” detailed look at these formats to see how they are mapped from the original record of the article.




In this assignment, you will be designing and implementing an alternative tool (to the existing ones), called <strong><em>BibliographyFactory</em></strong>. The main task of this tool is read and process a given .bib file (which has one or more articles) and create <strong>3</strong> different files with the correct reference formats for IEEE, ACM and NJ.




<u>In short</u>, you are given 10 files, called <em>Latex1.bib</em> to <em>Latex10.bib</em>. You BibliographyFactory application will need to read all 10 input files (in one execution), determine whether each of these files is valid or not (details given below). If a file is valid, then BibliographyFactory will create 3 different files based on the articles in this file, one for IEEE format, one for ACM format and the last for NJ format. To distinguish our application from other existing similar software, we will call these files IEEE<strong><em>i</em></strong>.json, ACM<strong><em>i</em></strong>.json, and NJ<strong><em>i</em></strong>.json (although in fact, the created files contain the references to the articles, and not json records!), where <strong><em>i</em> </strong>is the Latex file #. For instance, Latex3.bib will result in the creation of 3 files called: IEEE3.json, ACM3.json and NJ3.json. If a file is invalid, then none of the 3 output reference files (for this invalid file) is created. So, in best case, BibliographyFactory execution will result in the creation of 30 output files if all given Latex files are valid, and in worst case it will create 0 files (when all 10 input files are invalid).




The fine details of what you need to do and how your BibliographyFactory should work are given below.




<ol>

 <li>For the purpose of this assignment, and to provide little simplifications, the following should be assumed in relation to the input files and the articles (records) in these input file:

  <ol>

   <li>Each file may have one or more articles; the number is unknown before processing, and your code must assume that;</li>

   <li>An article starts with @ARTICLE followed by the body of the article (between “{“ and</li>

  </ol></li>

</ol>

“}”). It is assumed that all articles have enclosing bodies;

<ol>

 <li>Inside each of these articles, there exists few fields; i.e. author, volume, year, etc. These fields are assumed to always start with the field name, followed by an “=” sign and a “{“ character. For instance: pages={ , month= , etc.</li>

 <li>It also assumed that each of the bodies of these fields have a closing character for its body. In specific, it is assumed that each of these fields end with “},”;</li>

 <li>For simplicity, it is also assumed that there is a doi field, which maps to <a href="https://doi.org/">https://doi.org/</a></li>

 <li>The order of the article is NOT important. i.e., it is okay to have any of these fields above or below other fields;</li>

 <li>It is also assumed that empty lines can be there within the body of the articles, as well as between different articles;</li>

 <li><u>HOWEVER</u> (read carefully), any of the input files may have some of these fields as empty; i.e. number={}, title={}, etc. <u>This is what we classify as an Invalid File</u>. In other words, for a file to be valid, the file cannot have an empty field at any of its articles. Below is an image of an invalid file.</li>

</ol>




Figure 1. Example of an Invalid Input File







<ol start="2">

 <li>Write an exception class called <strong>FileInvalidException</strong> The class should have sufficient constructors allow:</li>

 <li>A default error message “<em>Error: Input file cannot be parsed due to missing information </em></li>

</ol>

<em>(i.e. month={}, title={}, etc</em>.) “ to be stored in the thrown object; and

<ol>

 <li>The passing of any different error message if desired. This is actually the constructor that you will be using throughout the assignment (see Figure 3 below).</li>

</ol>




<ol start="3">

 <li>In the main() method of the BibilographyFactory class, attempt to open all 10 input files (Latex1.bib to Latex10.bib) for reading. You need to use the <strong>Scanner</strong> class for the reading these files. If “any” of these files does not exist, the program must display an error message indicating “<em>Could not open input file xxxxx for reading. Please check if file exists! Program will terminate after closing any opened files.</em>”, and then exits. You <u>MUST</u> however, close all opened files before exiting the program. For example, if <em>bib</em> does not exist, then the following image shows the behavior of the program.</li>

</ol>







Figure 2. Example of Program Termination – One of the Input Files does not Exist




<ol start="4">

 <li>If all 10 input files can successfully be opened, the program will attempt to open/create all 30 output files (IEEE1.json to IEEE10.json, ACM1.json to ACM10.json, and NJ1.json to NJ10.json). You need to use PrintWriter to open these output files. If “any” of these output files cannot be created, then you must:

  <ol>

   <li>Display a message to the user indicating which file could not be opened/created;</li>

   <li>Delete all other created output files (if any). That is, if you cannot create all of these output files, then you must clean the directory by deleting all other created files;</li>

   <li>Close all opened input files; then exit the program.</li>

  </ol></li>

</ol>




If you reach this step, then all 10 input files have been opened and all 30 output files have also been created (however, they are surely empty).




<ol start="5">

 <li>Write a method (you should take advantage of static throughout the entire assignment!) called <strong>processFilesForValidation</strong>. This method will represent the core engine for processing the input files and creating the output ones. You can pass any needed parameters to this method, and the method may return any needed information. This method however must NOT declare any exceptions. In other words, all needed handling of any exceptions that may occur within this method, must be handled by the method. In specific:

  <ol>

   <li>The method should work on the already opened files;</li>

   <li>A method must process each of these files to find out whether it is valid or not;</li>

   <li>If a file is valid, then the method must create the proper records for each of the 3 formats</li>

  </ol></li>

</ol>

(IEEE, ACM and NJ) and store them in these files;

<ol>

 <li>If a file is invalid, then the method must stop the processing of this file only, throws <strong>FileInvalidException</strong> to display the exception error message, then display a message indicating which file was detected as invalid, and where the “first” problem in that file was detected (See Figure 3). The corresponding output file <u>MUST</u> then be deleted;</li>

 <li>The method will then continue with the processing of the following file.</li>

</ol>







For instance, let us assume that the given input files (these files can be any files and they are not restricted to the ones provided with the assignment; in fact, the marker will execute your assignment with different files; so your code must work correctly for any given files) have 3 invalid files, Latex3.bib, Latex4.bib and Latex8.bib. Your program must detect these invalid files and show the following:







Figure 3. Example of Processing – Number of Invalid Files and Particular Fields are Indicated







<ol start="6">

 <li>Again, once the processing is done, all unsuccessfully created files MUST be deleted. Here is how the directory would look like at this point based on the above senario:</li>

</ol>







Figure 4. Contents of Current Directory after above processing Example




<ol start="7">

 <li>Finally, at this point, the program needs to ask the user to enter the name of one of the created output files to display. If the user enters an invalid name, a FileNotFoundException should be thrown; however, the user is allowed a second and final chance to enter another name. If this second attempt also fails, then the program exits. Figure 5 and Figure 6 below show the behavior of this program. You must however apply the following:</li>

</ol>

– If the entered file is valid, then your program must open this file for reading using the <strong>BufferedReader</strong> class. Do not use the Scanner class to read the file for that task.




<ol start="8">

 <li>Finally, here are some general information:

  <ol>

   <li>It may assist you greatly if you take advantage of static variables/attributes and static attributes throughout the assignment; in fact, it is not necessary to utilize other aspects such as Inheritance, Polymorphism, etc.</li>

   <li>You must exactly match the format and look of the expected output files. For instance, use &amp; or et al. for the authors as expected, follow the exact order/format of the contents, use vol. instead of volume when as expected. In other words, a small difference in the expected output will surely result in mark deduction;</li>

   <li>For the processing of the authors, you may want to use the <strong>StringTokenizer</strong> class;</li>

   <li><u>You should minimize opening and closing the files as much as possible; a better mark</u> <u>will be given for that</u>;</li>

   <li>Do not use any external libraries or existing software to produce what is needed; that will directly result in a 0 mark!</li>

   <li>Again, your program must work for any input files. The files provided with this assignment are only one possible version, and must not be considered as the general case when writing your code.</li>

   <li>To make sure that the requirments are very clear to you, Figure 7 given an image (partially) of a sample input file, and Figures 8, 9 &amp; 10 show the output of this sample file in the 3 formats. These files are also provided with the assignment.</li>

  </ol></li>

</ol>










Figure 5. Example of Double-Fault for Displaying an Output File













Figure 6. Example of Displaying the Contents of a Successfully Created Output File







Figure 7. Example of a Sample Bib Input File – Partial Image







Figure 8. The Created IEEE File for the above Sample Bib File







Figure 9. The Created ACM File for the above Sample Bib File







Figure 10. The Created Natural Journal File for the above Sample Bib File




<strong><u>General Guidelines When Writing Programs:</u></strong><strong>  </strong>

<ul>

 <li>Include the following comments at the top of your source codes</li>

</ul>

// —————————————————–

// Assignment (include number)

// Question: (include question/part number, if applicable)

// Written by: (include your name and student ID)

// —————————————————–

<ul>

 <li>In a comment, give a general explanation of what your program does. As the programming questions get more complex, the explanations will get lengthier.</li>

 <li>Include comments in your program describing the main steps in your program.</li>

 <li>Display a welcome message which includes your name(s).</li>

</ul>




<ul>

 <li>Display clear prompts for users when you are expecting the user to enter data from the keyboard.</li>

 <li>All output should be displayed with clear messages and in an easy to read format.</li>

 <li>End your program with a closing message so that the user knows that the program has terminated.</li>

</ul>

<strong> </strong>

<strong><u>JavaDoc Documentation:</u></strong>

Documentation for your program must be written in <strong>javaDoc</strong>. In addition, the following information must appear at the top of each file:




Name(s) and ID(s)    (include full names and IDs)

COMP249

Assignment #   (include the assignment number) Due Date     (include the due date for this assignment)
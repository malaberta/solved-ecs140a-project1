Download Link: https://assignmentchef.com/product/solved-ecs140a-project1
<br>
This project specification is subject to change at any time for clarification. For this project you will be writing several Java classes to implement a programming language scanner and a CSV parser. The classes developed in this project will be used in subsequent projects. A Token class has been provided for you and an interface the Scanner will rely on for input has also been provided. The Scanner class must take in a PeekableCharacterStream and a List of keywords and must produce a stream of Tokens that are queried from either peekNextToken or getNextToken methods. The rules for the tokens defined below. You will also develop the CSVParser class that will parse CSV files into Maps, one for each row.

Your first task is to develop a class that implements the PeekableCharacterStream interface for a FileInputStream.

<strong>public</strong> <strong>interface</strong> PeekableCharacterStream{

// Returns true if more characters are available, false otherwise     <strong>public</strong> <strong>boolean</strong> moreAvailable();




// Returns the next character that would be returned without consuming

// the character. If no more characters are available -1 is returned.     <strong>public</strong> <strong>int</strong> peekNextChar();




// Returns the character ahead in the stream without consuming the

// the character. peekAheadChar(0) returns the same character as

// peekNextChar(). If no more characters are available at that position

// -1 is returned.     <strong>public</strong> <strong>int</strong> peekAheadChar(<strong>int</strong> ahead);




// Returns the next character and consumes it. If no more characters are

// available -1 is returned.     <strong>public</strong> <strong>int</strong> getNextChar();




// Closes the stream.     <strong>public</strong> <strong>void</strong> close(); }

Your second task is to develop the Scanner class that will rely on the PeekableCharacterStream interface and the Token class. The Scanner must have the following minimal interface.

<strong>public</strong> <strong>class</strong> Scanner{

// Constructor that takes in a stream and a list of keywords.

<strong>public</strong> Scanner(PeekableCharacterStream stream, List&lt;String&gt; keywordlist);

// Returns the next token without consuming it. If no more tokens are

// available a None token is returned.

<strong>public</strong> Token peekNextToken();




// Returns the next token and consumes it. If no more tokens are

// available a None token is returned.

<strong>public</strong> Token getNextToken();

}

<strong>Token Rules: </strong>

Identifier := ( <strong>_</strong> | <em>Alpha</em> ) { ( <strong>_</strong> | <em>Digit</em> | <em>Alpha</em> )  }

Operator := <strong>(</strong> | <strong>,</strong> |<strong> )</strong> | <strong>{</strong> | <strong>}</strong> | <strong>=</strong> | <strong>==</strong> | <strong>&lt;</strong> | <strong>&gt;</strong> | <strong>&lt;=</strong> | <strong>&gt;=</strong> | <strong>!=</strong> | <strong>+</strong> | <strong>–</strong> | <strong>*</strong> |

<strong>/</strong> | <strong>;</strong>  <strong> </strong>

IntConstant := [ <strong>–</strong> ] <em>Digit</em> { <em>Digit</em> }

FloatConstant := [ <strong>–</strong> ] <em>Digit</em> { <em>Digit</em> } [ <strong>.</strong> <em>Digit</em> { <em>Digit</em> } ]

StringConstant := <strong>“</strong> { ( CharacterLiteral | EscapedCharacter ) } <strong>“</strong>

Digit := <strong>0</strong> – <strong>9 </strong>

Alpha := <strong>A</strong> – <strong>Z</strong> | <strong>a</strong> – <strong>z </strong>

WhiteSpace := <em>Space</em> | <em>Tab</em> | <em>CarriageReturn</em> | <em>NewLine</em>

CharacterLiteral := <em>Space</em> – <strong>!</strong> | <strong>#</strong> – <strong>[</strong> | <strong>]</strong> – <strong>~</strong> EscapedCharacter := <strong>b</strong> | <strong>
</strong> | <strong>r</strong> | <strong>t</strong> | <strong>\</strong> | <strong>’</strong> | <strong>”</strong>

<strong>Additional Tokenizing Rules: </strong>

<ul>

 <li>Keywords are identifiers that are in the List provided to the Scanner.</li>

 <li>Whitespace must be skipped during the tokenizing.</li>

 <li>A negative sign immediately preceding an integer or float constant must be tokenized as an operator if the previous token was a constant or identifier. For example, “A -5” must be tokenized as Identifier “A”, Operator “-”, and IntConstant “5”, not as Identifier “A”, and IntConstant “-5”.</li>

 <li>If an underscore or Alpha character immediately follows a constant, the token is considered Invalid. All Alpha, Digit, and underscore characters will be part of the Invalid token.</li>

 <li>If an invalid character is in a string constant, the characters are consumed until the next non-escaped ” is reached or the end of stream is reached. The token type is considered Invalid.</li>

 <li>Any invalid character beginning a token will be considered an Invalid token by itself. For example, “@#4” must be tokenized as Invalid “@”, Invalid “#”, and IntConstant “4”.</li>

</ul>

<strong>Implementation Requirements: </strong>

<ul>

 <li>You may use java.io.FileInputStream.</li>

 <li>You may use java.util.Set, java.util.HashSet, java.util.Arrays and similar containers.</li>

 <li>You may <strong>not</strong> use java.util.regex or similar packages.</li>

 <li>You may <strong>not</strong> use java.util.StringTokenizer or similar library classes.</li>

</ul>

Your final task is to develop the CSVParser class that will rely on the PeekableCharacterStream interface. The CSVParser must have the following minimal interface.

<strong>public</strong> <strong>class</strong> CSVParser{

// Constructor that takes in a stream.

<strong>public</strong> CSVParser(PeekableCharacterStream stream);




// Returns the next row without consuming it. If no more rows are

// available null is returned.

<strong>public</strong> Map&lt;String,String&gt; peekNextRow();




// Returns the next row and consumes it. If no more rows are

// available null is returned.

<strong>public</strong> Map&lt;String,String&gt; getNextRow();

}




<strong>CSV Format Rules </strong>

<ul>

 <li>CSV files must have a header row, and no column in the header may be repeated or empty.</li>

 <li>Each row is terminated by a newline character.</li>

 <li>Each column is terminated by a comma character.</li>

 <li>Any whitespace (space, tab, carriage return, or newline) character that is part of a column must be a double quoted ” column. The escape sequence for a double quote in a double quoted column is two double quotes in a row.</li>

 <li>Any empty columns or missing columns will return a value of null for the corresponding value in the returned Map.</li>

 <li>Valid CSV files are not allowed to have more columns in a data row than the header row but may have fewer.</li>

</ul>




Your Scanner and CSVParser classes must have a main function that takes in a filename as an argument and outputs the contents similar to the examples in /home/cjnitta/ecs140a/proj1 on the CSIF. You can run the provided solutions by running the shell scripts Scanner.sh or CSVParser.sh and providing a filename to open. Your code will be tested on the CSIF and is expected to compile and run on the CSIF.




You <strong>must</strong> submit the source file(s), a Makefile, and README.txt file, in a tgz archive.  Do a make clean prior to zipping up your files so the size will be smaller. You will want to be in the parent directory of the project directory when creating the tgz archive. You can tar gzip a directory with the command:

tar -zcvf archive-name.tgz directory-name
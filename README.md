Download Link: https://assignmentchef.com/product/solved-cps2000-assignment-part-1-and-2
<br>
PART 1

In this assignment you are to develop a lexer, parser, semantic analyser and interpreter for the programming language – TeaLang. This part of the assignment is composed of three major components: i) design and implementation of a FSA-based table-driven lexer and hand-crafted top-down LL(k) parser, ii) visitor classes to perform XML generation, semantic analysis and interpreter execution on the abstract syntax tree (AST) produced by the top-down parser and iii) a report detailing how you designed and implemented the different tasks.

TeaLang is an expression-based strongly-typed programming language. The language has C-style comments, that is, //… for line comments and /*…*/ for block comments. The language is case-sensitive and each function is expected to return a value. TeaLang has 4 primitive types: ‘float’, ‘int’, ‘bool’ and ‘string’. Binary operators, such as ‘+’, require that the operands have matching types; the language does not perform any implicit/automatic typecast. The following is a syntactically and semantically correct TeaLang program:

float              Square (x : float ) {

return x∗x ;

}

bool XGreaterThanY(x : float , y : float ) {

let ans : bool = true ; i f (y &gt; x) { ans = false ; } return ans ;

}

bool XGreaterThanYv2(x : float , y : float )

return x &gt; y ;{

}

float                             AverageOfThree(x : float , y : float ,

let                total : float = x + y + z ;z : float ){return          total / 3;

}

string               JoinStr ( s1 : string ,                s2 : string ) {

let            s3 : string = s1 + s2 ;

return s3 ;

}

let x : float = 2.4; let y : float = Square (2.5); print y ;//6.25

print XGreaterThanY(x ,                    2.3);//true

print XGreaterThanYv2( Square (1.5) , y );// false

print AverageOfThree(x , y ,                        1.2);//3.28

print                 JoinStr (” Hello ” , ” World ”);//HelloWorldThe TeaLang programming languageThe following rules describe the syntax of TeaLang in EBNF. Each rule has three parts: a left hand side (LHS), a right-hand side (RHS) and the ‘::=’ symbol separating these two sides. The LHS names the EBNF rule whereas the RHS provides a description of this name. Note that the RHS uses four control forms namely sequence, choice, option and repetition. In a sequence order is important and items appear left-to-right. The stroke symbol ( …| …) is used to denote choice between alternatives. One item is chosen from this list; order is not important. Optional items are enclosed in square brackets ([ …]) indicating that the item can either be included or discarded. Repeatable items are enclosed in curly brackets ({ …}); the items within can be repeated zero or more times. For example, a Block consists of zero or more Statement enclosed in curly brackets.

Task BreakdownTask 1 – Table-driven lexerIn this first task you are to develop the lexer for the TeaLang language. The lexer is to be implemented using the table-driven approach which simulates the DFA transition function of the TeaLang micro-syntax. The lexer should be able to report any lexical errors in the input program.

Task 2 – Hand-crafted LL(k) parserIn this task you are to develop a hand-crafted predictive parser for the TeaLang language. The Lexer and Parser classes interact through the function GetNextToken() which the parser uses to get the next valid token from the lexer. Note that for the vast majority of cases, the parser only needs to read one symbol of lookahead (k=1) in order to determine which production rule to use. The parser should be able to report any syntax errors in the input program. A successful parse of the input should produce an abstract syntax tree (AST) describing the structure of the program.

Task 3 – AST XML Generation PassIn OOP programming, the Visitor design pattern is used to describe an operation to be performed on the elements of an object structure without changing the classes on which it operates. In our case this object structure is the AST (not the parse tree) produced by the parser in Task 2. For this task you are to implement a visitor class to output a properly indented XML representation of the generated AST. Please note that additional notes – with examples – on the Visitor design pattern are available on the VLE. Check those out before starting this task.

let x :                       float = 3.142 ∗ 20.0765;

&lt;Decl&gt;

&lt;Var Type=”float”&gt;x&lt;/Id&gt;

&lt;BinExprNode Op=”∗”&gt;

&lt;FloatConst &gt;3.142&lt;/FloatConst&gt;

&lt;FloatConst &gt;20.0765&lt;/FloatConst&gt;

&lt;/BinExprNode&gt; &lt;/Decl&gt;

Task 4 – Semantic Analysis PassFor this task, you are to implement another visitor class to traverse the AST and perform typechecking (e.g. checking that variables are assigned to appropriately typed expressions, variables are not declared multiple times in the same scope, etc.). In addition to the global program scope, local scopes are created whenever a block is entered and destroyed when control leaves the block. Note that blocks may be nested and that to carry out this task, it is essential to have a proper implementation of a symbol table. Your compiler should be able to report any semantic analysis errors resulting from the traversal on the AST. Note that whereas TeaLang allows for function definitions within local scope, for this task, function definitions need only be declared within the global scope. An important check carried out of the semantic analysis visitor is that of checking that a function always returns a value.

string OverUnder50( int : age ) { i f ( age &lt; 50) {

return ”Under Fifty ”;

}

else { return ”Over Fifty ”;

}

}

let x : int = 45;

while (x &lt; 50) { print OverUnder50(x ); \”Under

x = x + 1;Fifty”x5}

print OverUnder50(x );                             ”OverFifty”

\

Task 5 – Interpreter Execution PassFor this task, you are to implement another visitor class to traverse the AST and simulate an interpreter which executes the test program. The ′print′ &lt;Expression&gt; statement can be used in your test programs to output the value of &lt;Expression&gt; to the console and determine whether the computation carried out by the interpreter visitor is correct. Note that the symbol table now needs to be used to also store the values (in addition to type as was done with Task 4) of variables currently within scope.




PART 2

Over the years, TeaLang has grown in popularity and several developers started requesting additional features to improve the language and further increase its adoption amongst software houses. The highly anticipated new compiler is now due to be released around Q2 2021. Tea2Lang is expected to be a solid improvement over TeaLang and adds support for arrays, structs, the ‘auto’ type specifier and function overloading.

In this assignment you – the developer of the new Tea2Lang compiler – will be tasked with extending TeaLang (note that the specification of TeaLang can be found in Part I) into Tea2Lang. This assignment (Part II) is composed of three major components: i) modifications to the original TeaLang language specification, ii) extension of the Lexer/Parser and visitor classes for TeaLang to handle Tea2Lang features iii) a report detailing how you designed and implemented the different tasks. The following is a syntactically correct Tea2Lang program:

auto XGreaterY( int toCompare [ ] ) { let ans : auto = false ;

i f           (toCompare [0] &gt; toCompare [1])

{

ans = true ;

} return ans ;

}

auto XGreaterY( int x , int y) { i f (x&gt;y) { return true ; } else { return false ;

}}float Average( float toAverage [ ] , int let total : float = 0.0;count ) {

for      ( int        i = 0;         i&lt;count ;         i = i +1)

{

total = total + toAverage [ i ] ;

}

return           total / count ;

}

let           arr1 [ 2 ] : float ;

let                arr2 [ 4 ] : float = { 2.4 ,            2.8 ,       10.4 ,12.1 };

arr1 [0] = 22.4; arr1 [1] = 6.25; print arr1 [ 1 ] ;//6.25

printXGreaterY( arr1 );//true

printAverage( arr2 );//6.92

printXGreaterY (2 ,3);// false

Task BreakdownThe assignment is broken down into four tasks. Below is a description of each task with the assigned mark.

Task 1 – char type and ArraysIn this first task you are to extend TeaLang by adding another primitive type, ’char’, to represent individual characters and also include support for arrays. An array in Tea2Lang consists of a series of elements of the same type in contiguous memory that can be individually accessed using the indexing operator [ ] over the array identifier. By default arrays are left uninitialised when declared, i.e. element values are not individually set. The programmer has the option of initialising the elements in the array upon declaration. Check out the code fragments above for examples of how this can be done. Deviations from the syntax used in this code fragment are allowed as long as you support the required functionality. The following subtasks are included:

•    Update the EBNF grammar with new (or modified) rules to support arrays and ’char’ type.

•    Update the Lexer to generate the required new tokens.

•    Update the Parser to handle these new tokens.

•    Update the XML visitor to include ’char’ and arrays.

•    Update the Semantic Analysis visitor to support the new type and the use of arrays.

•    Update the Execution visitor to support evaluation of expression using ’char’ and arrays.

Task 2 – The ’auto’ typeTea2Lang supports the ‘auto’ type specifier both for variables and functions. Check out the code fragments above for examples. For variables it specifies that the type of the variable that is being declared will be automatically deduced from its initialiser. For functions it specifies that the return type will be deduced from its return statements. Note the ‘auto’ type specifier cannot be used to specify the type of the formal parameters in function declarations. The following subtasks are included:

•    Update the EBNF grammar with new (or modified) rules to support ’auto’.

•    Update the Lexer to generate the required new token.

•    Update the Parser to handle the new token.

•    Update the XML visitor to include ’auto’ types.

•    Update the Semantic Analysis visitor to support resolution of ’auto’ variables and functions.

•    Update the Execution visitor to support evaluation of expressions using ’auto’. Changes, if any, are minimal here since most of the work is done at the semantic analysis phase.

Task 3 – StructsStructs are user-defined data types in Tea2Lang. Unlike arrays, they allow programmers to combine data items of different primary data types under a single name. Each element in a struct is referred to as a member. In addition to data members (i.e. a normal Tea2Lang variable declaration), structures in Tea2Lang also support member functions. The structure is defined with the keyword ’tlstruct’ and all its members are public. The code below demonstrates how structs in Tea2Lang are used:

tlstruct                Vector {

let x : float = 0.0; let y : float = 0.0; let        z : float = 0.0;

int Scale ( float s ) { x = x ∗ s ; y = y ∗ s ; z = z ∗ s ;

return      0;               //Because           functionsalways returnsomething}

int Translate ( float tx , float x = x + tx ;ty ,float          tz ) {

y = y + ty ; z = z + tz ;

return      0;                   //Languagedoesnotsupport void

}

}

Vector Add( Vector v1 , let v3 : Vector ;Vectorv2){

v3 . x =v1 . x +v2 . x ;

v3 . y =v1 . y +v2 . y ;

v3 . z =v1 . z +v2 . z ;

returnv3 ;

}

let v1 : Vector : v1 . x = 1.0; v1 . y = 2.0; v1 . z = 2.0;

let v2 : Vector ; v2 . x = 2.0; v2 . y = 1.2; v2 . z = 0.0;

let               v3 : Vector = Add (v1 , v2 );

print v3 . x ;    // 3.0 print v3 . y ;      // 3.2 print v3 . z ;      // 2.0

v3 . translate (1.0 , 1.0 , 1.0); let v4 : Vector = Add (v1 , v3 );

print v3 . x ;    // 5.0 print v3 . y ;      // 6.2 print v3 . z ;      // 5.0The following subtasks are included:

•    Update the EBNF grammar with new (or modified) rules to support structures.

•    Update the Lexer to generate the required new tokens.

•    Update the Parser to handle these new tokens.

•    Update the XML visitor to include ’auto’ types.

•    Update the Semantic Analysis visitor to support additional semantic checks for structures.

•    Update the Execution visitor to support evaluation of programs using ’tlstruct’.

Task 4 – Function overloadingIn Tea2Lang, two functions can have the same name if the number and/or type of the arguments passed is different. This feature is referred to as function overloading. As far as the Lexer and Parser are concerned, no changes need to be carried out, however, the semantic analysis and execution visitors will now need to cater for this new feature. An example of function overloading is seen in the code examples (page 2). The function XGreaterY takes as argument both an array of int and two integers types. The following subtasks are included:

•    Update the Semantic Analysis visitor to support function overloading.

•    Update the Execution visitor to support evaluation of programs which include function overloading. Changes are minimal here since most of the work is done at the semantic analysis phase.
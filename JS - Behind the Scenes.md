![[image2.webp]] 


### Environment and Engine
A computer, compiler, or browser don't have any idea or understand code that is written in JS. This leaves us with the question, *how does the JS code run?*
Behind the scenes, *JS always run in ==**engine**==  which every environment has.*

These engine includes:
 - Chrome V8 (written in C++)
 - Firefox Spider Monkey
 - Safari JavaScript Core

While these engines work in a similar fashion, there are differences to note. It is also good to keep in mind that an engine is simple a ==*software*==. 

The first thing that a JS engine do after coming across written JS code is to ==check the code using the *parse*==.
*The parser understands JS **syntax and rules** and it's job is to go through the code one line at a time and check if it's correct.*
While the parser is running, if it comes across an error, it'll stop running, and send out an error.

However, if the code is correct, the *parser generates* something called the **Abstract Syntax Tree or AST** for shot.
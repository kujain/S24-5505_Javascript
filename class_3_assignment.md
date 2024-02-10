## Exercise: Creating flexible Functions

For this assignment, start with an assignment from the previous assignment or one of your decision tree black boxes (or create a new one if you like). For example, generating a triangle/chessboard pattern. Now rewrite that code and "refactor" it using functions, adding more flexibility and power to it through the use of parameters and callbacks where appropriate. Go crazy with it!

Then play around by tweaking the arguments so that by changing a few parameters, your function creates something unexpected and unique. Then put them together into a sequence of function calls, creating simple versions of "ASCII Art".

Here's an example of the above, using the triangle generator code.
```
let number = 1;
while (number <= 10) {
  let offset = 10 - number
  console.log(' '.repeat(offset) +  '#'.repeat(number));
  number++;
}
```
To convert this into a function, here's the first simple step:
```
function makeTriangle() {
    let number = 1;
    while (number <= 10) {
        console.log( '#'.repeat(number));
        number++;
    }
}
makeTriangle();
```
Now, to make this more flexible, we can make the number of rows into a parameter:
```
function makeTriangle( rows = 4 ) {
    let number = 1;
  while (number <= rows) {
        console.log( '#'.repeat(number));
        number++;
    }
}
makeTriangle(10);
makeTriangle(4);
makeTriangle(); // this still works using the default value of 4.

//We can also make that repeating pattern symbol into parameter!
function makeTriangle( rows = 4, pattern = '#' ) {
    let number = 1;
while (number <= rows) {
      console.log( pattern.repeat(number));
        number++;
    }
}
makeTriangle(10);
makeTriangle(4, '$');
makeTriangle(); // this still works using the default value of 4 and # as the patter.
```

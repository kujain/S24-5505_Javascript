## Assignment 1
#### Update the style of the first paragraph tag in the HTML to use a different font family, color and/or size.
```
const  my_p_elements = document.getElementsByTagName("p");

// get the first p elements
const my_p1 = my_p_elements[0];
my_p1.style.background = "rgb(255,0,0)";

// get the second p elements
const my_p2 = myBodyElements[1];
my_p2.style.background = "rgb(255,255,0)";
```

## Assignment 2
#### Add a new paragraph tag at the bottom of the "section" node.
```
const new_para = document.createElement('p');
new_para.textContent = "This is the end.\nThanks for watching";

// get the first section node and add inside it
const sect = document.getElementsByTagName('section')[0];
sect.appendChild(new_para);
```

## Assignment 3
#### Write code that, on click of a button, can choose a random image from unsplash and add it inside the section tag: �(you can use this url as the source: https://source.unsplash.com/random)
```
const an = document.getElementsByTagName('a')[0];

an.addEventListener("click", function(e){
  console.log('clicked on: a');
  e.preventDefault();

  const img = document.createElement('img');
  img.src = 'https://source.unsplash.com/random';

  // add image at the bottom of section
  let sect = document.getElementsByTagName('section')[0];
  sect.appendChild(img);
  e.preventDefault();
});
```

## Assignment 4
#### Create a table and paint alternative colors to its rows. here's the html Markup:
```
<table>
  <tr>
    <td>Cell 1:1</td>
    <td>Cell 2:1</td>
    <td>Cell 3:1</td>
    <td>Cell 4:1</td>
    <td>Cell 5:1</td>
  </tr>
  <tr>
    <td>Cell 1:2</td>
    <td>Cell 2:2</td>
    <td>Cell 3:2</td>
    <td>Cell 4:2</td>
    <td>Cell 5:2</td>
  </tr>
  <tr>
    <td>Cell 1:3</td>
    <td>Cell 2:3</td>
    <td>Cell 3:3</td>
    <td>Cell 4:3</td>
    <td>Cell 5:3</td>
  </tr>
  <tr>
    <td>Cell 1:4</td>
    <td>Cell 2:4</td>
    <td>Cell 3:4</td>
    <td>Cell 4:4</td>
    <td>Cell 5:4</td>
  </tr>
  <tr>
    <td>Cell 1:5</td>
    <td>Cell 2:5</td>
    <td>Cell 3:5</td>
    <td>Cell 4:5</td>
    <td>Cell 5:5</td>
  </tr>
</table>
```

```
// first assign the table and ID (or class or whatever to identify it)
let rows = document.querySelectorAll('#altColors tr');
for (let i = 0; i < rows.length; i++) {
  let row = rows[i];
  console.log(row);
  if ( i % 2 == 0 ) {
  	  row.style.backgroundColor = "green";
  }
}
```
Alternative 1 using the rows convenience selector (very legacy):
```
// alternative 1 using the rows convenience selector (very legacy)
// Note that if you are using an index to find the nth table in DOM, make sure it's selecting the correct one. eg. here I use 2 since in my html, this is the 3rd table.
let table = document.getElementsByTagName('table')[2];

// alt rows
for (let i = 0; i < table.rows.length; i++) {
  let row = table.rows[i];
  if ( i % 2 === 0 ) {
    row.style.backgroundColor = 'red';
  } else {
    row.style.backgroundColor = 'grey';
  }
}
```
Alternative 2 using query selector:
```
let table = document.getElementsByTagName('table')[2];
const trs = table.querySelectorAll('tr:nth-child(odd)');

// convery trs to array to use iterator
for( let tr of Array.from(trs) ) {
  tr.style.backgroundColor = 'purple';
}

```
------------------

## Class 4 Assignment solution:
```
/* This version uses a multi-dimensional array */
const my_ai = {
  myName: "HAL",
  myVersion: "0.0.1",
  myQuestions: [
     ["how are you", "getting better"],
     ["what is your name", "HAL"],
     ["why are you here", "sorry...that question needs pondering"]
    ],

  checkAnswer: function(q) {
    var q_length = this.myQuestions.length;
    // clean up question
    q = q.toLowerCase();
    if (q.substr(q.length-1) == "?" || q.substr(q.length-1) == ".") {
      q = q.substr(0,q.length-1);
    }

    for (let i=0; i < q_length; i++) {
      // console.log('current question set', this.myQuestions[i], q);

      if (this.myQuestions[i][0] == q.toLowerCase()) {
        return this.myQuestions[i][1];
      }
    }
    return "Sorry...I do not understand your question."
  }

}

let question = prompt('Ask your question');
let ans = my_ai.checkAnswer(question);
console.log(ans);
```

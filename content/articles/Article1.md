---
title: "Sorting A Table"
description: ""
omit_header_text: true
featured_image: images/7b6b442822c8ba56fb6ff82f7bf04f1f.jpg
summary: "Adding buttons to previously coded websites."
type: page
weight: 2
---


## Prepping for Assignment

For CSC 324, Fundamentals of Data Computing, at GC, we were given the following assignment titled "Sorting A Table' using VSCODE. 

The problem is described in full [here](https://homerhanumat.github.io/csc324resources/exercises/table-sort.html). For all homework problems for this course, we are required to push to our git repositories, which is noted in the link above. For this problem, we were given the task to build on a previous assignment titled Making-A-Table. The instructions and intent for this assignment is described [here](https://homerhanumat.github.io/csc324resources/exercises/table.html). However, my original submission for this problem was not ideal to build on, so I used Dr. White's key to complete Sorting A Table. 

<blockquote>
To begin, Dr. White gave us a custom.js file that defines an array called artists. This was the code we were given to add onto to create the two assignments that are discussed in the rest of this article. The code created an array that include 5 artists, their birth years, and a link to one of their youtube videos. For the array, the code included:

```js
 const artists = [
   {
     name: "Ms Scandalous",
     birthYear: 1985,
     link: "https://www.youtube.com/watch?v=2FPivlfvxu0"
   },
   {
    name: "Juggy D",
    birthYear: 1981,
    link: "https://www.youtube.com/watch?v=1jAc_-FVjdI"
  },
  {
    name: "Sukhbir Singh",
    birthYear: 1969,
    link: "https://www.youtube.com/watch?v=HiprNF9Jad0"
  },
  {
    name: "Abrar-ul-Haq",
    birthYear: 1989,
    link: "https://www.youtube.com/watch?v=-lnnVIP7FEc"
  },
  {
    name: "Rishi Rich",
    birthYear: 1970,
    link: "https://www.youtube.com/watch?v=O95-w2gACuA"
  }
];
```
</blockquote>

As I stated earlier, I copy and pasted Dr. White's code for `Table Assign` into my VSCODE to give a correct and buildable foundation to continue for this assignment.  In the remainder of the article I provide a detailed explanation of the solution-code for both his code and the edits and additions I made to the code to complete this task at hand. 

To preface,  when adjusting the "randomizer" button, I had tried a few whole numbers but wasn't really understanding their purpose. All I knew was, based on not using a number when I was originally attempting to create a solition, that a number was need. So, I asked chatGPT then eventually came to 0.5 as it only made sense to be a number that is used often, but couldn't be a whole number because I had just about tried every one possible. [Here is my chatGPT conversation](https://chatgpt.com/share/68f85092-7258-8002-808a-38db8bfeb79b). This conversation showed me that the 0.5 is needed as a pivot point to let sort randomly swap the elements being considered. If the number was not there, the automatic assumption would be that A>B. This would cause little to no change in the array and there would not be a shuffle. 

## Part One: Creating the Table 

To being, I used the function `populateTable` to pass the `artists` variable as an arguemtn to use the data sorted within `artists` to display the table on my webpage.

```js
populateTable(artists); 
```

I then used `querySelector` lines to grab references from elements like the `nameButton` and repeat with the following date and random buttons. These lines find the HTML elements that create results to be stored in new constants labeled `nameButton`, `dateButton`, and `randomButton` to prepare for interactive items on my website.

```js 
 const nameButton = document.querySelector("#name-button");
 const dateButton = document.querySelector("#date-button");
 const randomButton = document.querySelector("#random-button");
``` 
## Part Two: Creating Interactive Elements
#### Buttons

Once the buttons were made, the following lines attached an event listener to each button element that was selected earlier.

```js
 nameButton.addEventListener("click", sortbyName);
 dateButton.addEventListener("click", sortbyDate);
 randomButton.addEventListener("click", randomize);
```
The code lines aboce work in ways to tell the broswer what should happen when the buttons are clicked. For example, when the reader clicked the button stored in `nameButton` which would only be shown on the website as Name, the function `sortbyName` is ran and executed to re-sort the list of names in an alternate way than before.

#### Making the Buttons Work

Now, we define the `sortbyName` function mentioned above that will be a reusable block of code to perform the task of sorting the list of artists by their names. Line 2 here creates the message "Sorting by Name..." that will appear in the VSCODE console when the button is clicked and called.


```js
function sortbyName() {
  console.log("Sorting by name...");
```
The lines above do not actually sort anything, but log a message to be a place holder for future sorting code like the following:

```js
  function byName(a, b) {
```
Here, the two parametes, a and b, are taken to define the function `byName`. a and b will represent the items being compared, which in this case are artist objects like "Rishi Rich", etc. 

```js
    if (a.name < b.name) return -1;
```
This line checks to see if the name property of a comes before the name of b alphabetically. If it does, -1 is returned to tell JavaScript that a needs to be put before b in the `sort()` function that is called.

```js
    if (a.name > b.name) return 1;
```
For when the opposite is true and b comes before a alphabetically, 1 is returned to tell JavaScript that be needs to come before a.

However, if neither conidition is true and the name are alphabetically equal, the `sort()` function will return 0, while tells JavaScript to leave the order unchanged. 

```js
    return 0;
   }
```

## Part Three: Performing the Action

#### The Sorting

The following code explains the full `sortbyName()` function to sort the artists array, clear the old table content, and create a new and neatly sorted table to be displayed.

```js
 const sortedByName = artists.sort(byName);
```
To begin, the line above takes the artists array and uses the `byName` function we defined a few lines back to determine the order of the elements in alphabetical comparison to be sorted. The `sort()` method changes the original array and returns the sorted array to hold the new, sorted lists by name. 

 ```js
 const tab = document.querySelector("#bhangra");
 ```
Next, the "bhangara" HTML element is found and determined to be the table where the artist data is displayed.

I then cleared everything currently inside the "bhangara" element and used this line:

```js
 tab.innerHTML = "";
```

to "reset" the table before insert the newly sorted rows. If this line was not performed, there would be a chance of duplicates because the new rows would possibly get added to old ones.

Finally, the existing table `populateTable()` is called with the new, sorted array instead of the original one. 

 ```js
 populateTable(sortedByName);
}
```
With the lines above, the table is re-built and displayed in alphabetical order by artist name. 

#### Repeating for following Buttons

First, we will repeat the same steps for the sorting of the Date button for the rearranging. 

```js
 function sortbyDate() {
  console.log("Sorting by year...");
  const sortedByDate = [...artists].sort((a, b) => a.birthYear - b.birthYear);
  populateTable(sortedByDate);
  console.log("date");
 }
```
Now, we will repeat using the same steps for the sorting randomizing the table.

```js
 function randomize() {
  console.log("Randomizing...");
  const shuffled = [...artists].sort(() => Math.random()- 0.5);
  populateTable(shuffled);
  console.log("random");
 }
```
#### Part Four: Setting up the Table

```js
function populateTable(arr) {
```
The line above defines the `populateTable` function that takes the array parameter, `arr`, and sets the goal being able to display its data inside the webpages HTML table.

Then, the following line finds the HTML element and uses it to insert the rows of the data into the table.

```js
const tab = document.querySelector("#bhangra");
```
## Building the string of HTML code

```js
let contents = "<tbody>";
```
The code above created a variable called `contents` to build up a string of HTML code by starting to open the `<tbody>` tag that is the beginning of where the rows will go in the tables body. 

For the following code, the backticks (`) are template literals which will allow for the multiline strings so the code would not require awkward +
```js
contents += `
    <tr>
      <th>Name</th>
      <th>Year of Birth</th>
      <th>Link</th>
    </tr>
    `;

// now loop to make the data-rows:

arr.forEach(artist => {
  // open the row:
  contents += "<tr>";
  contents += `<td>${artist.name}</td>`;
  contents += `<td>${artist.birthYear}</td>`;
  contents += `<td><a href="${artist.link}" target = "_blank">${artist.link}</a></td>`;
  // close the row:
  contents += "</tr>"
});

// close out the table body:
contents += "</tbody>";

// now make contents be the inner html of
// the table:
tab.innerHTML = contents;
 }
```

We are done!

## Full Code

Here is a compelete solution ot the problem for readers for view below:

```js
 const artists = [
   {
     name: "Ms Scandalous",
     birthYear: 1985,
     link: "https://www.youtube.com/watch?v=2FPivlfvxu0"
   },
   {
    name: "Juggy D",
    birthYear: 1981,
    link: "https://www.youtube.com/watch?v=1jAc_-FVjdI"
  },
  {
    name: "Sukhbir Singh",
    birthYear: 1969,
    link: "https://www.youtube.com/watch?v=HiprNF9Jad0"
  },
  {
    name: "Abrar-ul-Haq",
    birthYear: 1989,
    link: "https://www.youtube.com/watch?v=-lnnVIP7FEc"
  },
  {
    name: "Rishi Rich",
    birthYear: 1970,
    link: "https://www.youtube.com/watch?v=O95-w2gACuA"
  }
];

populateTable(artists); 
 
 const nameButton = document.querySelector("#name-button");
 const dateButton = document.querySelector("#date-button");
 const randomButton = document.querySelector("#random-button");

 nameButton.addEventListener("click", sortbyName);
 dateButton.addEventListener("click", sortbyDate);
 randomButton.addEventListener("click", randomize);

function sortbyName() {
  console.log("Sorting by name...");

  function byName(a, b) {
    if (a.name < b.name) return -1;
    if (a.name > b.name) return 1;
    return 0;
   }
 const sortedByName = artists.sort(byName);
 const tab = document.querySelector("#bhangra");
 tab.innerHTML = "";
 populateTable(sortedByName);
}

 function sortbyDate() {
  console.log("Sorting by year...");
  const sortedByDate = [...artists].sort((a, b) => a.birthYear - b.birthYear);
  populateTable(sortedByDate);
  console.log("date");
 }

 function randomize() {
  console.log("Randomizing...");
  const shuffled = [...artists].sort(() => Math.random()- 0.5);
  populateTable(shuffled);
  console.log("random");
 }

function populateTable(arr) {
const tab = document.querySelector("#bhangra");

let contents = "<tbody>";

contents += `
    <tr>
      <th>Name</th>
      <th>Year of Birth</th>
      <th>Link</th>
    </tr>
    `;

arr.forEach(artist => {
  contents += "<tr>";
  contents += `<td>${artist.name}</td>`;
  contents += `<td>${artist.birthYear}</td>`;
  contents += `<td><a href="${artist.link}" target = "_blank">${artist.link}</a></td>`;
  contents += "</tr>"
});

contents += "</tbody>";

tab.innerHTML = contents;
 }
```
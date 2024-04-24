---
layout: post
title: IMDb Rating Rainbow 🌈
description: Data visualization of user reviews
---

![image](/assets/images/imdb-visualizer.png)

[link to the GitHub repo](https://github.com/bencavins/imdb-vision)

Project Description
============

The purpose of this app is to visualize the average audience rating per episode of any given TV Series listed on IMDb. Users can search for *any* TV series on IMDb and view the average user ratings for each episode in a colorful grid! The ratings are color coded (green = good, yellow = average, red = poor) so we can see which episodes/seasons are liked by the average user and which are not. Each cell provides a link to the IMDb page for that episode.


Project Details
============

Python/Flask are used on the backend and Javascript/React are used for the frontend. Here are a list of all technologies:
* Python
* Flask
* SQLAlchemy
* PostgreSQL
* Alembic
* Javascript
* React.js


The Data Pipeline
============

Data is being pulled from IMDb but *not* from their API. While they *do* have an API, it is a bit expensive. Luckily, IMDb also publishes their non-commercial datasets [here](https://developer.imdb.com/non-commercial-datasets/). The only problem: all this data is in TSV files! Not quite as simple to deal with as the JSON you would get from an API. 

For one, the data is segmented into different files. All the "name" data (including the name of the series) is in `name.basics.tsv`. The episodes themselves are in `title.episode.tsv`. The ratings are in `title.ratings.tsv`. This makes sense when you think about how IMDb works, but it presents a challenge here since I want to merge all this data back together. 

Another challenge, there is *a lot* of data! For example, `name.basics.tv` contains **12.6 million** rows. We might not care about all these names but we still need to loop through all of them to check if we need them or not. This whole ETL process is running on my humble laptop so I can't rely on a big beefy server to take care of the data load for me. 

In the end, I kept the data model basically the same as what was in these TSV files and used I/O streams to loop through the files and batch processing the insert the data into the database. You can see the whole ETL script in `seed.py` linked [here](https://github.com/bencavins/imdb-vision/blob/main/imdb-vision-backend/seed.py). The whole process takes somewhere between 20-30 mins on my laptop.


The API
============

The API for this project is very simple, there are only two routes:

<table style="border-collapse: collapse; width: 100%;">
  <thead>
    <tr>
      <th style="border: 1px solid black; padding: 8px;">Method</th>
      <th style="border: 1px solid black; padding: 8px;">Endpoint</th>
      <th style="border: 1px solid black; padding: 8px;">Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="border: 1px solid black; padding: 8px;">GET</td>
      <td style="border: 1px solid black; padding: 8px;">/tv_series</td>
      <td style="border: 1px solid black; padding: 8px;">Get all TV series metadata</td>
    </tr>
    <tr>
      <td style="border: 1px solid black; padding: 8px;">GET</td>
      <td style="border: 1px solid black; padding: 8px;">/tv_series</td>
      <td style="border: 1px solid black; padding: 8px;">Get all TV series data (including episodes) that match this title. Fuzzy matching is used and data is sorted by highest match score.</td>
    </tr>
  </tbody>
</table>



2nd paragraph. *Italic*, **bold**, and `monospace`. Itemized lists
look like:

  * this one
  * that one
  * the other one

Note that the actual text
content starts at 4-columns in.

> Block quotes are
> written like so.
>
> They can span multiple paragraphs,
> if you like.


H2 Header
------------

Here's a numbered list:

 1. first item
 2. second item
 3. third item

Note again how the actual text starts at 4 columns in (4 characters
from the left side). Here's a code sample:

    # Let me re-iterate ...
    for i in 1 .. 10 { do-something(i) }

As you probably guessed, indented 4 spaces. By the way, instead of
indenting the block, you can use delimited blocks, if you like:

~~~
define foobar() {
    print "Welcome to flavor country!";
}
~~~

(which makes copying & pasting easier). You can optionally mark the
delimited block for Pandoc to syntax highlight it by specifying the languagae after the start of a block (e.g. `~~~cpp`) which would look like :

~~~cpp
#include <iostream>
using namespace std;

int main() 
{    
    cout << "Size of char: " << sizeof(char) << " byte" << endl;
    cout << "Size of int: " << sizeof(int) << " bytes" << endl;
    cout << "Size of float: " << sizeof(float) << " bytes" << endl;
    cout << "Size of double: " << sizeof(double) << " bytes" << endl;

    return 0;
}
~~~

### An H3 header ###

Now a nested list:

 1. First, get these ingredients:

      * carrots
      * celery
      * lentils

 2. Boil some water.

 3. Dump everything in the pot and follow
    this algorithm:

        find wooden spoon
        uncover pot
        stir
        cover pot
        balance wooden spoon precariously on pot handle
        wait 10 minutes
        goto first step (or shut off burner when done)

    Do not bump wooden spoon or it will fall.

Notice again how text always lines up on 4-space indents (including
that last line which continues item 3 above).

Here's a footnote [^1].

[^1]: Some footnote text.

Tables can look like this:

| Header 1 | Header 2                   | Header 3 |
|:--------:|:--------------------------:|:--------:|
| data1a   | Data is longer than header | 1        |
| d1b      | add a cell                 |          |
| lorem    | ipsum                      | 3        |
|          | empty outside cells        |          |
| skip     |                            | 5        |
| six      | Morbi purus                | 6        |


A horizontal rule follows.

***

Here's a definition list:

apples
  : Good for making applesauce.

oranges
  : Citrus!

tomatoes
  : There's no "e" in tomatoe.

Again, text is indented 4 spaces. (Put a blank line between each
term and  its definition to spread things out more.)

Here's a "line block" (note how whitespace is honored):

| Line one
|   Line too
| Line tree

and images can be specified like so:

![example image](https://images.unsplash.com/photo-1488190211105-8b0e65b80b4e?w=300&h=300&fit=crop "An exemplary image")

Inline math equation: $\omega = d\phi / dt$. Display
math should get its own line like so:

$$I = \int \rho R^{2} dV$$

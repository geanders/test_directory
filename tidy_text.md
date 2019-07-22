## The "tidyverse"




## What makes data "tidy"?

The "tidy" data format describes one way to structure tabular data. If you have
data in a structured, tabular format that doesn't follow these rules, you don't
need to consider it "dirty", though---just think of "tidy" as the tagname for
this particular structure of data (the name, in this case, connects the data
format with a set of tools in R called the "tidyverse"). 

The rules for making data tidy are pretty simple, and they are defined in detail
and with examples in the journal article that originally defined the data format
[Tidy data]. Here, we'll go through those rules, with the hope that you'll be
able to understand what makes a dataset follow the "tidy" data format. If so, 
you'll be able to set up your data recording template to follow this
template, and you'll be able to tell if other data you get is in this format 
and, if it's not, restructure it so that it does. 

Tidy data, first, must be in a tabular (i.e., two-dimensional, with columns and
rows, and with all rows and columns of the same length---nothing "ragged").  
If you recorded data in a spreadsheet using a very basic strategy of saving a 
single table per spreadsheet, with the first row giving the column names (as described
in the previous module), then your data will be in a tabular format. 

There are some additional criteria for the "tidy" data format, though, and so
not every structured, tabular dataset is in a "tidy" format. The first of these
rules are that each row records the values for a single observation, and that
each column provides characteristics or measurements for that single
observation. 

To be able to decide if your data is tidy, then, you need to know what forms a
single observation in your dataset. The *unit of observation* of a dataset
is ... 

For example, say you are testing how the immune system of mice responds to a
certain drug over time. You may have several replicates of mice measured at
several time points, and those mice might be in separate groups (for example,
infected with a disease versus uninfected).  In this case, if a separate mouse
(replicate) is used to collect each observation, and a mouse is never measured
twice (i.e., at different time points, or for a different infection status),
then the unit of measurement is the mouse. There should be one and only one row
in your dataset for each mouse, and that row should include two types of
information: first, information about the unit being measured (e.g., the time
point, whether the mouse was infected, and a unique mouse identifier) and,
second, the results of that measurement (e.g., the weight of the mouse when it
was sacrificed, the levels of different immune cell populations in the mouse, a
measure of the extent of infection in the mouse if it was infected, and perhaps
some notes about anything of note for the mouse, like if it appeared noticably
sick).

The unit of observation, however, is not always the same as the study
"subjects". For example, say you conducted a trial on human subjects, where each
study subject was measured at different time points. In this case, the unit of
observation is the combination of study subject and time point.  That means that
Subject 1's measurement at Time 1 would be one observation, and the same
person's measurement at Time 2 would be a separate observation.  For a dataset
to comply with the "tidy" data format, these two observations would need to be
recorded on separate lines in the data. If the data instead had different
columns to record each study subject's measurements at different time points,
then the data would still be tabular, but it would not be "tidy". 

In this second example, you may initially find the "tidy" format unappealing,
because it seems like it would lead to a lot of repeated data. For example, if
you wanted to record each study subject's sex, it seems like the "tidy" format
would require you to repeat that information in each separate line of data
that's used to record the measurements for that subject for different time
points. This isn't the case---instead, with a "tidy" data format, different
"levels" of data should be recorded in separate tables. So, if you have some
data on each study subject that does not change across the time points of the
study---like the subject's ID, sex, and age at enrollment---those form a
separate dataset, one where the unit of observation is the study subject, so
there should be just one row of data per study subject in that data table, while
the measurements for each time point should be recorded in a separate data
table. A unique identifier, like a subject ID, should be recorded in each data
table so it can be used to link the data in the two tables. Once you read the
data into a scripting language like R or Python, it will be easy to link the
larger and smaller "tidy" datasets as needed for analysis, visualizations, and
reports.  

[Other criteria?]

## Why make your data "tidy"?

This may all seem like a lot of extra work, to make a dataset "tidy", and why 
bother if you already have it in a structured, tabular format? It turns out 
that, once you get the hang of what gives data a "tidy" format, it's pretty 
simple to design recording formats that comply with the rules. What's more, 
when data is in a "tidy" format, it can be directly input into a collection 
of tools in R that belong to something called the "tidyverse". This collection
of tools is very straightforward to use and so powerful that it's well worth
making an effort to record data in a format that works directly with the 
tools, if possible. Outside of cases of very complex or very large data, it
should be possible.  

The "tidyverse" is a collection of tools united by a common philosophy: **very 
complex things can be done simply and efficiently with small, sharp tools
that share a common interface**. The tidyverse isn't the only popular system 
that follows this philosophy---one other favorite is Legos. Legos are small, 
plastic bricks, with small [tines] on top and spaces for [tines] to fit on the
bottom. The [tines] all have the same, standardized size and are all spaced 
the same distance apart. Therefore, the blocks can be joined together in 
any combination, since each block uses the same *input format* ([tines] 
of the standard size and spaced at the standard distance) on the bottom of the
block and the same *output format* (again, [tines] of the standard size and
spaced at the standard distance) at the top of the block. This is true 
if you want to build with blocks of different colors or different heights 
or different widths or depths. It even allows you to include blocks at 
certain spots that either don't require input (for example, a solid sheet 
that will serve as the base) or that don't give output (for example, the 
round smooth blocks with painted "eyes" that are used to create different 
creatures). With Legos, even though each "tool" (block) is very simple, 
the tools can be combined in infinite variations to create very complex
structures. 

The tools in the "tidyverse" operate on a similar principle. They all input one
of a few very straightforward data types, and they (almost) all output data in
the same format they input it. For most of the tools, their required format for
input and output is the "tidy data" format, called a tidy *dataframe* in R.
Some of the tools require input and output of *vectors* instead of tidy
dataframes; a *vector* is a one-dimensional string of values, all of which are
of the same data type (e.g., all numbers, or all character strings, like names).
In a tidy dataframe, each column is a vector, and the dataframe is essentially
several vectors of the same length stuck together to make a table. Having
functions that input and output vectors, then, means that you can use those
functions to make changes to the columns in a tidy dataframe. A few functions in
the "tidyverse" input a tidy dataframe but output data in a different format.
For example, visualizations are created using a function called `ggplot`, as
well as its helper functions and extensions. This function inputs data in a tidy
dataframe but outputs it in a type of R object called a "ggplot object". This
object encodes the plot the code created, so in this case the fact that the
output is in a different format from the endpoint is similar to with the "eye"
blocks in Legos, where it's meant as a final output step, and you don't intend
to do anything further in the code once you move into that step. 

This common input / output interface, and the use of small tools that follow
this interface and can be combined in various ways, is what makes the tidyverse
tools so powerful. However, there are other good things about the tidyverse that
make it so popular. One is that it's fairly easy to learn to use the tools, in
comparison to learning how to write code for other R tools. The developers who
have created the tidyverse tools have taken a lot of effort to try to make sure
that they have a consistent *user interface*. So far, we've talked about the
interface between functions, and how a common *input / output interface* means
 the functions can be chained together more easily. But there's another
interface that's important for software tools: the rules for how a computer 
users employ that tool, or the *user interface*.


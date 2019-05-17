# ClusteredLabeledData
Using clustering algorithms and metrics, create labeled data to be used in 
classifying algorithms.

## What is this?
This is a code repository of me exploring a topic I wrote on for my 
final essay for my AI/ML Special Topics class at UAH. To see the actual essay, 
[here it is](https://docs.google.com/document/d/1ehqxeSzbD7R1aTfdQMXVjXJRPg9g6JYlufEznbRoiLY/edit?usp=sharing).

## But I don't want to read an essay!
Well here you go!

### What are Clustering Algorithms?
Clustering algorithms are a part of the data science field. The algorithm
takes in data and tries to partition it up so that the data are in nice
little spots. A classic example of a clustering algorithm is the 
[k-means algorithm](https://jakevdp.github.io/PythonDataScienceHandbook/05.11-k-means.html).

The k-means clustering algorithm isn't the greatest however. This is 
in part because of the random initialization it has in the beginning of the
algorithm and the fact that it looks for spherical clusters. Most data is 
not spherical as all experienced data scientists will tell you. The textbook
referenced above explains this in much more detail. Also, the link
above is actually a very good resource on most things related to data science.
The author has a textbook that is available for purchase if you don't want
to use the free online textbook or would prefer a hard copy of the book. I 
personally recommend it.

### What is Category Utility?
Category utility is an information gain metric that is best used with
clustered data. An information gain metric is a formula that tells you
how predictive the data it's operating on can be guessed to be in a certain
category. Or cluster for our purposes. The material covered in the textbook 
that is referenced within my essay can be found 
[here](https://www.cs.waikato.ac.nz/ml/weka/book.html) and the equation for 
Category Utility can be found on slide 118 on [this slide deck](https://www.cs.waikato.ac.nz/ml/weka/slides/Chapter4.pptx).
Or you can use [this Wikipedia article](https://en.wikipedia.org/wiki/Category_utility).

### How do the two relate together?
Well by using the Category Utility, we can essentially find the number of 
clusters that is likely to be the total number of possible classifications
within the data. If we treat each cluster as its own classification, we can
then take unlabeled data and turn it into labeled data that can be used in
classification algorithms, such as neural networks. We're assuming that as
our number of clusters approach the total number of classifications, our 
category utility will reach its maximum value.

### How will you address overfitting?
For those unaware, overfitting is when a model "memorizes" the data that is
passed in. This is bad, as we want our model to be able to perform optimally
on all types of data. 

How we address overfitting is that we put in stopping measures for the algorithm.
For instance, we can stop the algorithm once it reaches a number of clusters
proportional to the total number of data points. An example of this is if we
had 100,000 data points but we wanted to stop if the number of clusters was 
a fifth of the total number of data points. A fifth of 100,000 is 20,000. So
we would stop once the number of clusters was 20,000. We would likely go to 
a lower number. What would be the ideal number is how many data points you
think is in each classification. We don't expect there to be 5 data points 
in each classification in our data set, so that's why 20,000 might be too
large of a number.

Other possible overfitting measures can include stopping once the category
utility starts decreasing. Another might be to stop after a certain number of
iterations of the algorithm. These are just ideas that are by no means the
only measures that can be taken to prevent overfitting. If anyone else has
any more ideas to solve overfitting, please contribute to the discussion!

### How does the algorithm work?
1. Select an initial number of clusters
    - a good start might be 2 at the very least
2. Run the clustering algorithm on our data.
    - the clustering algorithm can be any that requires a number of clusters as a parameter.
3. Run the category utility on the generated clusters.
4. See if any of our stopping conditions is true.
    - Repeat from 2 onward until they are.
5. Your clusters are now the potentially labeled data that can be used in classification algorithms.

```R
#### Given the following data frame, how do I create a new column called “3” 
#### that contains the sum of 1 and 2? You may only use $, not [[. 
#### What makes 1, 2, and 3 challenging as variable names?
df <- data.frame(runif(3), runif(3))
names(df) <- c(1, 2)


#### my answer
df[3]<-df[1]+df[2]
names(df[3])<-3
print(df)
```


```R
#### In the following code, how much memory does y occupy?
x <- runif(1e6)
y <- list(x, x, x)


### #my answer
object.size(y)
```


```R
#### On which line does a get copied in the following example?
a <- c(1, 5, 3, 2)
b <- a
b[[1]] <- 10


#### my answer
#### at the last. i used lobstr::obj_addr to check
```


```R
#### Explain the relationship between a, b, c and d in the following code:
a <- 1:10
b <- a
c <- b
d <- 1:10


####my answer
#### a,b,c point to the same address. 
lobstr::obj_addr(a)==lobstr::obj_addr(b) & lobstr::obj_addr(a)==lobstr::obj_addr(c)
lobstr::obj_addr(d)!=lobstr::obj_addr(a)
```


TRUE



TRUE



```R
####The following code accesses the mean function in multiple ways. 
####Do they all point to the same underlying function object? Verify this with lobstr::obj_addr().
mean
base::mean
get("mean")
evalq(mean)
match.fun("mean")


####my answer
lobstr::obj_addr(mean)==lobstr::obj_addr(base::mean) & lobstr::obj_addr(mean)==lobstr::obj_addr(get("mean")) &
lobstr::obj_addr(mean)==lobstr::obj_addr(evalq(mean)) & lobstr::obj_addr(mean)==lobstr::obj_addr(match.fun("mean")) 
```


<pre class=language-r><code>function (x, ...) 
UseMethod("mean")</code></pre>



<pre class=language-r><code>function (x, ...) 
UseMethod("mean")</code></pre>



<pre class=language-r><code>function (x, ...) 
UseMethod("mean")</code></pre>



<pre class=language-r><code>function (x, ...) 
UseMethod("mean")</code></pre>



<pre class=language-r><code>function (x, ...) 
UseMethod("mean")</code></pre>



TRUE



```R
#### By default, base R data import functions, like read.csv(), will automatically convert non-syntactic names 
#### to syntactic ones. Why might this be problematic? What option allows you to suppress this behaviour?


#### my answer. cit [stackoverflow]
?check.names
#### check.names: logical.  If ‘TRUE’ then the names of the variables in the
#### data frame are checked to ensure that they are syntactically valid variable names. 
```


```R
#### What rules does make.names() use to convert non-syntactic names into syntactic ones?


#### my answer. cit [stackoverflow]
#### The character "X" is prepended if necessary. All invalid characters are translated to ".". 
#### A missing value is translated to "NA". Names which match R keywords have a dot appended to them.
#### Duplicated values are altered by make.unique
?make.names

```


```R
#### I slightly simplified the rules that govern syntactic names. Why is .123e1 not a syntactic name? 
#### Read ?make.names for the full details.


#### my answer
#### it begins with ""." . let's try.
make.names(.123e1)
```


'X1.23'


2.3.6 Exercises
Why is tracemem(1:10) not useful?

Explain why tracemem() shows two copies when you run this code. Hint: carefully look at the difference between this code and the code shown earlier in the section.

x <- c(1L, 2L, 3L)
tracemem(x)

x[[3]] <- 4
Sketch out the relationship between the following objects:

a <- 1:10
b <- list(a, a)
c <- list(b, a, 1:10)
What happens when you run this code?

x <- list(1:10)
x[[2]] <- x
Draw a picture.



2.4.1 Exercises
In the following example, why are object.size(y) and obj_size(y) so radically different? Consult the documentation of object.size().

y <- rep(list(runif(1e4)), 100)

object.size(y)
#> 8005648 bytes
obj_size(y)
#> 80,896 B
Take the following list. Why is its size somewhat misleading?

funs <- list(mean, sd, var)
obj_size(funs)
#> 17,608 B
Predict the output of the following code:

a <- runif(1e6)
obj_size(a)

b <- list(a, a)
obj_size(b)
obj_size(a, b)

b[[1]][[1]] <- 10
obj_size(b)
obj_size(a, b)

b[[2]][[1]] <- 10
obj_size(b)
obj_size(a, b)

2.5.3 Exercises
Explain why the following code doesn’t create a circular list.

x <- list()
x[[1]] <- x
Wrap the two methods for subtracting medians into two functions, then use the ‘bench’ package17 to carefully compare their speeds. How does performance change as the number of columns increase?

What happens if you attempt to use tracemem() on an environment?

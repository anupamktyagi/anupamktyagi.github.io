I have been fortunate enough to develop enterprise applications using functional programming as part of my job. I use F# extensively to write code ranging from analytical/quantitative software to reporting frameworks and domain specific languages. F# has been a great language to learn and is a very powerful tool to have in the .NET environment. However I have always been fascinated by Haskell. Partly due to its portrayal as a pure functional language and how it forces the use of strict functional paradigms.

Needless to say part of my learning to-dos this year is learning Haskell and hopefully implementing it in a real world application. I have been learning it for a couple of weeks now through the Learn You a Haskell for Great Good book available freely at http://learnyouahaskell.com. Mostly on and off on weekends. This is my first tryst with haskell and Learn You A Haskell is a great introduction to the language notorious for having a steep learning curve. Also I absolutely agree with haskellers that learning haskell provides insights into functional programming that are easily missed with F# and maybe other functional programming languages out there. A reason might be that it is very easy to manipulate F# into a non functional way of doing things. With Haskell , and it might be the way in which it limits you to thinking in a certain manner, manipulations are not as straightforward.

Unless you are really into it , it is difficult to compare languages and I would prefer not to do so. F# has its charm and usability and if you are in a .NET environment it is the language to go for. I am a newbie as far as Haskell is concerned. However no harm in showing off an elegant solution that haskell provides for an interesting problem.

Enter Project Euler

Chances are if you are reading this post, you are well aware of Project Euler. If not, you should register at https://projecteuler.net and start hacking. Its a great resource to learn any new programming language. Needless to say I have been using it for haskell.

Problem 4 : The problem 4 in project euler involves working in and around strings and goes as follows

A palindromic number reads the same both ways. The largest palindrome made from the product of two 2-digit numbers is 9009 = 91 × 99. Find the largest palindrome made from the product of two 3-digit numbers.

My solution as I approached this is as below.

{% highlight ruby linenos %} listproduct x xs = map (*x) xs

zipWithProd [] _ = [] zipWithProd _ [] = [] zipWithProd (x:xs) y = listproduct x y : zipWithProd xs y

ispalindrome x = x - (read (reverse $ show x) + 0) == 0

largestPalindromeList = map m (zipWithProd [100..999] [100..999]) where m y = filter ispalindrome y

largestPalindrome = maximum largestPalindromeList {% endhighlight %}

Thats quite a mouthful and its not a good solution. Walking through it you can see that I have a function (ispalindrome) that determines if a number is a palindromic number.

show is part of the Show typeclass in Haskell and is used to convert x into its equivalent string version. For eg show 2  gives "2" . 
read is part of the Read typeclass and acts like the inverse of show. 
zipWithProd is a higher order function that zips the two lists by multiplying corresponding elements
map is a higher order function in haskell that applies the function ispalindrome to each element of the list obtained out of the zipWithProd.
This solution reeks of newbieness and while i am not quite proud of it, it has gone some way in driving home the nuances of haskell. Basically what i am trying to do here is obtain a list of three digit number products, test each for the palindromic property and then out of those determine the maximum. 

The neat way to do this in haskell though is as follows, courtesy the haskell wiki (https://wiki.haskell.org/)

{% highlight ruby linenos %}
maximum [x | y<-[100..999], z<-[y..999], let x=y*z, let s=show x, s==reverse s]
{% endhighlight %}


A solution in F# will not be as elegant as this. A quick solution in F# can be

{% highlight ruby linenos %}

let threeDigitProds = [for x in [100..999] do for y in [x..999] -> x*y]
let palindromes : seq<int>  = threeDigitProds
       |> Seq.filter(fun x -> 
           let y= string x
           let z =new string(y.Reverse().ToArray())
           y=z                 
            )
            

let maxPalindrome  = palindromes      
      |> Seq.max

{% endhighlight %}

This is just one of those reasons why learning haskell can be really fun. There are a few more. For eg Typeclasses, Algebraic Data Types and Monads. More on that later.
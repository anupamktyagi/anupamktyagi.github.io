I have been fortunate enough to develop enterprise applications using functional programming as part of my job. I use F# extensively to write code ranging from analytical/quantitative software to reporting frameworks and domain specific languages. F# has been a great language to learn and is a very powerful tool to have in the .NET environment. However I have always been fascinated by Haskell. Partly due to its portrayal as a pure functional language and how it forces the use of strict functional paradigms.

Needless to say part of my learning to-dos this year is learning Haskell and hopefully implementing it in a real world application. I have been learning it for a couple of weeks now through the Learn You a Haskell for Great Good book available freely at http://learnyouahaskell.com. Mostly on and off on weekends. This is my first tryst with haskell and Learn You A Haskell is a great introduction to the language notorious for having a steep learning curve. Also I absolutely agree with haskellers that learning haskell provides insights into functional programming that are easily missed with  F# and maybe other functional programming languages out there. A reason might be that it is very easy to manipulate F# into a non functional way of doing things. With Haskell , and it might be the way in which it limits you to thinking in a certain manner, manipulations are not as straightforward.

Unless you are really into it , it is difficult to compare languages and I would prefer not to do so. F# has its charm and usability and if you are in a .NET environment it is the language to go for. I am a newbie as far as Haskell is concerned. However no harm in showing off an elegant solution that haskell provides for an interesting problem.


Enter Project Euler

Chances are if you are reading this post, you are well aware of Project Euler. If not, you should register at https://projecteuler.net and start hacking. Its a great resource to learn any new programming language. Needless to say I have been using it for haskell.

Problem 4 : The problem 4 in project euler involves working in and around strings and goes as follows

A palindromic number reads the same both ways. The largest palindrome made from the product of two 2-digit numbers is 9009 = 91 × 99. Find the largest palindrome made from the product of two 3-digit numbers.

My solution as I approached this is as below.

{% highlight ruby linenos %}
listproduct x xs = map (*x) xs

zipWithProd  [] _ = []
zipWithProd _ [] = []
zipWithProd (x:xs) y = listproduct x y : zipWithProd xs y

ispalindrome x = x - (read (reverse $ show x) + 0) == 0

largestPalindromeList = map m (zipWithProd [100..999] [100..999])
 where m y = filter ispalindrome y

largestPalindrome = maximum largestPalindromeList
{% endhighlight %}


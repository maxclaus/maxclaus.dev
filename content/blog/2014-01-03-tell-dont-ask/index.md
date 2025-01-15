+++
title = "Tell don't Ask"
+++

<p><em>Article originally posted on <a href="http://tribalingua.wordpress.com/2013/12/17/tell-dont-ask/">Tribalingua</a>.</em></p>
<p><span style="line-height: 1.5em;">Do you take care with how you write a letter? So that it will clear and easy for your recipient  to read? Well, it should be the same feeling with the code that you write. With a letter we sometimes have to stop and think what is the best way to write down what is in our minds. Therefore, we have to be clear and easy for anyone else reading what you were thinking when you wrote that.  Just as we have rules to write a nice readable letter, also we have Patterns and Principles to write clean and </span><span style="line-height: 1.5em;">understandable</span><span style="line-height: 1.5em;"> code.</span></p>
<p>The principle <strong>Tell don't Ask</strong> helps to ensure a correct division of responsibility  without causing excess coupling to an incorrect class.</p>
<blockquote><p>...you should endeavor to <em>tell</em> objects what you want them to do; do not <em>ask</em> them questions about their state, make a decision, and then tell them what to do. - <a href="http://pragprog.com/articles/tell-dont-ask">The Pragmatic Bookshelf</a></p></blockquote>
<p><a href="./telldontask1.png"><img class="aligncenter size-large wp-image-3892" alt="TellDontAsk" src="./telldontask1.png?w=490" width="490" height="602" /><!--more--></a></p>
<p>To exemplify it I wrote a sample based in a common code present in a project that I'm working on in this sprint.</p>
{% gist maxcnunes/8005735 %}
<p>In the Ask version I have too much logic outside the Form class, that should be responsible to do all that process. In the Tell version I just tell what I want and nothing else. This increases the maintainability and readability of my code because it is shorter, cleaner and I let the Form class do what it knows doing better than the Screen class.</p>
<p>As many others principles and patterns in software design, this is not set in stone nor is it  a silver bullet to solve all your problems, but anyway with approaches like that you will be guided towards a better code.</p>
<p>So do you want to be known as a good writer or as that crazy drunk friend that sends you nonsense messages on the phone at 3:00 AM?! Think about it :)</p>

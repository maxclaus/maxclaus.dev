+++
title = "Linux command line to check the directory's size"
+++

<p>Using the Nitrous.io I got this message "<strong>disk quota exceeded</strong>" after try install mongoid. The initial plan available for free accounts on Nitrous provides 750MB storage.</p>
<p>But I was asking myself how could my application in rails, that I just started to code, get all this space used? Try to guess could no help me to solve this problem then I learned this new linux command line to check the directories size:</p>
<pre class="brush: shell">du -h --max-depth=1 ~/ | sort -n -r</pre>
<p>And I understood exactly where the problem was, my .rvm directory was too much big:</p>
<pre class="brush: shell">405M    /home/action/
222M    /home/action/.rvm
144M    /home/action/.gem
24M     /home/action/.nvm
24K     /home/action/.subversion
15M     /home/action/.vim
8.0K    /home/action/.ssh
1.8M    /home/action/easy_order
0       /home/action/workspace
0       /home/action/.cache</pre>
<p><em>ps: I got this output after remove a ruby version not used</em></p>
<p>Explaning the command line:</p>
<ul>
<li><span style="line-height: 13px;">du : shows how much space one ore more files or directories is using</span></li>
<li>-h : format output to show the size in MB</li>
<li>--max-depth=1 : consider just the top directories</li>
<li>~/ : direcoty's path to exam</li>
<li>| sort -n -r: sort by size</li>
</ul>
<p><span style="color: #ff0000;">Off-Topic:</span> Please, help me to get more space in Nitrous. You just have to create an account using my <a href="https://www.nitrous.io/join/m02YDPBCqzU">link</a> :)</p>

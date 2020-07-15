# TryHackMe-OWASP-Top10

![Intro](Introduction_Image.png)

**[Click Here and Try It Out!](https://tryhackme.com/room/owasptop10)**

## [OWASP Top 10 - A challenge everyday for 10 days]

Learn one of the OWASP vulnerabilities every day for 10 days in a row. A new task will be revealed every day, where each task will be independent from the previous one. These challenges will cover each OWASP topic:


> My First Try at Hacking Lab Write-Ups ;)

### Day 1:

**Vulnerability:** <code> Injection </code>

**Target:** <code>http://MACHINE_IP/evilshell.php.</code>
***Simple Description: A Search bar is given, we also know that the PHP Code for the same allows command injection***

**Questions:**

![Answers](Answers_Day_1_(Blurred).png)

#### Approach for each Question: (Answers are at the end)
**Question 1:** <code> What strange textfile is in the website root directory ? </code><br>
**My Solution:**
<p>A simple <code>ls</code> command gave away the name of a textfile. 
Ideally, I should have also checked the root directory using <code>pwd</code>.</p>

**Question 2:** <code> How many non-root/non-service/non-daemon users are there ? </code><br>
**My Solution:**
<p>This seemed difficult at first, on running <code>cat /etc/passwd</code>, even though all the users were displayed, still I wasn't able to figure out much.
  I searched up online and then used <code> cut -d: -f1 /etc/passwd </code> to get only the usernames. Comparing this output with a similar output on my own
terminal led me to realise that there are no such non-special users.</p>


**Question 3:** <code> What user is this app running as ? </code><br>
**My Solution:**
<p>This was easy, a simple <code>whoami</code> did the task.</p>

**Question 4:** <code>What is the user's shell set as ? </code><br>
**My Solution:**
<p>This was the trickiest in my opinion. I used this amazing guide on the forums to figure it out. [Link to article](https://medium.com/@tirthesh.pawar/owasp-top-10-day-1-injection-e1d5b15b1baf). On deeper analysis of the <code>cat /etc/passwd</code> result. We find the answer. I owe this answer fully to this article. I realised that I needed to know what <code>cat /etc/passwd</code> actually gave.</p>

**Question 5:** <code> What version of Ubuntu is running ? </code><br>
**My Solution:**
<p>This again was pretty easy. <code>lsb_release -a</code> did the job.</p>

**Question 6:** <code> Print out the MOTD. What favorite beverage is shown ? </code><br>
**My Solution:**
<p>I tried a pretty amateur apporach at this. On opening the contents of the file that we found in *Question 1*, I thought I'd try out the same as the answer and it worked!
Yet actually, (again had to use this [article](https://medium.com/@tirthesh.pawar/owasp-top-10-day-1-injection-e1d5b15b1baf) the "message-of-the-day" file had been changed to "00-header" as mentioned in the *Hint*.Thus, using <code>cat /etc/update-motd.d/00-header</code>, the answer was finally revealed.</p>

#### Answers: (CAUTION!: If you are also trying this machine, I'd suggest you to maximise your own effort, and then only come and seek the answers. Thanks.)
**Q1:** <code>drpepper.txt</code>
**Q2:** <code>0</code>
**Q3:** <code>www-data</code>
**Q4:** <code>/usr/sbin/nologin</code>
**Q5:** <code>18.04.4</code>
**Q6:** <code>Dr Pepper</code>

---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

### Day 2:

**Vulnerability:** <code> Broken Authentication </code>

**Target:** <code>http://MACHINE_IP:8888</code>
***Simple Description: A SignIn Button and a Register Button is given on the top, 2 fields are given for Sign-Up and a new set of 3 fields is opened up on Registration***

**Questions:**

![Answers](Answers_Day_2_(Blurred).png)

#### Approach for each Question: (Answers are at the end)
**Question 1:** <code> 	What is the flag that you found in darren's account ? </code><br>
**My Solution:**
<p>We are given that there is an account named <code>darren</code> which contains a *flag*. To access this account, if we try something like <code>darren </code> (Notice the space at the end), or even <code>   darren</code> (3 spaces in the front), for *REGISTERING* a new account and then we try Logging in with this account. Then we are able to access the account details, in this case, the *flag* from the actual *darren* account.</p>

**Question 2:** <code> Now try to do the same trick and see if you can login as arthur. </code><br>
**Not Solution Based, only apply the above method again.**

**Question 3:** <code> What is the flag that you found in arthur's account ? </code><br>
**My Solution:**
<p>By trying the same method as in Darren's account, we are able to reach the flag in this one too! <br>What's important though, is going to the next level. Thus, I tried out various different types of alternative inputs like <code>arthur.</code> <code>art hur</code> <code>_arthur</code> <code>"arthur"</code>. <br>Well, none of those actually work and thus I realised that only *blank spaces* can be used to check Broken Authentication successfully.</p>

#### Answers: (CAUTION!: If you are also trying this machine, I'd suggest you to maximise your own effort, and then only come and seek the answers. Thanks.)
**Q1:** <code>fe86079416a21a3c99937fea8874b667</code>
**Q2:** <code>No Answer Required</code>
**Q3:** <code>d9ac0f7db4fda460ac3edeb75d75e16e</code>

---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

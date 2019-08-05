---
title: Behind the scenes of coding interviews - good vs bad!
layout: post
subtitle: What happens inside an interview room? What factors affect the decision
  of an interviewer?
tags: "[coding interview]"
---

Interviewing is a skill in and of itself. You can be the best developer in the world but you may still screw up an interview.

<blockquote class="twitter-tweet"><p lang="en" dir="ltr">Google: 90% of our engineers use the software you wrote (Homebrew), but you can’t invert a binary tree on a whiteboard so fuck off.</p>&mdash; Max Howell (@mxcl) <a href="https://twitter.com/mxcl/status/608682016205344768?ref_src=twsrc%5Etfw">June 10, 2015</a></blockquote> <script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script>

How many times have you come out of an interview and wondered what did I do wrong? Why did they reject me? As a candidate, it helps a lot to understand the expectations in an interview. In this article, I want to show every aspiring candidate the difference between a good and a bad interview and how it is perceived by the interviewer. We will compare and contrast two different interviews and learn from each of them so that you can tweak your actions to match the expectations.

## First Interview
Let me take the same question above "Inverting a binary tree".

*Interviewer (I)*: Hi, Welcome to our company. I am xxx doing yyy. So tell me about yourself.

*Candidate (C)* : I am xxx. I have about 5 years of experience in Backend development. I love solving technical problems.....

*I*: That's great. So shall we move on to the problem-solving part?

*C*: Sure!

*I*: So you are given a binary tree. I want you to invert the binary tree and print the resulting tree.

*C*: ***(Thinking in the head)*** Hmmm Ok. A binary tree has two children. So I am assuming inverting means printing from leaf to root. So the easiest way to do that is to traverse the tree till the end and find the leaves...

*I*: ***(After 5 mins of complete silence)***  Do you understand the question? Do you need any clarification?

*C*: I am **clear**. Now I am just thinking of a way to print the nodes starting from the leaf.

*I*: What do you mean to print the nodes starting from the leaf?

*C*: So basically I should print from leaf to root right? It is easy to traverse until the leaf. But the hard part is traversing back?

*I*: Hmmm. Are you sure you understand the question right? Inverting a tree means you should **swap the left and right children**. 

*C*: Sorry I am not clear. When you said invert I **assumed** you meant printing from leaf to root.

*I*: That's alright ***(This is where you lost the job)***. Now that you are clear let's proceed.

*C*: Yes I am clear. So now I have to swap the left and right nodes. That's easy right.
***(Writes code in silence)***
```ruby
def invert(node)
  t = node.left 
  node.left = node.right
  node.right = t
  return node
end
```

*C*: I am done with the code.

*I*: Cool. So what have you done here?

*C*: I have inverted the tree by swapping the left and right nodes. So I keep a temp variable to achieve the same.

*I*: ***(Trying to nudge towards a proper solution)*** But this swaps only the root node right?

*C*:***(Puzzled)*** Hmm yes, so the left and right children will be inverted. That's the question right?

*I*: ***(Still there is no clarity in question)*** So the question is the complete tree should be inverted. Not just the root.

*C*: Oh geez. So it is not just the root but the complete tree. Am I right?

*I*: Yes that is correct.

*C*: Ok. Let me think about it. 

***(After 2 mins)***

*C*: I think I got it. So basically I need to do the same algorithm I wrote for the whole tree. Am I right?

*I*: Yes, but how do you do that?

*C*: ***(Starts writing Code)***

```ruby
def invert(node)
  invert(node.left)
  invert(node.right)
  t = node.left 
  node.left = node.right
  node.right = t
  return node
end
```

So I am **guessing** this should work.

*I*: Hmmm, let me see. ***(Finds the issue. Can you?)*** I am not sure if it works. Can you please run me through it?

*C*: Sure. First I am inverting the left subtree, then the right subtree and then I am swapping them so that root is inverted.

*I*: Hmmm. But the left and right nodes are returning new nodes after the swap right? You are still swapping the old nodes.

*C*: I am not sure what you mean by that. I think this **will** work for all cases.

*I*: Great man! We have run out of time. Thanks for your time, it was lovely talking to you. HR will get back to you.

## Feedback
Now, what do you think was the final decision and what was the interviewer's feedback? The hypothetical feedback would be something along these lines:

* The candidate assumed a lot of things and did not clarify the problem.
* The candidate came up with the approach out of nowhere and there was no proper reasoning behind the approach taken. (Remember the silence in the interview?)
* The candidate was not clear with the requirements even in the implementation stage.
* The candidate struggled with the implementation and he was not able to pick up hints pointing towards the solution.
* The candidate failed to identify the bugs in code, even after providing enough time and probing to check if the solution is correct.

If this were an actual interview, the candidate would have been rejected. Now how should the ideal interview go?

## Second interview
*Interviewer (I)*: Hi, Welcome to our company. I am xxx doing yyy. So tell me about yourself.

*Candidate (C)* : I am xxx. I have about 5 years of experience in Backend development. I love solving technical problems.....

*I*: That's great. So shall we move on to the problem-solving part?

*C*: Sure!

*I*: So you are given a binary tree. I want you to invert the binary tree and print the resulting tree.

*C*: ***(Thinking out loud)*** Cool. So a binary tree has two nodes. So what exactly is inverting? is it swapping the left and right?

*I*: Exactly. So left node should be on the right and vice versa. 

*C*: Ok. So in this case what happens?

***Provides an example and clarifies input and output***

*I*: You are correct to some extent. But this should happen for the whole tree, not just the root alone.***(Notice how early the requirements were solidified)***

*C*: Oh got it! So I am thinking I need to do it recursively. Man, that's tough! Let me see. But before that, I'll just check my understanding by running through one more example.
*Provides one more eg to clarify any missing pieces*

*I*: Yes you are right. That's the output. I think you got the problem completely. So how do you approach it?

*C*: Let me see. So to swap left and right, I can just use a temp. But then how will I do it for remaining? Oh ya, I could just recurse for the others and do the same.

*I*: Cool. Is there any problem with that approach?

*C*: Hmmm. Yes, if I just swap the left and right recursively, how will I track the old and new tree?

*I*: I am not sure I am following you. What is old and new?

*C*: What I meant is, there will be updated children, I need to swap them and not the old children.

*I*: Yes, correct.

*C*: Ya I can just call this function recursively for left and right and store those values in a variable. I could then update the tree with those variables. This way I can make sure the whole tree is inverted.

*I*: Cool. Anything else you are missing?

*C*: No I think. So it will take O(n) time and O(1) space as I don't use any extra space.***(Notice how proactively the candidate discusses time and space)***

*I*: I am fine. You can start coding.

*C*: Sure. ***(Talks through the code while coding)***

```ruby
def invert(node)
  l =   invert(node.left)
  r =  invert(node.right)
  t = l
  node.left = r
  node.right = l
  return node
end
```

*C*: So I am done. Let me walk you through my code. So for a tree like ...***(Explains and dry runs with an example)***

*I*: I guess you are right. Does it work for all cases?

*C*: Hmmm. I guess I'll get Null pointer exception for an empty tree. Let me fix that by adding a null check.

*I*: Now it looks good. Anything else you are missing.

*C*: No, I think other things I have covered like no leaves, one leaf, etc.***(Notice how he calls out each case he considered)***

*I*: Cool. I am good. Any questions? :)

## Feedback
So what do you think about this interview?
* The candidate clarified the requirements before starting implementation.
* The candidate also froze the requirements by running through a few examples and clarifying his understanding.
* The candidate came up with a working solution without any probing.
* The candidate proactively discussed the time and space complexities.
* While coding, the candidate had a clear vision of what he was doing and where he was going.
* The candidate had a bug in his code, and when asked to check for errors, he found the error and rectified it themselves.

## Conclusion
Interviewing is a completely different skill from coding. Even though you are good at problem-solving, the interview is a setting where the interviewer is trying to decide between hiring you or not. So in addition to coding, you also need to understand the interviewer's perspective so that you make it easy for him to hire you. In this article, I wanted to compare and contrast a good interview vs a mediocre one. Try to practice interview skills separately as the more you practice the better you get at it. You can [reach out](https://kaizencoder.com/about) to me if you need help taking mock interviews.
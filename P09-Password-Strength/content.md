---
title: "React Redux Password Strength"
slug: react-redux-password-strength
---

# What makes a strong password? 

Good question! Passwords, as a subject, are worthy of an entire class! 
For our purpose we will just look at a few features in the broad
topic. 

The goal is create a view that can display a strength rating for 
any given password. 

Read this post if you are interested in how passwords are guessed by 
hackers. 

- https://nulab-inc.com/blog/nulab/password-strength/

Here is a library that rates passwords:

- https://github.com/dropbox/zxcvbn

## Challenges 

Evaluate and dipslay the password strength. 

## Using the zxcvbn Library

This library is easy to use just follow these three steps: 

1. Add it as a dependency: `npm i --save zxcvbn`
2. Import it into a component: `import zxcvbn from 'zxcvbn'`
3. Call the method with password you'd like to evaluate: `zxcvbn('p@$$w0rd')`

The `zxcvbn()` method returns an object with data that evaluates the 
input password. 

This object has lots of properties. Think of different ways to display
this information. Log the object to the console and take a look at the 
properties.

`score` and `guesses` would be a good starting point. Score is a value from 
0 to 4, making this the easiest to work with. 

crack_times_seconds might also be interesting to show. 

Think of interesting ways you can display some the other proprties. 

### Stretch Challenges 

**Make a Component**

Make a Component dedicated to displaying password strength. 
Pass the object from zxcvbn to this component, or it might be 
better still to pass the password in and have this component 
run the evaluation. 

**Style the evaluation**

Style the password evaluation. Think about how you can graphically 
describe the password strength. Try any or all of these ideas: 

- Set the background color based on strength
- Show a bar that expands with a higher score
- Set the width of and color of the bar




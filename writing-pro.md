## Intro

### Goals
+ Write a great techical documents (proposals, design docs, tutorials, etc). <br>
+ Write a documentary short stories.

### Context
A few years ago, when seeing the term "tech writing", I imagined the folks who write a documentation for the developers about how to use a specific API (e.g. documentation on iOS frameworks, Microsoft WINAPI docs etc). 
Now I perceive a process of tech writing as creating a clear, engaging, and well-covered Confluence docs on the company's products/frameworks/processes/solutions/etc.
I think it's critical to write a good documentation, and an importance is directly proportional to the number of people in the company.        

## Resources
*I tried not to break the copyright rules by quoting the chunks from the resources. But as I don't put the link for each quote, formally I break the rules.*
1. ["The Staff Engineer's Path" by Tanya Reilly](https://www.oreilly.com/library/view/the-staff-engineers/9781098118723/)
2. ["What I Think About When I Edit" by Eva Parish](https://evaparish.com/blog/how-i-edit)

## Techniques
### Where to start when writing anything

> I recommend writing a preamble, just for your own use, on everything you write. Take a few minutes and consider what you’re trying to say. 
> + What is your main point? 
> + Who are you writing for? 
> Then actually write this information down at the top of your document (or notebook, or cafe napkin) so it’s there staring you in the face as you work. 
> As you write, and as you edit, you can compare what you have on the page to what you set out to do.

### A possible structure of a technical doc
so I want to write a doc on some stuff. for a more concrete example let’s assume it’s a Confluence doc. 

#### context
when it was created, what’s the status of it (in progress/done/design review). who are the owners of it. links to the other related docs. 

#### goals
what is the purpose of this doc. what is the problem and why is it the right problem. the goals should not contain any design decisions, esp high level ones. the design should serve the goals, not vice versa.

#### design
the approach of how to solve the problem. diagrams. proofs that the proposed soliton will work. if there are dependencies on another systems and components, describe how they will be used, so reviewers can catch some misunderstandings. 

> Depending on what you’re trying to do, it could include:
> * APIs
> * pseudocode or code snippets
> * architectural diagrams
> * data models
> * wireframes or screenshots
> * steps in a process
> * mental models of how components fit together
> * organisational charts
> * vendor costs
> * dependencies

at the end of this section, the readers should understand what you intend to do, and they should have enough info in order to tell you whether they think it will work. 
it’s better to be concrete than vague here, because if someone will argue on this step and catch a mistake, the mistake will be very cheap at this point. 


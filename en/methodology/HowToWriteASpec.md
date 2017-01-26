So **why** should we write specs? you may be asking.

> Why won't people write specs? People claim that it's because they're saving time by skipping the spec-writing phase. They act as if spec-writing was a luxury reserved for NASA space shuttle engineers, or people who work for giant, established insurance companies. Balderdash. First of all, failing to write a spec is the single biggest unnecessary risk you take in a software project. It's as stupid as setting off to cross the Mojave desert with just the clothes on your back, hoping to "wing it." Programmers and software engineers who dive into code without writing a spec tend to think they're cool gunslingers, shooting from the hip. They're not. They are terribly unproductive. They write bad code and produce shoddy software, and they threaten their projects by taking giant risks which are completely uncalled for.

*– Joel Spolsky on [Painless Functional Specifications](http://www.joelonsoftware.com/articles/fog0000000036.html)*

## Contents

- Sections
  - [Disclaimer](#disclaimer)
  - [Author](#author)
  - [Problem Overview](#problem-overview)
  - [Constraints](#constraints)
  - [Background](#background)
  - [Theory of Operation](#theory-of-operation)
  	* [Black box](#black-box)
  	* [Hypothesis](#hypothesis)
	* [Functional Specification](#functional-specification)
	* [Technical Specification](#technical-specification)
  - [Open Issues](#open-issues)
- Considerations
  - [Divide and Conquer](#divide-and-conquer)
  - [Diagrams](#diagrams)
  - [Specs should be validated](#specs-should-be-validated)
  - [Specs should be maintained](#specs-should-be-maintained)
  - [Side Notes](#side-notes)
  
  ## Sections

All specs should include the following sections. 

We're heavily based on Joel Spolsky's [Painless Functional Specifications - Part 2: What's a Spec?](http://www.joelonsoftware.com/articles/fog0000000035.html)

## Disclaimer

The current status of the spec, i.e "This spec is not complete, is missing x" or "This spec is considered complete".

## Author

Someone must take responsability and ownership of the document. Only one person here.

## Problem Overview

This is a description that people will usually see before anything else. This is the big picture. Include diagrams if needed.

## Constraints

You should also define the constraints of the problem. There is no single system that behaves the same way, no matter the surrounding conditions, so make sure to list all the conditions and their importance. What may be a problem in a small computer may not be in a server.

## Background
This is the summary of the previous work done on this problem: research, failed attempts or improvements done by you or someone else. Be as clear as possible in this stage because this is how you will justify your course of action.

## Theory of operation

This section is all about the details. People will usually skim the document until they need to know a particular detail. Describe with detail how everything in your system will work, down to actual pseudo-code, objects, interfaces, messages, etc.

### Black box

In this section, you will present a black box diagram. A black box diagram, is an object which can be viewed in terms of its input, ouput and messages without any knowledge of its internal workings. [Wikipedia](http://en.wikipedia.org/wiki/Black_box).

### Hypothesis
The Hypothesis is the foundation for your solution. It is a single sentence in which the solution is based. In some cases, it can be more than one sentence but keep it simple: it’s better to create more specs instead of trying to fit all into one.

For example.

* This design will handle at least 10k request per second.
* There's an API that I can use to get X data.

Later you have to prove those with a small prototype, a benchmark or relevant data.

### Functional Specification
This is a detailed version of the solution proposal. Here you should be using diagrams, storyboards and text in an organized way that describes the different states, buttons or APIS on your solution. All the components and moving pieces of your solution should be specified. Think of this section as the anatomy of the solution.

### Technical Specification

In the technical spec, you describe the implementation using pseudo-code (Check [Why should I use pseudo-code](#why-should-i-use-pseudo-code)).

The idea is to define both the API and the Implementation of your classes/objects, this way thinking in advance all the problems you may have when implementing this in actual code.

For example, let's write a quick implementation of a PubSub class.

```
Class PubSub ->
  publish: -> (String eventName, Object data)
  	let data be data or {}
  	
	if self.events includes eventName
		for each callback in self.events[eventName]
			call callback(data)
    
  subscribe: -> (String eventName, F() callback)
  	let self.events be self.events or {}

  	if self.events not includes eventName
  		set self.events[eventName] to []
  	
  	push callback into self.event[eventName]
```

We describe the arguments the function is expecting, the actual implementation using pseudo-code, the idea is that the implemetation is language agnostic, so you can recode this in any language that you want (in this case, at least one language that has lambdas).

#### Why should I use pseudo-code

When doing your first implementation, you will be tempted to just copy paste the code you wrote in your spec as production code. Writing code using pseudo-code doesn't let you do this, and while you are writing this to actual code, it will give a second time to review what you just plan to do, and also you maybe you will find bugs or errors when writing from pseudo-code to actual code.

## Open Issues

What is this spec missing? What it doesn't solve? This section is good to generate discussion on how to solve them. By the time the programmers start work, all of these need to be stomped out and this section will be empty.

## Considerations

## Divide and conquer

A single project may and will contain several specs. If you're feeling like writing an IBM manual from the 80's, that's pretty much the signal that the system, and thus the spec, needs to be broken down in sub-systems.

## Diagrams

Diagrams are your friends but you should only include ASCII diagrams as they're the most text friendly out there. You can use services like [asciiflow](http://asciiflow.com) for easy edition.

## Specs should be validated

Before implementing them they should be approved by at least one peer.

## Specs should be maintained

If the code is not considered not "code complete" and there's design changes, the spec should always reflect that. If the spec goes out of date then the maintainer is to be blamed. Quoting Joel:

> The updating continues as the product is developed and new decisions are made. The spec always reflects our best collective understanding of how the product is going to work. The spec is only frozen when the product is code complete (that is, when all functionality is complete, but there's still testing and debugging work.)

## Side Notes

While you're writing a spec, remember your various audiences: programmers, testers, marketing, tech writers, etc. Leave side notes all over the spec whenever is needed. Labeling them as "Technical note", "Marketing note", "Testing note" etc will make sure people can easily browse your document for the notes they're interested.

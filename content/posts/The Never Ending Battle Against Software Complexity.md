
## What is Complexity?

Recently, I finished reading "A Philosophy of Software Design" and in the second chapter, it explores the topic of Software Complexity.   

The book "A Philosophy of Software Design" defines complexity practically:

> "Complexity is anything related to the structure of a software system that makes it hard to understand and modify."

In other words, complexity can take many forms, and doesnt necessary has anything to do with performance, your code can be performant and still be complex

I'd like to share some key definitions and insights from the book in this article. But first, let's imagine a common situation that probably you’ve already been to…

---
## A Short Horror Story

Let's dive into a horror story many of you have probably experienced or will experience.

1. It started with a simple CRUD task management app. The code was clean, modular, and easy to maintain. The development team was happy, and the system worked perfectly for initial clients.
    
2. Problems began when the sales team sold the system to a large company, claiming it had calendar integration, email notifications, and an amazing report generator. With the sale finalized, these features had to be implemented quickly.
    
3. **Calendar Integration:** The team had to integrate with Google Calendar and Outlook. Different developers implemented the solutions, resulting in inconsistent approaches.
    
4. **Email Notifications:** Email notifications were added next. One developer used a specific library, while another created a custom solution. The mixed approaches made the code confusing.
    
5. **Report Generator:** For the report generator, developers used various technologies: PDFs, Excel exports, and interactive dashboards. The lack of a unified approach made maintenance a nightmare.
    
6. **Growing Complexity:** Each feature was developed in isolation and quickly, leading to dependencies between features. Developers started creating "quick fixes" to make everything work, increasing the system's complexity and coupling.

Software development doesn't happen in a vacuum; various internal and external factors influence it. We've all been, or will be, in a situation like this.

---
## The Beginning of the End

Then the problems began:

1. Changes in one part of the system affected other parts unexpectedly.
2. Small changes required modifications in many other files, making estimations difficult.
3. Month after month, the code became harder to understand, often fixed through trial and error.
4. Productivity declined, and everyone dreaded maintenance tasks.
5. The inevitable call for "We need to refactor."
6. Certain tasks could only be handled by specific developers (classic)
7. Over time, the once beautifully written and well-documented software became a train wreck.

## Naming the Symptoms

It's clear we now have a complex system. 

Now let's "dissect" this complexity to make it easier to identify and mitigate it. 

Well, "mitigate" means:

> "To make less severe, serious, or painful; to alleviate."

I believe complexity is often inherent in code. Some things are complex by nature. Your role as a developer isn't just to create code that the computer can execute efficiently but also to create code that future developers (including your future self) can work with.

> “Controlling complexity is the essence of computer programming.”  
> — Brian Kernighan


The author of the mentioned book states that complexity typically manifests in three ways, which we will explore here.

## Change Amplification

> Change amplification occurs when a seemingly simple change requires modifications in many different places.

For example, if the Product Owner requests a "priority" or "completion date" field and your entities are tightly coupled, how many changes would you need to make?

## Cognitive Load

> Cognitive load refers to the amount of knowledge and time a developer needs to complete a task.

So imagine this scenario: A new developer joined the team, he was assigned to fix a bug in the report generator. To complete this task, the dev needed to:

- Understand the different calendar integrations (Google and Outlook).
- Grasp the distinct approaches to email notifications.
- Navigate through the fragmented code of the report generator, dealing with PDFs, Excel, and dashboards.
- Integrate these diverse technologies and styles to find and fix the bug.

It's the classic "impossible to estimate" scenario, where the task could take one point or eight—better roll a D20 and respond accordingly.

## Unknown Unknowns

> Unknown unknowns are when you don't know what you don't know.

This is the worst manifestation of complexity because you might alter things you shouldn't, causing everything to break.

Example: A developer modified the email-sending code to add a new notification, unaware that it would affect the report generator, which depended on that function. This caused significant issues for clients, exemplifying the worst form of emergent complexity.

## Causes of Complexity

Having seen the horror story and the three main symptoms, let's look at what causes complexity.

### 1. Dependencies

Dependencies are essential in software and cannot be completely eliminated. They allow different parts of the system to interact and function together. However, dependencies, when not managed properly, can significantly increase complexity.

#### Definition:

> A dependency exists when code cannot be understood or modified in isolation, requiring consideration or modification of related code.

#### Types of Dependencies:

- **Direct Dependencies:** When a module or class relies directly on another. For example, if Class A calls a method from Class B, Class A is directly dependent on Class B.
- **Transitive Dependencies:** These occur indirectly. For instance, if Class A depends on Class B, and Class B depends on Class C, then Class A has a transitive dependency on Class C.
- **Cyclic Dependencies:** These are the worst form of dependencies where a group of modules are interdependent in a circular manner. This can lead to severe maintenance and scalability issues.

### 2. Obscurity

Obscurity occurs when important information is not obvious. This can make the codebase hard to understand, leading to increased cognitive load and the risk of unknown unknowns.

#### Definition:

> Obscurity occurs when important information is not obvious.

#### Examples of Obscurity:

- **Poorly Named Variables and Functions:** Names that do not convey the purpose or usage can lead to confusion. For instance, variables named `x` or `temp` without context.
- **Hidden Side Effects:** Functions that modify state or perform actions that are not apparent from their signature can introduce obscurity. For example, a method named `calculateTotal` that also updates the database.
- **Global State:** Overuse of global variables can lead to hidden dependencies and side effects, making the code difficult to understand and predict.
- **Deep Inheritance Hierarchies:** Inheritance can obscure the actual behavior of classes, especially when behavior is spread across multiple levels of the hierarchy.

## Remember: Complexity is Incremental

- Complexity is rarely caused by a single "error" or bad decision.
- Complexity builds up "slowly" through bad decisions and dependencies over time.

Because it is incremental, it's easy to think, "just this once, it won't matter." But when accumulated, fixing one or two dependencies alone won't make much difference.

> “Everything is a tradeoff in software engineering.”
> — I don't remember the author

# Conclusion

I could  write a lot of rules, stratategies and frameworks and  that you priobably already saw in the intenert on hjow to avoid complexity: SOLID, Design Patterns, Yagni, KISS etc etc

However, you can unify them all into one guiding principle (as mentioned in "The Pragmatic Programmer."):  **"Is what I am implementing easy to change?"** If the answer is no, then you are probably increasing complexity. 

Ensuring that your code is easy to change not only simplifies maintenance but also reduces the cognitive load on developers, making the system more adaptable and less error-prone over time.



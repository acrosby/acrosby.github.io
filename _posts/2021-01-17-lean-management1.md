---
layout: post
title:  "Lean Philosophy"
categories: management
tags: development management lean
---

Given my experience and education, I have always been sort of philosophically aligned with the concepts in ["Lean"](https://en.wikipedia.org/wiki/Lean_software_development#Amplify_learning) management, production, and software development thought to have originated at Toyota in the 90's. Using software as example, those are:

* Eliminate Waste
  >  If some activity could be bypassed or the result could be achieved without it, it is waste. Partially done coding eventually abandoned during the development process is waste. Extra features like paperwork and features not often used by customers are waste. Switching people between tasks is waste. Waiting for other activities, teams, processes is waste. [(from wikipedia)](https://en.wikipedia.org/wiki/Lean_software_development#Eliminate_waste)
* Amplify Learning
  >  Software design is a problem-solving process involving the developers writing the code and what they have learned. Software value is measured in fitness for use and not in conformance to requirements. [(from wikipedia)](https://en.wikipedia.org/wiki/Lean_software_development#Amplify_learning)
* Decide Late
  > As software development is always associated with some uncertainty, better results should be achieved with a set-based or options-based approach, delaying decisions as much as possible until they can be made based on facts and not on uncertain assumptions and predictions. The more complex a system is, the more capacity for change should be built into it, thus enabling the delay of important and crucial commitments. The iterative approach promotes this principle – the ability to adapt to changes and correct mistakes, which might be very costly if discovered after the release of the system. [(from wikipedia)](https://en.wikipedia.org/wiki/Lean_software_development#Decide_as_late_as_possible)
* Deliver Fast
  > In the era of rapid technology evolution, it is not the biggest that survives, but the fastest. The sooner the end product is delivered without major defects, the sooner feedback can be received, and incorporated into the next iteration. The shorter the iterations, the better the learning and communication within the team...The myth underlying with this principle is haste makes waste. However, lean implementation has provided that it is a good practice to deliver fast in order to see and analyze the output at the earliest. [(from wikipedia)](https://en.wikipedia.org/wiki/Lean_software_development#Deliver_as_fast_as_possible)
* Empower the Team
  > ...managers are taught how to listen to the developers, so they can explain better what actions might be taken, as well as provide suggestions for improvements. The lean approach follows the agile principle "build projects around motivated individuals [...] (sic) and trust them to get the job done", encouraging progress, catching errors, and removing impediments, but not micro-managing...The developers should be given access to the customer; the team leader should provide support and help in difficult situations, as well as ensure that skepticism does not ruin the team’s spirit. Respecting people and acknowledging their work is one way to empower the team. [(from wikipedia)](https://en.wikipedia.org/wiki/Lean_software_development#Empower_the_team)
* Build Integrity In
  > Conceptual integrity means that the system’s separate components work well together as a whole with balance between flexibility, maintainability, efficiency, and responsiveness. This could be achieved by understanding the problem domain and solving it at the same time, not sequentially. The needed information is received in small batch pieces – not in one vast chunk...One of the healthy ways towards integral architecture is refactoring. As more features are added to the original code base, the harder it becomes to add further improvements. Refactoring is about keeping simplicity, clarity, minimum number of features in the code. [(from wikipedia)](https://en.wikipedia.org/wiki/Lean_software_development#Build_integrity_in)
* Optimize the Whole
  >  --by decomposing the big tasks into smaller tasks, and by standardizing different stages of development, the root causes of defects should be found and eliminated. The larger the system, the more organizations that are involved in its development and the more parts are developed by different teams, the greater the importance of having well defined relationships...in order to produce a system with smoothly interacting components. [(from wikipedia)](https://en.wikipedia.org/wiki/Lean_software_development#Optimize_the_whole)

The next points are hopefully not a regurgitation of "Lean" principles so much as documentation of my perspective, and what to continually keep in mind while managing projects or developing software.

* Explore and play to understand the existing context and work space, continue to learn and adapt processes and methodologies as you do.
* Do the minimum viable amount of work to solve a problem and/or deliver the minimal viable product (known as MVP in the startup world).
* Build iteratively, refactor early, assume evolution
* Good names/language and clear structure are self documenting: think about consistency, clarity, and transparency.
* Just try it: Let things fail early and fail hard. Learn from failures to achieve a more complete undertanding.

Here is a structure that I follow when executing a task or making a change:

* Make an effort to understand what is already there, assume it generally works as intended and that functionality is depended on.
* What can be reused, adapted, or modified without changing pre-existing behavior?
* Can this change be made to fit into the pre-existing paradigm?
* Does your problem differ from that of others?
* What elements of your new changes can be reused? Have they been made modular?
* Could someone carry on without my input, and will others understand what I've done?
* What parts of this process (at any level) can be automated as to avoid undue waste of others' time or my own?


It's interesting that most if not all of these bullets can be not only applied to a lot of different management and development tasks, but projected to most of our day in and out of work. Consider that every task undertaken is in maintenance of one thing or another (good or bad)--a car, a home, a relationship, a community, etc. We are all part of a complex system with continually changing requirements and sometimes opposing goals. Our actions, changes we make, and the elements we focus on maintaining, all play a role.

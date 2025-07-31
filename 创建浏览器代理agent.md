# agentq
dpo
## 网页代理

从网上购物代理下单的

# web agents
## autonomous software program
- 1.automates repetitive tasks
- 2.gathers data
- 3.monitor sites
# applications
- search engines
- e-commerce
- social media
- data analysis
# key components

<img width="808" height="447" alt="image" src="https://github.com/user-attachments/assets/574fa847-0691-4af7-bfae-4f772ae8ffc2" />

# 根据learningai网页构建一个处理视觉信息就是截图的代理
以及结构信息，就是网站的html 的dom表示的，

代理如何处理网页的dom结构理解网页的？

<img width="812" height="443" alt="image" src="https://github.com/user-attachments/assets/a615498d-45d4-463f-bcff-6fc462d7e8dc" />

<img width="558" height="370" alt="image" src="https://github.com/user-attachments/assets/382dc2ad-0045-44a8-b6db-eff715d9af2a" />

# limitations to existing frameworks

- 1. reliability & trust
- 2.decision-making errors
- 3.plan divergence&looping
## compounding mistakes
- early errors snowball
- lack of self-correction
- LIMITed context
- inconsistent reasoning
- biases in training data

<img width="734" height="422" alt="image" src="https://github.com/user-attachments/assets/c6cbbe00-8a19-4813-80f8-488d010a494e" />

### decision-making errors

exploration:breadth first search

<img width="763" height="385" alt="image" src="https://github.com/user-attachments/assets/4ad4b7ab-f67e-4a47-86d2-cd404be2e437" />

## plain divergence & looping

limitations to existing frameworks

1.reliability & trust

2.decision-making errors

3.plan divergence & looping

<img width="796" height="411" alt="image" src="https://github.com/user-attachments/assets/6a5401ac-5fc4-409d-85cd-335f237e76ad" />

即使是高级代理也缺乏自我纠错的能力

# 构建一个代理，抓去网页，根据自然语言指令将结构以结构话形式输出
<img width="373" height="363" alt="image" src="https://github.com/user-attachments/assets/ba5db49b-4364-4af8-ab21-71eb576eb527" />



# 1
Transcript
0:00 Welcome to "Building AI Browser Agents", built in partnership with AGI Inc.
0:05 AI browser or AI web agents can log into websites
0:09 fill out forms, click through web pages, or even place an online order for you.
0:14 Your AI web agent can use both visual information
0:17 that is, screenshots and structural information
0:21 such as the HTML or the Document Object Model (DOM)
0:24 representation of a web page to reason and take actions.
0:29 If you open a page on a website and take a look at the code underlying
0:33 that web page, you see how large the action space can be for the agent
0:36 at each step.
0:38 Since these agents can run long sequences of actions automatically,
0:42 any error can have unintended consequences like paying for the wrong flights
0:46 or ordering random products, or if the agent misreads a single field,
0:51 say a product name,
0:52 it can hit down the wrong path entirely, and these errors can compound quickly.
0:56 In this course,
0:57 you'll learn about these problems and several approaches to tackle them.
1:00 I'm delighted to introduce
1:02 the instructors Div Garg and Naman Garg, who are the co-founders of AGI Inc.
1:07 Div, Naman, and their team have built MultiOn, which is a web agent platform
1:12 that is based on the approach that they published in the AgentQ paper.
1:16 Thanks Andrew.
1:17 To address the challenges you mentioned, we have introduced
1:21 AgentQ. AgentQ combines Monte Carlo Tree Search (or MCTS) with a self critic
1:26 mechanism and iterative fine-tuning using Direct Preference Optimization, or DPO.
1:32 During the search process of AgentQ, different branches
1:34 or sequential actions are explored and the outcomes are evaluated.
1:38 The simulations combined with their feedback, are used to create
1:40 preference pairs at each node of the search tree.
1:42 The DPO algorithm is then used to fine tune the underlying language policy model
1:46 by learning from this high level preferences.
1:48 This helps favor actions that lead to better outcomes
1:51 or are ranked higher by the AI feedback.
1:54 In this course, you will build several web agents.
1:57 You will build a simple web agent that analyzes DeepLearning.AI website,
2:02 and list all the courses on a specific topic.
2:05 Then you will extend this to taking actions like clicking on a course
2:10 or summarizing it, and even signing up for a batch newsletter.
2:13 Next, you will dive deep into MCTS that is an integral part of our AgentQ method
2:19 and solve a grid world problem of finding the optimal path, we will then
2:23 explore a variant of AgentQ plus MCTS that takes a course title
2:28 and searches the web and navigates the result until it finds the right course.
2:32 You will visualize and analyze different tree paths
2:35 the agent takes until it accomplishes the goal.
2:38 Many people have worked to create this course.
2:40 I'd like to thank Michelle Gee
2:41 and Milind Maiti from AGI Inc. From DeepLearning.AI,
2:46 Esmaeil Gargari and Geoff Ladwig have also contributed to this course.
2:51 The first lesson will be an introduction to AI web agents.
2:54 That sounds great!
2:56 Now let's have you, rather than your web agent, get started.


# p2

Transcript
0:00 In this lesson, we'll jump right into what web agents are and how they can be
0:04 used to automate tasks online, like purchasing an item on an e-commerce website.
0:08 We will also discuss common challenges such as reliability issues,
0:12 compounding errors, and agents getting stuck in loops.
0:15 Let's go.
0:16 First, let's see a real-world example.
0:19 Imagine you want to purchase books online.
0:21 But don't have time to search and check out.
0:24 In this demo, we have asked our web agent
0:26 to order two books that are "Radical Candor" and "The Cold Start Problem",
0:31 and add them to our cart on Amazon.
0:35 Here, we notice
0:36 how the agent is navigating to Amazon just like a human would.
0:40 It's intentionally searching for the first book.
0:45 Once it finds the book
0:47 and proceeds to add it to the cart.
0:50 and proceeds to add it to the cart.
0:51 Next, it goes and starts searching for the second book.
0:58 And then
0:58 also proceeds and adds it to the cart.
1:03 And here we see the agent exactly, in a sense, where to click
1:06 And how to navigate the website.
1:11 Finally, the agent can go and place the order.
1:17 As you can see, the agent successfully found both books
1:20 and added them to the cart without any human intervention.
1:24 This is just one example of what web agents can do.
1:25 Imagine all the possibilities.
1:29 These agents could automate tasks across virtually any website
1:33 on the internet.
1:36 A web agent is an autonomous software program
1:37 that performs on a task automatically on our behalf.
1:40 These intelligent agents having created various purposes
1:44 such as automating repetitive online tasks,
1:48 gathering data from multiple sources
1:52 or monitoring websites,
1:53 for changes or updates.
1:56 Web agents can power complex applications in our daily digital lives.
2:01 This range from an online search
2:03 that goes beyond simple queries,
2:06 e-commerce assistance for finding products and completing
2:09 purchases, social media management including monitoring and automated posting,
2:14 data analysis
2:15 across multiple platforms, customer support automation,
2:19 cloud booking and planning, as well as specialized
2:23 applications in finance, healthcare and many other industries.
2:27 Now let's see the key components
2:29 for building web agents.
2:32 Here we explore the architecture
2:34 on how these agents work.
2:37 A well designed web agent consists of five essential modules.
2:41 The user interface module, which allows people to communicate with the agent
2:45 using natural language.
2:47 The control module,
2:49 which acts as the brain of the system and hence reasoning and decision
2:53 making for actions.
2:55 The third is the knowledge base where the agents stores important data, rules, and
2:58 information needed to complete tasks.
3:01 The fourth is a communication module
3:03 that manages interactions with websites, API's and other systems.
3:08 And finally, the data processing module,
3:11 which analyzes, processes and transforms data before returning the results.
3:14 Within these modules, several specialized components
3:17 work together.
3:20 First, it parsers that can systematically extract
3:24 website data, and interpret HTML.
3:26 Second, action models that through decision
3:29 making and predict actions to take. Third, executors that execute
3:34 specific actions on the website, such as clicks, form filling, etc...
3:40 Here's how the entire process flows.
3:43 First, a human provides a request to the agent.
3:47 The agent understands the user's request.
3:50 It personalizes its approach based on the context.
3:54 The action model takes
3:56 of the representation of the website
4:00 and determines what actions to take on the webpage.
4:04 Next, the model predicts what is the optimal action in the setting.
4:08 In the second, this action is then executed on the website.
4:12 The cycle repeats until the task is complete.
4:14 Let's see an example.
4:16 Here is a screenshot of the DeepLearning.AI website
4:20 first page.
4:21 You are going to build an
4:22 agent that processes both visual information
4:26 like screenshots, as well as structural function.
4:30 That is the HTML DOM representation of the website,
4:33 that can navigate to find courses
4:36 on DeepLearning.AI and do a website
4:39 interactions. Now we explore how agents can process
4:43 the complex structure to understand HTML elements,
4:48 web agents can interact with virtually any HTML element on a webpage.
4:51 This can range from links to Textarea finding
4:56 information, checkboxes, for making selections,
5:00 radio buttons
5:02 for choosing options,
5:04 Dropdown menus for selecting from lists
5:07 Buttons for submitting forms or triggering actions
5:10 As well as reset button fields.
5:12 To understand the limitations of existing frameworks, let's examine the key steps
5:15 an agent follows. First, planning.
5:19 Determining what actions to take.
5:21 Second, reasoning.
5:23 Making decisions based on the available information.
5:26 Third, environmental actions.
5:29 Executing the planned actions.
5:32 Finally, explanations.
5:34 That is communicating to the user what was done and why.
5:38 There are many issues that occurred during this reasoning phase.
5:41 If an agent cannot perform a reasonable plan, it may make incorrect decisions.
5:46 This is why improving reasoning is a critical
5:48 focus in later lessons.
5:52 Let's see the main limitations
5:54 of existing autonomous agent frameworks.
5:57 First.
5:58 Reliability and trust challenges.
6:01 Ensuring automation systems can be trusted
6:04 with mechanisms for human rights.
6:07 Second, decision making errors
6:10 where there is compounding mistakes
6:12 and tradeoffs between exploration and exploitation.
6:16 And finally, plan divergence and looping.
6:19 Whether there are risks of breaking cycles
6:21 or divergence plan during agent execution.
6:24 First, it's very hard to establish reliability and trust.
6:28 With current autonomous systems,
6:30 they are stochastic and things can go wrong.
6:33 When it comes to decision-making errors,
6:36 agents suffer from compounding mistakes.
6:39 That is a cascade of errors that can grow over time. Early errors can snowball
6:43 into larger problems as they influence
6:45 subsequent decisions. Lack of self-corrections.
6:48 Means agents can identify and fix their own mistakes.
6:52 This can lead to catastrophic failures as errors accumulate and magnify.
6:56 Limited context.
6:58 Agents may miss critical information while making decisions
7:00 without complete context,
7:03 choices become increasingly flawed.
7:06 Inconsistent reasoning decisions based on incomplete natural processes
7:11 leads to empathetic behavior and unreliable outcomes.
7:16 Biased problems. Which might be present in training data can be amplified in
7:20 agent decisions. Over time, this creates increasingly skewed or unfair results.
7:26 Together, these issues significantly undermine the decision-making
7:30 capabilities
7:31 of autonomous agents.
7:34 Web agents constantly face a critical decision-making challenge.
7:38 Should they exploit what they already know? Or should they explore new possibilities?
7:43 These trade-offs fundamentally shape how agents navigate websites.
7:47 In the exploitation
7:47 strategy, agents focus on maximizing rewards.
7:51 They follow single path deeply before considering alternatives.
7:55 They explore the children elements in the DOM tree
7:58 and use recursion to navigate deeper into the promising paths.
8:02 The advantages of exploitation are that it maximizes the current rewards
8:06 by leveraging known successful strategies.
8:09 It allows efficient use of resources on paths
8:13 with non-proven values that gives more predictable performance
8:17 in familiar environments.
8:19 It also has a lot of disadvantages where you can miss alternative paths.
8:24 The agents can be locked into the current strategy.
8:27 They might be unable to adapt if the chosen path is suboptimal.
8:31 Now we examine the alternative approach, exploration.
8:35 In exploration, agents use a breadth first search strategy.
8:40 The agent tries new untested paths
8:42 to discover potentially better rewards and strategies.
8:45 Rather than going deep, it goes and explores all possible directions.
8:48 As shown in the diagram,
8:50 the agent examines all child elements at each level before going deeper.
8:54 When a promising part is found, the agent continues exploration.
8:59 If a path doesn't lead to the desired state
9:00 the agent can backtrack and it can try alternatives.
9:04 This creates a broader search pattern across the whole website structure.
9:08 It has advantages that can unlock new opportunities
9:11 of discovering higher rewards or better paths that were not previously known.
9:16 It can prevent stagnation, reduces the risk
9:19 of being stuck in suboptimal strategies,
9:22 and it enables adaptation to changing environments or requirements.
9:27 It also has a couple of disadvantages,
9:30 such as it might have more immediate cost.
9:33 Exploration may not yield
9:35 immediate rewards and could even lead to worse outcomes.
9:38 It can lead to the risk of extra time.
9:40 Pursuing unknown paths can result in efficient use of resources and time,
9:45 and also increasing complexity in decision-making processes.
9:49 The critical challenge for web agents is determining when
9:51 explore vs when to exploit.
9:54 Choosing incorrectly between strategies is a common source of decision
9:57 making errors.
9:59 The ideal approach often involves balancing both strategies
10:02 proactively based on context.
10:05 Now, we examine a critical challenge facing automizations.
10:10 When they stray away from their intended path.
10:12 Among the limitations in current frameworks,
10:15 we'll now focus on plan divergence and looping behaviors.
10:19 Plan divergence happens when an agent veers of course.
10:23 In this diagram, you can see the ideal path as a straight line. But the actual path
10:26 diverse significantly. Like asking an assistant to summarize a topic
10:31 but receiving unrelated information instead.
10:34 Even advanced AI agents lack the ability to self-correct when
10:37 they make mistakes. Once an agent deviates or gets stuck,
10:41 recovery becomes extremely difficult due to three key factors.
10:44 First, agents typically have limited
10:47 domain knowledge, they are trained on general information
10:50 but struggle with specialized tasks. Second, unexpected
10:54 changes in the environment can confuse an agent causing it to repeat ineffective actions
10:58 rather than adapt. Finally, insufficient training data makes it difficult
11:02 for agents to navigate unfamiliar situations, and recognize when they should backtrack.
11:07 In this lesson, we explored what agents are.
11:10 What are the key components in building them. And the main issues. In the next lessons,
11:15 you will learn how to address these fundamental challenges.

# p3

0:07
/
7:35
Transcript
0:00 In this lesson,
0:01 you will build a simple web agent that is capable of scraping the web
0:05 and providing the results
0:06 as a structured output based on natural language instructions.
0:10 All right, let's dive into the code.
0:12 So, in this lesson we are going to be building a simple web agent. Here,
0:18 We are calling it a learning recommender agent.
0:21 Here we start with navigating to the DeepLearning.AI website,
0:25 and we ask the agent to scrape the courses,
0:28 list a specific course on a specific topic,
0:30 and then read the details and learning objectives of that course.
0:35 Now let's go to the lab.
0:37 So we are going to start with importing our libraries.
0:40 In this lesson we are going to be using Pandas,
0:43 playwright.asyncio, OpenAI, web client,
0:47 an image library to display our screenshot data
0:50 and same for IPython.
0:52 And then we are going to be using our helper functions.
0:55 Then we start with initializing our
0:58 OpenIA client with the API key.
0:59 OpenIA client with the API key.
1:01 And we also make sure our notebook can run asynchronously.
1:06 I'm going to run this.
1:08 And then we already have the key set up for you in the DeepLearning.AI platform.
1:12 We are going to start with creating a simple web scraping agent.
1:16 So, here we describe a web scraper agent, we initialize it.
1:21 We also initializing our browser
1:23 that we are scraping our HTML content.
1:28 We also allow you to take screenshots
1:31 and converting it into a screenshot buffer to better display.
1:35 And finally, you are allowed to close your browser.
1:38 Then we initialize our web agent client.
1:42 We start with creating our structured data format.
1:46 Here, we start describing our DeepLearning.AI course
1:51 which has this title, description, who the presenter is, this image url.
1:55 And the course url.
1:57 Here you create multiple
1:59 DeepLearning.AI courses.
2:01 So we will start with creating our OpenAI client.
2:04 Here we are describing a model, which is typically 4o-mini
2:08 with a static version which is highly fine-tuned
2:11 towards running a script response. So we are describing our
2:15 system prompt which describes the role of the agent. Here,
2:19 we are asking you to act like a web scraping agent and
2:21 it's task is to follow the relevant information
2:25 convert it from HTML to Json.
2:28 And here we allow you to give your own instructions.
2:32 And its objective is to return the title, description, presenter, image url,
2:37 course url, of all the courses in the DeepLearning.AI website.
2:41 And basically instructed to only give JSON and not the format
2:45 that we don't want. Then you give your HTML content to the agent,
2:51 and you also describe the response format
2:54 you want your structured output to be.
2:57 Here,
2:57 you return your structured response.
3:00 In the web scraper,
3:02 this is where everything comes together. You first get your HTML content.
3:07 Then we take a screenshot.
3:10 And finally, you give it to your LLM
3:13 to process and return a structured response.
3:16 And as a way to do it properly,
3:18 we also close our scraper.
3:21 Now let's work on our first example.
3:23 So we first start with our target URL.
3:26 This is where the web page was targeted.
3:29 And, we also define a base URL that we need for displaying
3:32 our final course url.
3:35 then let's give it an instruction.
3:37 So in the instruction
3:38 it's a simple instruction where we ask it to get all the courses.
3:42 And we get the result and screenshot from the web scraper.
3:46 We run this.
3:49 So the agent started extracting the HTML content taking screenshot
3:53 and finally it is processing the results to get our scrape data.
3:59 This might take some time, but we will speed up in post.
4:03 And finally, we have a structured response.
4:05 Here,
4:06 using the visualize Course function, you will visualize your results.
4:10 The details of this is in the helper file.
4:13 And here's our output.
4:15 As you can see, it just scraped all the courses
4:18 that are in the DeepLearning.AI website.
4:21 And it starts with Long-term Agentic Memory
4:23 with LangGraph. A description, who the presenter is.
4:26 The image url.
4:28 And finally, the course url that you can directly navigate to.
4:31 Same with Llama Index,
4:34 Windsurf, course from DeepLearning.AI, Arize,
4:37 and many more.
4:41 And you can also visualize the screenshot of the page that the web scraper agent
4:45 got these courses from. Now let's work on a second example.
4:48 What you can do is you can read the description
4:51 and have the LLM understand what the course is about.
4:55 And only retrieve the course that you are interested in.
4:59 You can ask the agent to read all the description about the course.
5:02 And the description can be given the title,
5:05 some of the course summary, even like who the presenter is
5:09 and some overall details that are not visible here.
5:13 And that way LLM has information that is not visible to you,
5:17 but it has an inherent understanding of what the course is about.
5:21 Now we will give you the instruction
5:24 that follows it reading a description about the course
5:28 and only giving three courses that are about the subject.
5:31 And we make sure that it does not give any other course an output.
5:36 Here the course we are choosing is
5:37 "Retrieval Augmented Generation (RAG)."
5:40 And now let's processes our results.
5:43 Now that we've generated our instruction's response.
5:45 We can use the visualize function again
5:48 to see our structured response visualization.
5:51 Here, now the courses that our agent is returning is about RAG.
5:56 So you can see if it was able to find this courses in RAG, course description
6:00 and their tags and labels.
6:02 Now let us see some of the challenges that we have in our web agents.
6:07 Here, if we give it like a bit more complex example.
6:11 Where were suppose
6:11 we will get the summary of it, of course, and provide for the learning from it
6:16 given the subject.
6:17 Let's see what it can return.
6:19 Now, we will use
6:20 our visualization function again to visualize the results.
6:23 What our agent returned.
6:25 And here you see that it followed instructions correctly,
6:29 the instruction was to give us the summary and learnings that we get from it.
6:34 But since the agent was not able to follow our instructions correctly,
6:37 it returned all the courses that are available in the website.
6:41 Now you might be able to
6:43 improve the agent in terms of having it go deeper in the course,
6:48 open the course, get the learnings and description, summary,
6:52 all the teachings and have the agent then able to output that as a structured result.
6:57 But then you're overfitting towards the data.
7:00 But rather, the use case that we want from our agent is
7:03 it needs to understand our task really well and generalize our learnings.
7:08 In this lesson, we learned how to build simple web agents
7:12 that are capable of
7:13 scraping the web and follow our instructions.
7:16 We also notice the challenges where
7:18 sometimes the instructions can be unclear or
7:20 agents just do not have a capability of following that.
7:23 And then they give us the wrong output, which shows the challenges.
7:27 In the next lesson, we'll go over how can we overcome
7:31 some of these challenges that we have seen in our current web agent.

# p4

0:00
/
9:24
Transcript
0:00 In this lesson, you will build
0:01 autonomous web agent that can execute multiple tasks simultaneously.
0:05 You will prompt the agent to perform tasks such as navigating, taking actions,
0:09 summarizing the web pages
0:10 even filling up a form and signing up for a newsletter.
0:13 All right. Let's start coding. Now
0:16 you will make the use case much more complex
0:19 and see how can the agent work fully autonomously.
0:23 The agent will open a course page, to get the summary
0:26 of learning outcomes, and even subscribe for the newsletter.
0:30 In the lab, you will learn how to create autonomous web agents.
0:34 You will use MultiOn web agent in this lab.
0:38 Now we start by importing
0:41 our MultiOn client.
0:43 And we've prepared some functions in utils for you
0:45 to make the lab much easier to visualize.
0:49 So we allow you to visualizeSession, see a MultiOn demo.
0:52 Have a session manager, image utils, and also display step header.
0:58 Here, we start by initializing our MultiOn agent.
1:02 We load the MultiOn API key from the utils. Now we create MultiOn client.
1:08 Here you are creating a simplified client for a MultiOn API.
1:12 First, we initialize the MultiOn client with the API key.
1:16 Here we use the already
1:19 created instance for MultiOn class.
1:22 Then we create a new session for agent,
1:26 which starts at the URL that we provide,
1:29 and we also allow to include screenshots. Then, we also allow you to
1:33 close all open sessions,
1:36 and we allow you to also navigate to a particular URL.
1:40 Now we allow you to execute task in the current session.
1:44 Here,
1:45 you can give it on a specific task that you want the agent to follow.
1:50 And here the task executes in a single step,
1:53 but you can allow it to continuously run in a multiple steps.
1:58 Some of the instructions that were given to our agent is:
2:01 First, do not ask questions to the user.
2:05 It has all the necessary information in the page,
2:08 and it should try to
2:10 complete the task in the best of its abilities.
2:13 And finally to describe the task and also ask it to return a screenshot.
2:18 Now we initialize a MultiOn clients that we created.
2:23 Let's start with our first example.
2:25 We give it an instruction to get a list of all the courses.
2:29 Here, we start by creating our session.
2:33 You ask it to execute task, based on each step.
2:36 And we define each step as a particular action
2:40 that the agent can take. And it can be either click,
2:44 tag, submit, scroll, or triggering the information.
2:48 Right now we limit it to a certain number of max steps.
2:51 And that we define is ten.
2:55 You can visualize the session using the visualize session function.
3:00 And then execute the task
3:02 following the instruction that we have given it.
3:04 A new session has been created,
3:06 we continue to see how many steps have been executed.
3:11 Now, let's run it.
3:13 So, this might take some time, but we'll speed it up in post.
3:17 Now, we have our results.
3:20 So we can see the step zero.
3:23 It created a session.
3:24 Then the first step that it take it scrolls on the page,
3:28 to load more content.
3:30 Similarly, it keeps scrolling down until it will reach the end of the page
3:32 by following multiple steps.
3:35 Now you will see the final response.
3:39 We will use the visualize session function again.
3:42 And this is the final response that the agent gives us. Here,
3:46 it was able to find all the courses
3:49 that are a part of the DeepLearning.AI website and in full details.
3:53 You can see it does not follow a particular structure
3:56 because it is a more of a conversational assistant.
3:58 Where it follows and answers as more for a conversation.
4:01 But if we give it an instruction: give a structured output
4:05 like a JSON on markdown, it would've followed the results.
4:09 You can see, it's like the final screenshot
4:12 where it stopped and started giving us all the course listing.
4:17 Now you will create your own browser
4:19 UI.
4:20 Here,
4:20 you use your initialize my own client as part of our session manager
4:24 for which we already provided for implementation in the utils folder.
4:28 We will ask it to follow certain instructions like
4:31 finding the course on a subject and open it.
4:34 Summarize the course, get detailed course lessons.
4:38 And finally, we start with a more complex example and go to the DepLearning.AI
4:43 homepage subscribe to The Batch Newsletter, use a particular name, email,
4:47 choose any other required field.
4:50 And then give it a guidelines to make sure that it selects
4:54 the proper dropdown values.
4:55 And once it sees the subscribe button, it clicks it.
4:59 Now, let's describe our variables, like course,
5:03 subject, email and name.
5:05 Here we have given it subject as RAG.
5:09 We define the name as Div Garg.
5:11 And our email info@theagi.company
5:14 Now. We will create our own MultiOn browser UI
5:18 and also see what results and page is interacting on.
5:22 Now our MultiOn Browser
5:24 UI is fully loaded, and you can see it started on DeepLearning.AI courses.
5:29 We will start with the first example.
5:31 We are asking it to find the RAG course and open it.
5:35 You can see it entered
5:36 the RAG course in the search bar and waiting for the search bar to roll.
5:41 And here it is trying to scroll and find the course,
5:44 that it wants to open and examine its content.
5:48 Scroll more to see which course, it wants to open for RAG.
5:52 Ask the question on I've seen multiple courses on RAG,
5:56 but it wants us to give it a specific title
5:59 and as you can see in the browser UI,
6:01 you see a course on Multimodal RAG.
6:03 And I would ask you to open it on that.
6:08 As you can see,
6:09 is just able to and interact with the browser and open the course on Multimodal
6:13 RAG.
6:14 Now, as the next instruction will ask it to summarize it.
6:23 Here, it has given
6:24 us the summary of the course
6:27 and concludes the summary.
6:30 Here, you can ask it to give it a more detailed
6:34 core lessons.
6:38 Here, it improves the format and gives us
6:41 variety of different topics that the lesson covers.
6:45 Go to the course website and see in detail if we have the concepts
6:49 right.
6:49 So you can see this is the Multimodal RAG Chat with Video.
6:52 With Vasudev Lal.
6:54 Let us see the course outline.
6:58 And you can see it has eight lessons and six core examples.
7:00 And our agent was able to find
7:03 the course lessons outline
7:07 in a structured order.
7:11 This is the basic capabilities of autonomous AI agents.
7:12 Let's do something even more exciting.
7:15 We will ask the agent to go to the DeepLearning.AI homepage subscribe to The Batch Newsletter,
7:19 use the name Div Garg, info@theagi.company.
7:23 Choose other required fields like country
7:25 as United States and job title as software engineer.
7:29 And we can give it a guideline
7:30 to make sure that proper dropdown values are selected by typing and clicking on it.
7:34 And finally when it sees the subscribe button
7:36 and it clicks it.
7:41 Navigating to the DeepLearning.AI homepage.
7:43 This might be a small to see, but it is able to enter the Div Garg as a name
7:48 and also the email.
7:51 It might have reached
7:53 the maximum number of steps, but we will ask it to continue.
7:57 Now it selected country as United States.
8:03 So, it missed one particular step
8:06 and we will ask it to
8:08 and also select the job title.
8:17 So the agent seems to be asking
8:19 more questions just to make sure that it follows the correct guidelines.
8:22 And I can mention.
8:23 Yes, that is correct.
8:28 And you can see
8:30 now is entering the proper job title.
8:32 Trying to select it from the dropdown menu.
8:35 And it has finally selected it.
8:38 And, it clicked subscribe button to to subscribe to the newsletter.
8:42 So in this lesson
8:42 you learned how to create autonomous web agents how you can give it simple
8:47 instructions and if you follow them and you can also follow
8:51 a much more structured response without us manually describing it as code.
8:56 And then you also see how it can interact with the browser.
9:00 But you also see there are some challenges where
9:02 it might forget some steps
9:05 or it might need more clarification or guidelines to follow.
9:08 But agents are able to follow these steps
9:11 fully autonomously in a multiple-step manner.
9:13 fully autonomously in a multiple-step manner.
9:14 Now I encourage you to interact with this amazing browser UI,
9:18 and if you are not subscribed to the DeepLearning.AI Batch newsletter,
9:21 try it and see how it goes.

# p5

Transcript
0:00 In this lesson, we will explore Agent Q, a framework designed to teach
0:04 AI agents how to self-correct for various techniques used by AI researchers.
0:08 We'll dive into the key methods for improving agent performance,
0:11 We also provide a comprehensive overview of the Agent Q framework
0:15 and examine how it effectively addresses common AI agent challenges.
0:19 Let's dive in.
0:20 Remember, from lesson one, the existing frameworks have various limitations.
0:25 First, reliability and trust.
0:27 Second,
0:28 decision-making errors.
0:30 Third, plan divergence and looping.
0:32 There are four steps for agent execution: plan, reasoning,
0:36 where significant issues for agent execution come from the reasoning part.
0:41 And this is what we are going to address in this lesson.
0:44 Now, let's learn about Agent Q.
0:47 Which is a state-of-the-art AI algorithm
0:49 that addresses these issues and improve reasoning in web agents.
0:54 It combines the following methodologies to teach agents
0:56 to self correct.
0:56 The Monte Carlo Tree Search that we're going to explore
1:00 search spaces.
1:01 Self-critique mechanisms for continuous improvement.
1:04 Web agents receive real-time feedback.
1:06 And that Direct Preference Optimization (DPO), which is a reinforcement
1:11 learning algorithm that improves based on the current experience.
1:14 You will learn how these methods work together
1:17 to create a powerful framework for autonomous agent reasoning called Agent Q.
1:21 Our research team has published this findings in a white paper online,
1:24 that can be found on Arxiv. In the next lab you'll explore
1:26 some of these concepts.
1:27 Now, as step one, in understanding Agent Q,
1:32 we will learn about how Monte Carlo Tree Search
1:35 or MCTS works.
1:37 MCTS is search methodology for backtracking and exploring.
1:41 And it allows decisions may be planned several steps ahead.
1:46 In MCTS, we start at the root node
1:49 which is our current situation.
1:51 From here, the algorithm follows
1:53 what it thinks is the best path based on what it knows so far
1:57 using an exploitation strategy.
1:59 The algorithm continuous down the tree,
2:02 selecting what seems to be the most promising, until it reaches an end node
2:05 where no further exploration is needed.
2:06 At this point, the algorithm expands a tree, by creating a new possibility
2:10 and explores this unchartered territory.
2:12 Once we reach the end node, which is as far as we can go,
2:15 that algorithm predicts an expected Future Reward of continuing
2:18 on this path as a Monte Carlo estimate.
2:21 Think of this as playing out a quick point scenario
2:25 to see how good this choice might be.
2:27 After the future reward estimate, MCTS review of all the nodes
2:31 as we see on the way down. This call back propagation essentially telling the algorithm:
2:36 Hey, this path led to these results.
2:37 so update your knowledge accordingly
2:39 The magic of MTCS is that this entire process repeats many times.
2:43 But this situation the agent gets smarter, focus more on the promising parts
2:47 and less on dead ends.
2:48 Just like how you might get better at chess, by thinking 2 moves and their consequences.
2:55 In understand step two of Agent Q
2:57 self-critic mechanisms and for supervision.
3:01 This is an approach that uses an LLM critic
3:04 to give feedback and improve reasoning capacities of the actors.
3:08 When an user asks something like booking at a restauran reservation, the AI receives
3:12 a request along with any context or history from previous interactions.
3:16 Like part of the AI because it's every possible actions it can take.
3:20 It might set a second date and time first. Or selecting
3:23 a specific restaurant. Go to the OpenTable homepage, to start
3:26 from there.
3:27 This is where the critique comes in.
3:29 Think of it as the actor's
3:29 thoughtful advisor. The critic analyzes,
3:32 what the current run is showing, what the user actually asked for,
3:36 what information is most relevant right now.
3:39 Based on this analysis,
3:39 the critic can determine which actions make the most sense.
3:43 It provides detailed feedback on each option
3:45 in our restaurant booking example, instead of randomly trying actions.
3:48 The critic might suggest a better sequence.
3:51 First, go to the OpenTable homepage, then search for the restaurant name
3:55 and finally search the date and time. This ranking of actions
3:58 helps
3:59 the AI make smarter choices, similar to how you might mentally consider different approaches
4:03 before deciding on the best way to solve the problem.
4:06 For step three, for Agent Q,
4:08 we understand Reinforcement Learning from Human Feedback or RLHF.
4:13 Which is a method that allows AI assistance to learn
4:16 to make better decisions by incorporating human judgments
4:19 about what works best.
4:21 It's like training a helpful assistant
4:23 through ongoing feedback and guidance.
4:25 Now, we understand how all this comes together in a real-world example
4:29 of booking at a reservation at OpenTable.
4:32 When the agent runs through the Monte Carlo Tree research and a self-critic process,
4:36 it creates what we call 'preference data'.
4:38 These are comparisons between different outcomes from the same user query
4:41 and tell us which outcome is better.
4:43 In this case, the outcome one is preferred over outcome two.
4:46 This preference data is crucial
4:48 for improving the system and modeling what we call a reward model.
4:52 The reward model labels different actions, with rewards, giving a score of plus one,
4:56 the good behavior and minus one to the less useful ones.
5:00 This rewards help fine-tune the AI agent to make better decisions.
5:05 The system then generates sample outputs and fix them back
5:09 to the reward model for evaluation
5:11 This creates a continuous learning loop the AI tries something, gets feedback,
5:15 learns from it, and improves. The cycle is the essence of reinforcement
5:18 learning. Just like how we humans learn from experience and feedback
5:21 over time.
5:23 If you want to learn more about RLHF,
5:25 the Deep Learning course is available in the link below.
5:29 Now we understand step three of Agent Q Direct Preference Optimization or DPO,
5:33 a faster approach to reinforcement learning from human
5:37 feedback.
5:38 DPO streamlines how AI learns from preferences
5:41 by directly updating the model without creating a separate reward model.
5:45 It refines the AI's decision-making through direct feedback loops.
5:47 Essentially creating a shortcut in the learning process.
5:52 Instead of building an immediate reward model,
5:55 DPO takes preference data and directly fine-tunes the AI model itself.
5:59 This powerful approach complements our earlier
6:01 techniques, Monte Carlo Tree Search, explores possibilities.
6:06 Self-critique evaluates options.
6:09 You can read more about DPO in the research paper reference
6:11 at the bottom of the slide.
6:13 This approach significantly speeds up learning
6:16 while maintaining quality and improving response quality.
6:19 To repeat, the Agent Q framework comprises of three methods.
6:23 First, Monte Carlo Tree Search,
6:26 a method for structured exploration in search.
6:29 Second, self-critique mechanism and process supervision,
6:33 incorporating feedback for better decision making.
6:36 That's part of the search process.
6:38 These two methods combine to search,
6:40 identify failures and find out better options.
6:43 Direct Preference Optimization
6:46 is a reinforcement learning algorithm
6:48 that optimizes based on what the agent has seen before.
6:53 These three methodologies address the main challenges
6:55 of web agents identified before.
6:58 Here,
6:59 let's look at an example
7:00 on booking a reservation on OpenTable.
7:03 First, the agent incorrectly navigates to the wrong restaurant.
7:08 Then, Agent Q
7:09 identifies the failure and navigates back to the homepage.
7:13 It then corrects to go to the right restaurant,
7:17 then it accidentally selects the incorrect date
7:20 in which case it can be corrected by opening the date selector.
7:24 And then, going to the seat selection for the correct date.
7:27 And finally completing the reservation.
7:30 We tested Agent Q in real world scenarios
7:32 in booking on OpenTable. Every benchmark Agent Q against other methods
7:35 We find that GPT-4o is only able to reach a success
7:41 rate of 62.6% in terms of successful OpenTable reservations.
7:46 Agent Q, without including any AI feedback, which has an accuracy of 75.2%.
7:53 Similarly, Agent Q without including MCTS
7:56 reaches an accuracy of 81.7%.
8:01 Our final agent algorithm including all the three
8:02 methodologies here discussed so far,
8:07 is able to reach an amazing score of 95.4%
8:08 in these scenarios.
8:11 To recap,
8:13 we learned Agent Q and its main three elements. MTCS, Self-critique, and DPO.
8:15 In the next lesson,
8:18 you're going to explore MTCS and Agent Q in action. Alright! See you there.
# p6

0:10
/
9:53
Transcript
0:00 In this lesson, you will deep dive into Monte Carlo
0:03 Tree Search. A powerful algorithm for finding
0:06 optimal solutions in complex decision spaces.
0:10 We will then explore MCTS approach in AgentQ framework
0:14 to create autonomous browser agents capable of completing web tasks.
0:18 All right. Let's code.
0:20 In this lab, we're going to go over how can we can implement MCTS over the grid
0:25 world.
0:26 And in this example, you can see
0:28 we have our starting state, which is green at cell 7,6.
0:33 And an end state in the red color.
0:36 Which is at 2,4.
0:38 This marks are starting and end state
0:41 and ones with w are walls or obstacles.
0:47 And in this example
0:49 we want to traverse the grid to reach from start state to end state
0:53 Where you can traverse through the white nodes.
0:56 The agent can only travel north, south, east and west.
1:00 And now we'll go over the different examples of exploring
1:04 how weights can affect the speed of convergence to the optimal path.
1:08 The final Q-value and the exploration pattern across the grid.
1:13 Once we implement, MCTS, in the grid world example, we will take this to our AgentQ
1:18 example, Where we run MCTS with our browser agent.
1:23 Let's now code and have fun.
1:26 Let's start with the lab.
1:27 First, we start by importing all necessary packages.
1:32 Here we have already created one
1:33 grid world example,
1:36 where we have a MCTSGridWrapper
1:40 and the DFS algorithm to add labels to our grid.
1:43 Let's start with our MCTS example for Gridworld.
1:47 So we first start by creating our initial grid state.
1:51 And here the zero represents our possible path
1:54 that we can take to traverse the grid once the obstacles.
1:59 Two is a starting position and three is end state,
2:03 the final state that we want to reach.
2:05 Here we first start by constructing a grid, adding our colors,
2:10 defining our boundaries.
2:12 And we plot our graph.
2:15 Let's see our initial map.
2:17 So in the map, have our starting position which is green at cell
2:21 6,7 and the end which is red
2:25 at cell 2,4 and ours obstacles
2:28 which are marked by W classifying them as walls.
2:32 the goal is to reach from the starting position
2:35 to the end state by taking the shortest path possible, and then we will use
2:41 MCTS to find is the most optimal and the shortest route that we can get.
2:46 Now we are going to run MCTS on our grid example.
2:51 One thing we do is we compare how different weights
2:55 can affect our MCTS results and exploration.
2:58 We have low wight 1.0 and high rate of 3.0
3:03 and we have 5 explorations.
3:05 And overall we run around thousand iterations
3:09 for MCTS. This MCTSGridWrapper is in your utils files
3:13 where you can see the implementation.
3:15 Here, this allows us to trigger execution over grid,
3:18 to see and collect optimal routes.
3:21 Now, once our MCTS
3:22 has been triggered. Here you can use compare
3:26 exploration weights that's provided in mcts_animation.
3:30 That's part of how you do the follow.
3:32 This allows you to visualize our MCTS results.
3:36 Here, we can see
3:38 in the heatmap of
3:38 in the heatmap of
3:40 our n states for different explorations
3:43 and you can see different results, where this particular weight for 1.8
3:47 we see it starts, as an initial state, and reaches the end state
3:52 where you can see how much more darker colors,
3:55 whereas you see a much more brighter yellow.
3:58 This signifies, is falling apart, but this part is less optimal.
4:03 So the q value is lower.
4:04 So you find darker green.
4:06 Whereas here and state the q value is higher,
4:09 signifying that this is the best state to reach
4:13 and as you can see
4:14 in this animation, this is cell signifies the lowest Q-value that means the agent.
4:19 We are always avoiding this particular state.
4:22 And similarly for this roll out
4:24 we avoid going through this path
4:26 which are really not optimal for the agent to follow.
4:29 And similarly for the algorithm to avoid these weights, this signifies
4:33 that these are very less optimal path, but with the lowest
4:36 q value.
4:37 Now, for more exciting results let's see something cool.
4:45 Here you can see,
4:46 what's the best path our algorithm is following
4:49 and for the first example,
4:51 it's able to reach the most optimal state,
4:53 at the end, and it converges closer to
4:56 0.8 in value.
4:58 Initially, the model is exploring a much larger path,
5:01 but then it's able to converge into a shortest path possible.
5:05 Let's make it much more complex.
5:06 You can add much more obstacles.
5:08 You can make it even bigger.
5:10 So you can visualize how well entity performs with different weights
5:14 and different rollout, and how quickly it converges into the shortest path
5:19 However, please
5:20 leave a path for our agent to follow from start to the end.
5:24 Now,
5:25 once we finish with our MCTS,
5:27 Let's see MCTS
5:28 in a browser example, with our AgentQ.
5:32 So, in the AgentQ, we represent a world
5:34 model, in a browser state.
5:36 The states are represented by the DOM, URL and the objective.
5:39 The action executions are clicking, typing, navigation,
5:43 and it's able to do state transitions. In the browser MCTS,
5:47 that process follows, first initialization of the world model such configurations
5:53 and then we run our MCTS algorithm to generate q-reward values
5:57 for DPO, which is Direct Preference Optimization.
6:01 Now let's see this in our lab.
6:03 AgentQ clone is available for you, to use, to visualize a tree,
6:08 we can use this function plotTree and the dfs_browser_nodes
6:12 to visualize our proper tree representation for entity as tree.
6:17 So these are different states on what URLs
6:21 messages, actions and critic_responses that were captured,
6:25 during the MCTS process this are all nodes and these are all Q-values.
6:30 Then this represents our objectives, rewards mentioning
6:34 which states are terminal and the completed tasks.
6:37 And we run DFS to fully end and collect all this label data.
6:42 Now, let's visualize our tree.
6:46 So now we can see a pretty
6:48 complex tree representation for high density of trees.
6:52 Now let's zoom out to properly visualize
6:55 the whole tree and what paths it took.
6:59 As you can see it started at
7:01 how it could accomplish the initial state and it assigned it a Q-value
7:05 then, it went to the first node
7:09 then, it realizes it's not the most optimal path, it abandoned it
7:12 and the second node, same. The third node is, a more doable path that is selected.
7:17 And you can see because of the Q-value and it's much higher
7:21 than the rest of the Q-values, And from what we can see, node 4
7:25 has the highest Q-value and is also the end state.
7:29 So this is where it stopped,
7:31 after evaluating all the possible rollouts.
7:34 On starting this node
7:35 it further created 3 more paths, that it can follow
7:39 And started with node 4, node 5 and node 6
7:43 Then it further explores all the paths following those nodes.
7:47 And then, it back propagate back to node 4 and assigns
7:51 it the highest Q-value and determines is that terminal state,
7:55 where it reaches the goal and also the shortest route possible to achieve our goal.
8:01 From this possible path,
8:03 it continued to node 4 and it didn't explore it further
8:06 because this is a terminal state, but it's already on the course page
8:10 which is Building and Evaluating Advanced RAG,
8:12 That was one of the possible objectives.
8:15 Then, in the other nodes, you can see,
8:17 it instead navigated to community.DeepLearning.AI
8:21 And further path, it navigated to short courses
8:25 in the community and even more exciting,
8:28 this page is about RAG
8:30 But it's not
8:31 a course, it's more of a community discussion on the course.
8:35 And you can see
8:36 once it sees that it's more of a discussion, it abandons this path.
8:41 And same with our other
8:43 possible path, which is again on the community page.
8:46 Further, it explores down, finds the course or discussion
8:50 on RAG, in this case building multimodal RAGs search.
8:54 And same with trying to find knowledge graph for RAG.
8:58 And again
9:00 here, it is decided it needs to navigate back and back propagate
9:04 to its initial state because it is the wrong page.
9:08 And same you can see here once it's continue down this line
9:12 it says this is a multimodal search
9:14 but not the proper state that it needs to be, same.
9:18 It sees it is a discussion.
9:20 And here it even sees an error that allows it to think
9:23 it can continue further and it is a terminal state.
9:26 Following this route, the agent sees that node 4
9:29 is the shortest route and the best possible state
9:32 to see the course listing for our RAG course.
9:36 In this lesson, you learned about how to implement MCTS,
9:39 And also see how MCTS can behave in a browser environment
9:43 and find the shortest and most optimal path possible,
9:46 and see how it can actually improve our results
9:50 compared to previous results.

# p7

Transcript
0:00 In this lesson, we will discuss the key factors driving AI agents
0:04 and their evolution in the field.
0:06 You will learn about the current limitations and will explore possible
0:09 future directions for where AI agent technology is headed,
0:13 and how these developments might shape the AI landscape.
0:17 Let's learn about the key factors driving AI agents proliferation.
0:21 The first is technological advancements.
0:24 Specialized hardware improvements such as GPUs and storage
0:28 computing, larger models and more complex agents to run Python drivers.
0:32 Second, computational and algorithm innovation provides a foundation
0:37 for agents capable of planning and acting autonomously.
0:40 With a variety of very different
0:41 new advancements in LLMs.
0:43 Another factor is data availability.
0:45 Right now, we have large diverse data sets that enable
0:48 agents to learn complex patterns for decision-making through
0:52 open data initiatives and large scale platforms.
0:56 Web agents have these current challenges.
0:59 At first,
1:00 from the lack of uniformity.
1:02 There's, like, diverse frameworks
1:04 and implementations, but there's no ways to make them work together.
1:08 And there's a fragmented ecosystem. Where again
1:10 there's a lot of things going on in that critical system.
1:14 But interoperability is really hard. What is needed is some sort of standardization
1:18 for interoperability, scalability and collaboration.
1:23 As AI agents become increasingly adept at navigating the web, it's crucial to assess
1:27 their performance in environments, that mirror real-world conditions.
1:31 Traditional evaluation methods often fall short in replicating
1:33 the dynamic and unpredictable nature of actual interactions.
1:37 You're seeing too many websites, and need deterministic environments
1:41 to ensure consistent conditions for each evaluations,
1:43 eliminating variability that could affect performance assessments.
1:47 Limited insight into user behavior and agent performance in web navigation.
1:51 Can be corrected by realistic interactions that emulate real-world challenges.
1:52 Can be corrected by realistic interactions that emulate real-world challenges.
1:55 Including loading errors
1:57 high latency, and disruptive pop-ups,
1:59 to test agents' resilience and adaptability.
2:02 Finally, eval methods fall short in unpredictable web interactions
2:05 and need comprehensive evaluation metrics.
2:08 But just as both the final outcomes of the transactions
2:11 and the ability to navigate complex web scenarios effectively.
2:16 To address these
2:16 challenges, we are building a new benchmark:
2:20 Realistic Evaluation for Agents Leaderboard.
2:23 REAL.
2:24 The REAL benchmark addresses previous challenges
2:27 by providing a deterministic yet realistic playground
2:31 that models real-world browser experiences.
2:33 This setup allows for consistent evaluation of AI agents abilities
2:37 to perform tasks such as information retrieval and transaction operations,
2:41 and establishes a baseline for browser agent models.
2:44 This collective approach aims to establish robust baselines and leaderboards
2:49 for state-of-the-art agents, benefiting both the public and academic sectors.
2:54 I encourage you to engage with the project by providing feedback.
2:57 Sharing insights and contributing to the refinement of evaluation scenarios.
3:01 By collaborating, we can enhance the evaluation frameworks for AI agents,
3:05 ensuring that they are well equipped to handle the complexities of the real world
3:08 web navigation tasks.
3:10 So far we've discussed a single AI agent.
3:13 Now, as an user, you can have a multi-system
3:18 for the manager agent that oversees multiple specialized worker agents.
3:22 However, with everyone creating their own agents.
3:25 This can lead to a chaotic ecosystem.
3:28 Let's explore the challenges and considerations for Multi-Agent Systems.
3:32 First one is the coordination complexity
3:35 that is ensuring coherent behavior among autonomous agents,
3:38 which can be challenging without a centralized oversight.
3:41 Second, communication overhead.
3:43 Decent resistance
3:44 may require more complex communication protocols to facilitate effective collaboration.
3:48 And third, security concerns. Maintaining system integrity and preventing malicious behavior,
3:54 and an open, decentralized environment necessitates robust security measures.
3:58 What is needed is modularity,
4:01 specialization, and control.
4:04 Here are some future research directions that you see. First,
4:07 exploring hybrid architectures that combine centralized and decentralized
4:10 elements to leverage the advantages on both approaches.
4:14 Advanced communication protocols that are more effective and allow
4:18 for better coordination.
4:19 And third,
4:20 investigating the application of decentralized multi-agent systems
4:24 in different domains such as collaborative robotics, sensing and simulations.
4:28 Here are some Multi-Agent Architectures that need further explorations.
4:32 That is the senior supervisor.
4:34 Using LLM for tool-calling. Having a network-based architecture.
4:37 Having custom
4:39 multi-agent workflows. And having hierarchy.
4:43 Now, we take a look at the future trends and actions.
4:47 Web agents advancing capabilities for better natural language
4:50 understanding and tool use.
4:51 The deep learning will enable for students to perform complex sequence of actions online.
4:55 Such as appointments, researching and summarizing information
4:59 coordinating across websites all on user's behalf.
5:03 Multi-agent systems cooperate in a shared environment
5:06 and learn sophisticated strategies by interacting with each other.
5:10 Finally,
5:11 Advances in distributed cloud computing
5:13 will support the other advancements,
5:16 and lead to building more scalable systems that can be deployed in the real world.
5:21 In this
5:21 lesson we explored some of the challenges in the current agentic system.
5:25 And the future trends on how this can be
5:28 standardized and improved for deployment.

# p8

Transcript
0:00 In this course, you learned about web agents from the ground up.
0:04 You started with the fundamentals of what they are and how they work
0:08 then progressed through building simple and autonomous web agents.
0:11 You explored advanced frameworks like AgentQ for self-correction,
0:14 and finally examined the current limitations,
0:16 and future trajectory of AI agent technology.
0:19 We are looking forward to seeing what you have built on your own.










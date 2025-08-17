## Additional Resources

- [Building Agents with Model Context Protocol](https://www.youtube.com/watch?v=kQmXtrmQ5Zg&t=1s&ab_channel=AIEngineer) - Full Workshop with Mahesh Murag of Anthropic
- [Mahesh Workshop Agent Example](https://github.com/maheshmurag/workshop-mcp-agent-example) (this example shows the use of MCP agent: an example of a host or LLM-based application that is MCP compatible).
- [Claude Desktop Setup](https://modelcontextprotocol.io/quickstart/user) (you may need to download [Node.js](https://nodejs.org/en), and also [uv](https://github.com/astral-sh/uv?tab=readme-ov-file#installation))
- [Testing your server with Claude Desktop](https://modelcontextprotocol.io/quickstart/server#testing-your-server-with-claude-for-desktop) - If you’re a Windows user and using uv, you may need to put the full path to the uv executable in the command field. 
- [MCP core architectures](https://modelcontextprotocol.io/docs/concepts/architecture); [MCP Python SDK](https://github.com/modelcontextprotocol/python-sdk).
- If you code with Typescript, check this [MCP course](https://www.aihero.dev/mcp-prerequisites).
- [MCP server with Docker](https://github.com/daveebbelaar/ai-cookbook/tree/main/mcp/crash-course/6-run-with-docker) 
  
   In lesson 9, you can setup the remote server using `uv` as explained in the course. Then you can create this DockerFile:
    ```
    FROM python:3.11-slim
    WORKDIR /app
    RUN pip install uv
    COPY pyproject.toml uv.lock ./
    RUN uv pip install --system .
    COPY research_server.py .
    EXPOSE 8001
    CMD ["uv", "run", "research_server.py"]
    ```
    And then create the image using  this command: `docker build -t my-server .`

    Then run the container using: `docker run -p 8001:8001 my-server`


## 💻 &nbsp; Accessing Utils File and Helper Functions
In each notebook on the top menu:

**1:** &nbsp; Click on <em>"File"</em>

**2:** &nbsp; Then, click on <em>"Open"</em>

You will be able to see all the notebook files for the lesson, including any helper functions used in the notebook on the left sidebar. See the following image for the steps above.

<img width="450px" src="images/upload-file2.png" style="border-width:3px; border-color:#f5ecda; border-style:solid; border-radius:6px">

<hr style="height: 3px; background-color:#f0f0f0; border: none;">


## 💻 &nbsp; Downloading Notebooks
In each notebook on the top menu:

**1:** &nbsp; Click on <em>"File"</em>

**2:** &nbsp; Then, click on <em>"Download as"</em>

**3:** &nbsp; Then, click on <em>"Notebook (.ipynb)"</em>

<img width="450px" src="images/how-to-download-notebooks.png" style="border-width:3px; border-color:#f5ecda; border-style:solid; border-radius:6px">

<hr style="height: 3px; background-color:#f0f0f0; border: none;">


## 💻 &nbsp; Uploading Your Files
After following the steps shown in the previous section ("File" => "Open"), then click on <em>"Upload"</em> button to upload your files.

<img width="700px" src="images/upload-file-3.png" style="border-width:3px; border-color:#f5ecda; border-style:solid; border-radius:6px"></img>

<hr style="height: 3px; background-color:#f0f0f0; border: none;">


## 📗 &nbsp; See Your Progress
Once you enroll in this course—or any other short course on the DeepLearning.AI platform—and open it, you can click on 'My Learning' at the top right corner of the desktop view. There, you will be able to see all the short courses you have enrolled in and your progress in each one.

<img width="700px" src="images/progress-upper.png" style="border-width:3px; border-color:#f5ecda; border-style:solid; border-radius:6px"></img>

Additionally, your progress in each short course is displayed at the bottom-left corner of the learning page for each course (desktop view).

<img width="700px" src="images/progress-bottom.png" style="border-width:3px; border-color:#f5ecda; border-style:solid; border-radius:6px"></img>

<hr style="height: 3px; background-color:#f0f0f0; border: none;">


## 📱 &nbsp; Features to Use

**🎞 &nbsp; Adjust Video Speed:** Click on the gear icon (⚙) on the video and then from the <em>Speed</em> option, choose your desired video speed.

**🗣️ &nbsp; Captions (English and Spanish):** Click on the gear icon (⚙) on the video and then from the <em>Captions</em> option, choose to see the captions either in English or Spanish.

**🔅 &nbsp; Video Quality:** If you do not have access to high-speed internet, click on the gear icon (⚙) on the video and then from <em>Quality</em>, choose the quality that works the best for your Internet speed.

<img width="350px" src="images/options.png" style="border-width:3px; border-color:#f5ecda; border-style:solid; border-radius:6px"></img>

**🖥 &nbsp; Picture in Picture (PiP):** This feature allows you to continue watching the video when you switch to another browser tab or window. Click on the small rectangle shape on the video to go to <em>PiP</em> mode.

**✔ &nbsp; Hide and Unhide Lesson Navigation Menu:** If you do not have a large screen, you may click on the small hamburger icon beside the title of the course to hide the left-side navigation menu. You can then unhide it by clicking on the same icon again.

<hr style="height: 3px; background-color:#f0f0f0; border: none;">


## 🧑‍🎓 &nbsp; Efficient Learning Tips
The following tips can help you have an efficient learning experience with this short course and other courses.

**🧑‍🏫 &nbsp; Create a Dedicated Study Space:** Establish a quiet, organized workspace free from distractions. A dedicated learning environment can significantly improve concentration and overall learning efficiency.

**📅 &nbsp; Develop a Consistent Learning Schedule:**
Consistency is key to learning. Set out specific times in your day for study and make it a routine. Consistent study times help build a habit and improve information retention.

**Tip:** Set a recurring event and reminder in your calendar, with clear action items, to get regular notifications about your study plans and goals.

**☕ &nbsp; Take Regular Breaks:**
Include short breaks in your study sessions. The Pomodoro Technique, which involves studying for 25 minutes followed by a 5-minute break, can be particularly effective.

**💬 &nbsp; Engage with the Community:**
Participate in forums, discussions, and group activities. Engaging with peers can provide additional insights, create a sense of community, and make learning more enjoyable.

**✍ &nbsp; Practice Active Learning:**
Don't just read or run notebooks or watch the material. Engage actively by taking notes, summarizing what you learn, teaching the concept to someone else, or applying the knowledge in your practical projects.

<hr style="height: 3px; background-color:#f0f0f0; border: none;">


## 📚 &nbsp; Enroll in Other Short Courses
Keep learning by enrolling in other short courses. We add new short courses regularly. Visit DeepLearning.AI Short Courses page to see our latest courses and begin learning new topics. 👇

<b><a href="https://www.deeplearning.ai/courses/?utm_source=dlai-learn-platform&utm_medium=referral-sc&utm_campaign=appendix-tips-help">👉👉 🔗 DeepLearning.AI – All Short Courses [+]</a></b>

<hr style="height: 3px; background-color:#f0f0f0; border: none;">


## 🙂 &nbsp; Let Us Know What You Think
Your feedback helps us know what you liked and didn't like about the course. We read all your feedback and use them to improve this course and future courses. Please submit your feedback by clicking on <em>"Course Feedback"</em> option at the bottom of the lessons list menu (desktop view).

<img width="700px" src="images/feedback.png" style="border-width:3px; border-color:#f5ecda; border-style:solid; border-radius:6px"></img>

Also, you are more than welcome to join our community <a href="https://community.deeplearning.ai/">👉👉 🔗 DeepLearning.AI Forum</a>

<hr style="height: 3px; background-color:#f0f0f0; border: none;">


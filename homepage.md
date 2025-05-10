# More Human Than Human: A Multi-Modal AI Framework for Natural Language Cobot Control

**Advancing Natural Human-Robot Collaboration with Multi-Modal AI in Unstructured Environments**

[![More Human Than Human Framework - Architecture](_assets/architecture_diagram.png)](docs/02_System_Architecture.md)
*(Click image to explore the System Architecture)*

The "More Human Than Human" framework represents a significant step towards enabling collaborative robots (cobots) to understand natural language, perceive complex environments, and execute tasks with human-like adaptability. Developed within the high-fidelity NVIDIA Isaac Sim environment, this project integrates cutting-edge Large Language Models (LLMs), Vision-Language Models (VLMs), and Deep Reinforcement Learning (DRL) to bridge the gap between human intention and robotic action.

---

## 🚀 See the Framework in Action!

Watch a demonstration of the "More Human Than Human" framework processing a natural language command and executing a task in a simulated unstructured environment.

[![Framework Demo Video Thumbnail](_assets/framework_demo_thumbnail.png)](_assets/framework_demo_video.mp4)


---

## ✨ Key Features & Innovations

* 💬 **Intuitive Natural Language Control:** Interact with cobots using everyday spoken or typed commands. The framework intelligently interprets intent and can engage in clarification dialogues.
* 👁️ **Advanced Scene Understanding:** Leverages VLMs for rich semantic understanding of the environment, complementing geometric perception to ground language in visual context.
* 🧠 **AI-Powered Task Planning:** Employs state-of-the-art foundation models (e.g., Gemini, GPT-4) to decompose high-level goals into executable robotic actions.
* 😊 **Sentiment-Based Behaviour Adaptation:** A novel HRI feature allowing the robot to modulate its execution style (e.g., speed, precision) based on the sentiment or context of the command (e.g., "handle carefully" vs. "do it quickly").
* 🦾 **Dexterous Skill Acquisition (DRL):** Incorporates a modular skill library architecture, with successfully trained DRL policies for complex, contact-rich manipulation tasks like bolt pickup.
* 🔗 **Hybrid-Hierarchical Architecture:** A unique design combining the reasoning power of large AI models with the flexibility of a modular skill base and the precision of dedicated motion planners.
* 📊 **Foundation Model Benchmarking:** The framework is designed to systematically evaluate and compare the performance of different foundation models on embodied robotic tasks.
* 🌐 **High-Fidelity Simulation:** Developed and validated in NVIDIA Isaac Sim, enabling realistic testing and paving the way for sim-to-real transfer.

---

## 📚 Explore the Framework

Dive deeper into the technology, design, and performance of the "More Human Than Human" framework:

* **[Introduction: The Vision Behind the Framework](docs/00_Introduction.md)**
    * *Why we need more intuitive robot control and the project's mission.*
* **[Core Technologies: The Building Blocks](docs/01_Core_Technologies.md)**
    * *Learn about the Multi-Modal AI, DRL, and Simulation technologies powering the framework.*
* **[System Architecture: How It All Works Together](docs/02_System_Architecture.md)**
    * *A detailed look at the framework's design, data flow, and components.*
* **[Key Features In-Depth](docs/03_Key_Features_Hub.md)**
    * *Explore specific innovations like Sentiment Adaptation and DRL for Dexterity.*
* **[Demonstrations & Use Cases](docs/04_Demonstrations.md)**
    * *See more examples and potential applications.*
* **[Performance & Evaluation: Putting It to the Test](docs/05_Performance_Evaluation.md)**
    * *Review the systematic testing methodology, results, and insights gained.*
* **[Technical Insights & Development Journey](docs/06_Technical_Insights.md)**
    * *Learnings from developing with advanced AI and simulation tools.*
* **[Future Roadmap: What's Next?](docs/07_Future_Roadmap.md)**
    * *Our vision for future enhancements and research directions.*

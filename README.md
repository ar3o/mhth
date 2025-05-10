# More Human Than Human: A Multi-Modal AI Framework for Natural Language Cobot Control in Unstructured Environments

![Project Banner](images/banner.png)

## 📄 Project Overview

This project presents **"More Human Than Human"**, a multi-modal AI framework designed to enable natural language control for collaborative robots (cobots) operating in unstructured, dynamic environments. Developed within the high-fidelity NVIDIA Isaac Sim simulation platform, the framework bridges the gap between intuitive human commands and complex robotic actions by integrating cutting-edge AI technologies.

Inspired by biological systems, our framework acts as a "brain" for the robot, combining high-level reasoning from **Large Language Models (LLMs)** and semantic scene understanding from **Vision-Language Models (VLMs)** with low-level dexterous control via a **modular skill library** incorporating motion planners and Deep Reinforcement Learning (DRL) policies.

The goal is to move beyond rigid, pre-programmed industrial robots and create systems that can understand nuanced instructions like "carefully pour me some tea" or "unscrew the bolts on this object," interpret their surroundings visually, make intelligent decisions, and execute tasks safely and effectively without requiring specialized programming expertise.

## ✨ Key Features & Contributions

*   **Novel Hybrid-Hierarchical Architecture:** A unique pipeline combining the high-level reasoning power of foundation models (LLMs/VLMs) with a modular skill base for robust, grounded execution.
*   **Foundation Model Benchmarking:** Provides a framework and methodology for evaluating and comparing the embodied performance of different multi-modal models (Gemini, Claude, GPT) on robotic planning and reasoning tasks within a realistic simulated environment.
*   **Sentiment-Based Behaviour Adaptation:** Explores a novel Human-Robot Interaction (HRI) concept where the framework interprets the user's sentiment (e.g., "quickly," "carefully") to dynamically adjust robot motion parameters (speed, precision).
*   **Modular Skill Base with DRL Integration:** Supports an extensible library of robot capabilities, including standard motion planning routines (CuRobo, RMPFlow) and the integration of complex, learned manipulation skills acquired via Deep Reinforcement Learning (DRL) for contact-rich tasks (demonstrated with a bolt pickup policy).
*   **Digital Twin for Action Pre-Testing & Validation:** Leverages the high-fidelity physics and rendering of NVIDIA Isaac Sim as a "digital twin" to potentially validate AI-generated plans before real-world execution, including AI-driven analysis of simulated outcomes.
*   **Context-Aware Planning:** The AI reasoning engine considers the robot's state, object properties, environmental context, and interaction history to generate more intelligent and adaptive action plans.
*   **VLM Concepts for Perception:** While primarily using simulated ground truth for precision, the framework includes experimental integration of VLM capabilities for tasks like 3D bounding box detection and language-grounded point identification directly from images.

## 🏗️ Architecture Overview

The framework operates as a pipeline, processing natural language commands through several stages:

1.  **Input Reception & Understanding:** Receives command (text/voice), gathers context (visual data, scene state, robot state, history), and performs initial ambiguity checks using an efficient VLM.
2.  **Perception & Scene Understanding:** Processes visual and scene data. Utilizes simulated ground truth (primary) or experimental VLM/CV methods to identify objects, determine 6D poses, and understand semantic relationships.
3.  **AI Reasoning & Task Planning:** The core LLM/VLM engine integrates all information (command, perception outputs, context). Using sophisticated prompt engineering, it interprets intent, decomposes the task, selects skills, calculates parameters, and generates a structured Action Plan.
4.  **Action Execution & Control:** Dispatches the planned actions to the Modular Skill Base. The skill base invokes appropriate low-level controllers (motion planners like CuRobo/RMPFlow, DRL policies) to execute movements and manipulations in the simulation.
5.  **Monitoring & Adaptation:** Continuously monitors execution status. Detects errors (simulation errors, skill failures, VLM analysis). If errors occur, compiles new context and feeds back to the AI reasoning engine for potential replanning and error recovery.

⚙️ Technical Implementation Details
Simulation Platform: NVIDIA Isaac Sim (utilizing PhysX for physics, RTX for rendering).
AI Models: Evaluated using various state-of-the-art models including Google Gemini (2.5 Pro, Flash 2.5, Flash 2.0), Anthropic Claude 3.7 Sonnet, and OpenAI GPT-4.1. The framework is designed to be model-agnostic, relying on API calls.
Motion Planning: Integration with CuRobo and RMPFlow libraries for collision-free trajectory generation.
DRL: Trained a bolt pickup policy using Proximal Policy Optimization (PPO) via the RSL-RL library within Isaac Lab (NVIDIA's DRL training environment for Isaac Sim).
Speech-to-Text: Utilizes the Deepgram API for processing voice commands.
Perception: Primarily uses simulated ground truth; experimental features integrate VLM analysis directly from rendered RGB images.
Robot: Franka Emika Panda robot with a parallel-jaw gripper simulated in Isaac Sim.
Interface: Integrated within the Isaac Sim environment for direct interaction and visualization. Supports remote input via a socket server.
🧪 Evaluation & Results
The framework was systematically evaluated in a Basic Shapes Manipulation scenario designed to mimic unstructured environment challenges (clutter, randomization, varied objects). Testing focused on Plan Generation and Execution Success.
Evaluation Scenario: Basic Shapes Manipulation
A tabletop with 12 geometric shapes (cubes, cylinders, spheres, cuboids of varying sizes/colors) placed with randomized orientations and some clutter. The robot must interact with these objects based on diverse natural language commands.
![alt text](images/scenario_screenshot.png)

Plan Generation Evaluation:
Different foundation models were tested on their ability to generate valid action plans for 10 commands (5 short-horizon, 5 long-horizon), evaluated on Task Comprehension, Action Sequence Validity, and Object & Spatial Awareness (scoring 0-2 per metric).
Top Performers:
Google Gemini 2.5 Pro: 55/60
Anthropic Claude 3.7 Sonnet: 53/60
OpenAI GPT-4.1: 53/60
Key Findings:
Leading models demonstrated strong command interpretation and logical sequencing.
Gemini 2.5 Pro showed superior spatial reasoning, particularly with orientation and implicit hiding tasks, suggesting benefit from 3D data training.
GPT-4.1 exhibited notable creativity and personality in handling abstract commands ("Construct something beautiful").
A clear trade-off exists between model speed (latency) and plan quality, highlighting a challenge for real-time control.
Prompt engineering was shown to improve plan quality, even with less capable models.
Execution Evaluation (using GPT-4.1 generated plans):
Successfully generated plans from GPT-4.1 were executed in the Isaac Sim environment, evaluated on Command Completion, Plan Adherence, and Error Recovery.
Overall Execution Success Rate: 60%
Primary Failure Cause: Execution failures were primarily linked to collisions within the cluttered environment. While the AI planned correctly, the motion planner's inability to dynamically treat non-target objects as collision obstacles (a known limitation addressed in future work) caused issues during manipulation in close proximity. Error recovery mechanisms were also found to be ineffective in these cases.
🚧 Challenges & Limitations
Developing this framework involved significant hurdles:
Isaac Sim Complexity & Stability: The platform has a steep learning curve, high GPU VRAM requirements, and exhibited stability issues (e.g., memory leaks), significantly impacting development speed and limiting the scope of evaluation scenarios.
RL Policy Integration: Successfully training DRL policies was achieved, but integrating these learned skills to be robustly callable and utilized by the high-level AI planner proved more complex than anticipated, a key unrealized goal.
Execution Robustness: Reliably executing complex manipulations in clutter remains challenging due to limitations in the current motion planning integration (lack of dynamic obstacle avoidance) and nascent error recovery capabilities.
Simulated Perception vs. Real: While using ground truth simplified development, moving to real-world applications requires integrating and evaluating actual sensor data and state-of-the-art real-world perception models.
Benchmark Subjectivity: The evaluation scoring relied on human judgment, introducing potential bias.
🌱 Future Work
Based on the project's findings and limitations, key directions for future development include:
Enhancing Execution: Implementing comprehensive real-time collision avoidance by integrating environmental objects as dynamic obstacles for the motion planner. Improving error detection and developing more sophisticated, AI-driven error recovery strategies.
Integrating Real Perception: Replacing simulated perception with actual sensor data processing pipelines incorporating state-of-the-art models like SAM 2 or FoundationPose.
Full RL Integration: Developing robust interfaces and mechanisms for the high-level AI to seamlessly select and execute trained DRL policies for complex, dexterous tasks.
Expanding Skill Library: Adding more diverse fundamental robot skills and specialized learned policies.
More Complex Scenarios: Designing and evaluating the framework on a wider range of challenging, cluttered, and dynamic environments.
Generalization Testing: Evaluating the framework's ability to handle truly novel objects and situations not encountered during development.
Exploring End-to-End Potential: As foundation models advance, investigating their potential to take on more direct control roles, potentially simplifying the pipeline.
▶️ Getting Started
(This section provides general guidance. Specific installation and setup steps depend on the project's code structure and dependencies)

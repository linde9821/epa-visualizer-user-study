This README is designed to guide you through the setup and provide the necessary background to participate in the user
study for the **EPA Visualizer**.
Please read it carefully, and thank you for your time and expert insights :)

# 1. Getting Started

## 1.1 Run the application

The application is a JVM-based desktop tool developed with Kotlin and Compose Desktop. The setup *should* be easy.

**Need Help?** If you encounter setup issues, please contact
me [Moritz Lindner @ moritz.lindner@student.hu-berlin.de](mailto:moritz.lindner@student.hu-berlin.de).

<details>
<summary><b>Option A: Pre-compiled Version (Recommended)</b></summary>

1. Download the appropriate ZIP file for your operating system and processor architecture:

|         | linux                                                                                                                                                     | macOs                                                                                                                                                         | Windows                                                                                                                                                     |
|---------|-----------------------------------------------------------------------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **arm** | <a href="https://github.com/linde9821/epa-visualizer-user-study/raw/refs/heads/main/distributions/linux-arm64.zip?download=" target="_blank">download</a> | <a href="https://github.com/linde9821/epa-visualizer-user-study/raw/refs/heads/main/distributions/macos-arm64.zip?download=" target="_blank">download</a>     | <a href="https://github.com/linde9821/epa-visualizer-user-study/raw/refs/heads/main/distributions/windows-arm64.zip?download=" target="_blank">download</a> |
| **x64** | <a href="https://github.com/linde9821/epa-visualizer-user-study/raw/refs/heads/main/distributions/linux-x64.zip?download=" target="_blank">download</a>   | <a href="https://github.com/linde9821/epa-visualizer-user-study/raw/refs/heads/main/distributions/macos-intel-x64.zip?download=" target="_blank">download</a> | <a href="https://github.com/linde9821/epa-visualizer-user-study/raw/refs/heads/main/distributions/windows-x64.zip?download=" target="_blank">download</a>   |

2. Extract the contents to a local directory.
3. Execution: Follow the platform-specific instructions below to launch the application:

### Linux:

* Navigate to the `EPA Visualizer/bin` directory.
* Run the EPA Visualizer executable from your terminal or by double-clicking it.
* You may need to ensure it has execution permissions first: `chmod +x bin/"EPA Visualizer"`.

> _Note:_
> Graphics & OpenGL: The application uses hardware acceleration via Skia.
> Please ensure your graphics drivers are up to date and support OpenGL.
> Unlike Windows and macOS, where standardized graphics drivers are typically bundled with the OS or vendor updates,
> Linux environments vary significantly in how they handle hardware acceleration.
> Ensuring the correct OpenGL libraries (such as libgl1) are installed is often a manual requirement on some
> distributions to ensure the UI renders correctly.

### macOS:

* Open the app folder and locate `EPA Visualizer.app` and run it.
* If you get a warning stating the "App is damaged and can't be opened" please follow the steps described in the note
  below.

> _Note:_
> Because the application, it is not notarized by Apple you may receive an error stating the "App is damaged and can't
> be opened,".
> run the following command in your Terminal to bypass the security flag:
> `sudo xattr -cr /path/to/EPA\ Visualizer.app`
> Once executed, you can open the app normally.
> _If this is not possible please use Option B described below._

### Windows:

* Navigate into the extracted EPA Visualizer folder.
* Double-click `EPA Visualizer.exe` to start.

</details>

<details>
<summary><b>Option B: Building from Source</b></summary>

If you prefer to build the application yourself, you will need a JDK installed:

1. **Clone** the <a href="https://github.com/linde9821/epa-visualizer" target="_blank">epa-visualizer repository</a>:
   `git clone git@github.com:linde9821/epa-visualizer.git`
2. **Set up Git LFS**: This repository uses Git Large File Storage. Ensure you have Git LFS installed and run the
   following in the project root to pull the actual data files: `git lfs install && git lfs pull`
2. **Navigate** to the root folder.
3. **Execute** the command: `./gradlew run`

> _Note: Initial building may take a few minutes as dependencies are downloaded._
</details>

## 1.2 Load the event log and begin the study

1. **Extract the Data**: Download and
   unzip <a href="https://github.com/linde9821/epa-visualizer-user-study/raw/refs/heads/main/User%20Study%20Project.zip?download=" target="_blank">
   User Study Project.zip</a>.
2. **Launch the App**: Open the EPA Visualizer.
3. **Open Project**: Click the **Open Project** button on the welcome screen.
4. **Select Directory**: In the file browser, select the **directory** of the extracted ZIP file.

**Need Help?** If you encounter setup issues, please contact
me [Moritz Lindner @ moritz.lindner@student.hu-berlin.de](mailto:moritz.lindner@student.hu-berlin.de).

After that, the application will generate the EPA and render the visualization.
Please read "2. Background: Extended Prefix Automata (EPA)" to get an explanation of what the application is actually
showing.
You can then begin the study.

# 2. Background: Extended Prefix Automata (EPA)

The Extended Prefix Automaton (EPA) is a specialized, state-based representation that is used to analyze process execution variants in large, complex event logs:

- The Problem: Traditional visualizations often focus on individual process variants, failing to depict the entire landscape of variants.
- The EPA encodes these variants as paths in a graph. This ensures that every trace (process execution) can be reproduced exactly without losing information through abstraction. Our application visualizes this EPA in order to show the existing variant.
- The application aims to minimize visual clutter while enabling in-depth analysis of specific process behaviors, such as performance bottlenecks related to variants. With its various interactive layouts, filters, and animations, the application allows you to explore the underlying complexity of your business processes.

Core Concepts:

- States & Transitions:
    - States (Nodes): Each node represents an activity that is reached at a specific point in the process.
    - Root State: All process paths originate from a single "root" entry state.
    - Transitions (Edges): Lines between states represent the flow of activities in a variant.
- Partitions & Branching:
    - Shared Prefixes: Different process variants often have the same initial activities. These activities are
      visualized as a single joint path.
    - A "branch" is created in the automaton when process variants diverge.
    - Partitions: Each branch, or unique sequence of activities, is assigned to a specific partition. The total number of partitions in the EPA is equal to the number of unique process variants observed in the data.

We have [an explanatory video](www.youtube.com) about how to use the core feature available for you.
There is also a [slide deck](Slide%20Deck.pdf) explaining all features in a written form.
The questions in the user study are designed so that you won't get lost.

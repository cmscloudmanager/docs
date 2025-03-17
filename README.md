# CMS Cloud Manager blog / documentation

<img src="https://raw.githubusercontent.com/cmscloudmanager/docs/refs/heads/main/image/cmscloudmanager.png" alt="CMS Cloud Manager" width="128" align="right">

The **CMS Cloud Manager** project is a tool created at the Cloudfest Hackathon 2025 by [@akinom500](https://github.com/akinom500), [@BrutalBirdie](https://github.com/BrutalBirdie), [@commitnix](https://github.com/commitnix), [@nixautomatix](https://github.com/nixautomatix), [@markoheijnen](https://github.com/markoheijnen), [@ochorocho](https://github.com/ochorocho), led by [@Hayajiro](https://github.com/Hayajiro), and [@javiercasares](https://github.com/javiercasares).

The project is a tool that, in addition to installing a specific CMS, allows for the creation and setup of a server for optimal performance, taking security and efficiency into account.

Here is the [GitHub Project](https://github.com/cmscloudmanager).

Here is a [Blog](#blog) on how the project went.

**Docs**

- [App Documentation](app.md)
- [CLI Documentation](cli.md)
- [User Documentation](user.md)

---

## Blog

![CMS Cloud Manager](https://raw.githubusercontent.com/cmscloudmanager/docs/refs/heads/main/image/photo-004.jpeg)

### The initial idea

The project's initial idea was to develop a tool that simplifies securely setting up a CMS on your own server.

Today, there are plenty of solutions for shared hosting that allow deploying CMS platforms like WordPress with just a single click. But what about options for users who have a VPS or cloud server?

![First team meeting](https://raw.githubusercontent.com/cmscloudmanager/docs/refs/heads/main/image/photo-001.jpeg)

In the past, providers like Cloudways offered systems enabling remote server setup on platforms such as DigitalOcean, complete with secure, scalable WordPress installations and built-in backups. However, these solutions were proprietary and closed.

Could an open solution with similar capabilities be created? The answer is yes, and that's exactly what we're aiming to achieve with this project for the Cloudfest Hackathon 2025.

The project aims to create a tool that allows users to easily deploy a CMS to a cloud server by simply selecting their preferred cloud provider (such as Hetzner, Google, Amazon, Azure, etc.), choosing their desired CMS (WordPress, Drupal, Joomla, etc.), and answering basic questions like "How many daily visitors do you expect?". Based on these inputs, the tool will programmatically provision a suitable server using the cloud provider's API, configure it securely according to best practices, and automatically deploy all necessary components, providing a scalable, hassle-free solution.

### First steps

After presenting the initial concept of the project, the team began by introducing each of its eight members, highlighting their respective skill sets, and exploring ideas for potential features. The team possesses extensive experience in development, systems, and infrastructure—ideal skills for a project like this.

![Initial ideas](https://raw.githubusercontent.com/cmscloudmanager/docs/refs/heads/main/image/photo-005.jpeg)

![Initial ideas](https://raw.githubusercontent.com/cmscloudmanager/docs/refs/heads/main/image/photo-006.jpeg)

The agreed-upon approach involves creating a web-based control panel, which will gather user input through simple questions and generate a YAML file. This YAML file will serve as the initial configuration input for Ansible to provision and set up the server.

![First preview of the panel](https://raw.githubusercontent.com/cmscloudmanager/docs/refs/heads/main/image/screenshot-first.png)

To efficiently manage multiple CMS options and their possible combinations, the CMS deployments will be containerized using Docker. This strategy ensures scalability of volumes—even beyond the initial server—by leveraging the capabilities provided by cloud platforms. Additionally, it facilitates easy migration across different infrastructures and simplifies backup management.

![The team is working hard](https://raw.githubusercontent.com/cmscloudmanager/docs/refs/heads/main/image/photo-002.jpeg)

![The team is working hard](https://raw.githubusercontent.com/cmscloudmanager/docs/refs/heads/main/image/photo-003.jpeg)

### First Recap

Six hours after the project began, we already had several parts up and running. On one hand, the CLI tool—with its various components—was operating independently, so the next step was to connect them.

The APP was also starting to store data and feature a usable interface, initiating the process of selecting the project, connecting to the API to explore available options, and generating the YAML file—or later, executing the CLI directly from the same server.

All of this ended up being developed in Python as a common backend system.

Also, some ideas came up...

![A chat?](https://raw.githubusercontent.com/cmscloudmanager/docs/refs/heads/main/image/screenshot-chat.png)

### Starting the Second Day

On the second day of the Hackathon, a brief meeting was held to review the project's status.

On the API side, all three components that will make it up are ready. The first component will connect to the cloud providers' APIs and enable the provisioning of machines. The second part will configure the elements inside the machine so that Ansible and its playbooks can be used. The third component will launch the playbooks and ultimately create all the services, handle security, and finish setting up the applications and CMS.

The frontend offers several possibilities. For now, the main approach is to launch the project from the local environment in such a way that a YAML file can be generated for later execution using the CLI, and it now allows API keys to be stored in a local database, keeping them readily available and enabling multiple profiles.

### Full Steam Ahead

Setting the day’s priorities has been easy, and now we have the tools!

On one hand, the CLI tool has been finalized by connecting all three parts into one, allowing it to be easily executed by providing the YAML file that contains all the necessary elements to set up the server and create the application or CMS.

On the other hand, the App that allows you to easily create the YAML file, after several steps and meetings, is now working thanks to Docker Compose. This means it can be set up almost anywhere, although it’s designed to work locally to prevent data leaks—such as API Keys—which can be stored locally.

### The End Is Near

It’s the last day in the morning, just 3 hours before the presentation and project delivery.

Now it’s time for the final touches, to finish the details of the presentation and decide what to say, since there are only 5 slides and 5 minutes to present. In fact, tomorrow, Tuesday, the presentation will be given at Cloudfest and will only last 2 minutes. It needs to be clear, concise, and focused on what really needs to be said and explained.
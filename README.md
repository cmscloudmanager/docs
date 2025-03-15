# CMS Cloud Manager documentation

<img src="https://raw.githubusercontent.com/cmscloudmanager/docs/refs/heads/main/image/cmscloudmanager.png" alt="CMS Cloud Manager" width="128">

The **CMS Cloud Manager** project is a tool created at the Cloudfest Hackathon 2025 by [@BrutalBirdie](https://github.com/BrutalBirdie), [@commitnix](https://github.com/commitnix), [@nixautomatix](https://github.com/nixautomatix), and [@markoheijnen](https://github.com/markoheijnen), and led by [@Hayajiro](https://github.com/Hayajiro), and [@javiercasares](https://github.com/javiercasares)

The project is a tool that, in addition to installing a specific CMS, allows for the creation and setup of a server for optimal performance, taking security and efficiency into account.

## The initial idea

The project's initial idea was to develop a tool that simplifies securely setting up a CMS on your own server.

Today, there are plenty of solutions for shared hosting that allow deploying CMS platforms like WordPress with just a single click. But what about options for users who have a VPS or cloud server?

![First team meeting](https://raw.githubusercontent.com/cmscloudmanager/docs/refs/heads/main/image/photo-001.jpeg)

In the past, providers like Cloudways offered systems enabling remote server setup on platforms such as DigitalOcean, complete with secure, scalable WordPress installations and built-in backups. However, these solutions were proprietary and closed.

Could an open solution with similar capabilities be created? The answer is yes, and that's exactly what we're aiming to achieve with this project for the Cloudfest Hackathon 2025.

The project aims to create a tool that allows users to easily deploy a CMS to a cloud server by simply selecting their preferred cloud provider (such as Hetzner, Google, Amazon, Azure, etc.), choosing their desired CMS (WordPress, Drupal, Joomla, etc.), and answering basic questions like "How many daily visitors do you expect?". Based on these inputs, the tool will programmatically provision a suitable server using the cloud provider's API, configure it securely according to best practices, and automatically deploy all necessary components, providing a scalable, hassle-free solution.

## First steps

After presenting the initial concept of the project, the team began by introducing each of its eight members, highlighting their respective skill sets, and exploring ideas for potential features. The team possesses extensive experience in development, systems, and infrastructure—ideal skills for a project like this.

The agreed-upon approach involves creating a web-based control panel, which will gather user input through simple questions and generate a YAML file. This YAML file will serve as the initial configuration input for Ansible to provision and set up the server.

![First preview of the panel](https://raw.githubusercontent.com/cmscloudmanager/docs/refs/heads/main/image/screenshot-first.png)

To efficiently manage multiple CMS options and their possible combinations, the CMS deployments will be containerized using Docker. This strategy ensures scalability of volumes—even beyond the initial server—by leveraging the capabilities provided by cloud platforms. Additionally, it facilitates easy migration across different infrastructures and simplifies backup management.

![The team is working hard](https://raw.githubusercontent.com/cmscloudmanager/docs/refs/heads/main/image/photo-002.jpeg)

![The team is working hard](https://raw.githubusercontent.com/cmscloudmanager/docs/refs/heads/main/image/photo-003.jpeg)

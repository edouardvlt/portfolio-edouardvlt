# Edouard Vallet
**System Admin | Network | Cloud**

[Portfolio](https://edouard-vallet.fr/) | [LinkedIn](https://linkedin.com/in/edouard-vallet/) | [GitHub](https://github.com/Edouardvlt)

---

## About

**Location:** Nantes, France
**Focus:** Cybersecurity, Infrastructure, DevOps
**Status:** Alternance

> "Conception d'architectures systèmes robustes et sécurisées."

### Experience & Education

| Period | Organization | Role / Details |
| :--- | :--- | :--- |
| **2025-2028** | Sup de Vinci, Nantes | Bachelor Info Sys/Network |
| **2024-2025** | ESGI, Nantes | Bachelor 1 & 2 |
| **2025** | Optimix, Lille | Web Development Internship |
| **2023** | Soluce Informatique | IT Support Internship |

---

## Technical Skills

### Systems & Virtualisation
Linux, Bash, Windows, Docker, VMware ESXi.

### Network & Security
OPNsense, Cisco CCNA, Cloudflare Tunnel (Zero Trust).

### Development
Python, C, Go, JavaScript, HTML, CSS, React, PHP.

### Tools
Git, GitHub, VS Code, Figma, MySQL, Grafana.

---

## Featured Projects

### Multi-Site CCNA Project
Infrastructure & Network. Implementation of VLANs, OPNsense, and ESXi.

### Hytale Dashboard
Web Development. Next.js, Socket.io, Leaflet.

### ApplyTrack API
Backend. Node.js, Express, REST Architecture.

### Server Acer (Home Lab)
Infrastructure & DevOps. Docker-based homelab environment.

---

## Portfolio Architecture (High Availability)

This repository contains the source code for my portfolio, which is self-hosted on my personal infrastructure (Home Lab) with an automatic failover system to the cloud to guarantee 100% availability.

### Technical Architecture

The site relies on a modern architecture combining a physical server and Edge services:

*   **Primary Hosting**: Physical server Acer Aspire X1430 running Ubuntu Server.
*   **Containerization**: Application encapsulated in a Docker container (`site-portfolio`).
*   **Reverse Proxy**: Nginx Proxy Manager (NPM) manages internal routing and SSL certificates.
*   **Secure Exposure**: Cloudflare Tunnel (Zero Trust) allows external access without opening ports on the internet router.

### CI/CD & GitOps

Deployment is fully automated to allow instant updates:

1.  **GitHub Actions**: A workflow is triggered on every `git push` to the master branch.
2.  **Webhooks Portainer**: GitHub communicates directly with the Portainer instance on the Acer server to redeploy the stack automatically.
3.  **GitOps**: Synchronization between the GitHub repository and Docker containers in production.

### Resilience & Failover

To mitigate any potential local server failure, a Failover system has been implemented:

*   **Cloudflare Worker**: An Edge script acts as an intelligent router.
*   **Failure Detection**: The Worker tests the health of the Acer server (via `server.edouard-vallet.fr`).
*   **Automatic Switching**: In case of Acer unavailability (timeout or 5xx error), traffic is redirected to GitHub Pages in less than 3 seconds.
*   **Traceability**: Addition of a custom HTTP header `X-Served-By` to identify the source (Acer or GitHub) in real-time.

### Specific Optimizations

*   **Media Management**: Use of a `<video>` tag with `autoplay loop muted` attributes for optimal WebM format support across all browsers.
*   **Remote Access**: Configuration of secure SSH/SFTP access for remote administration via mobile.

---

## Languages & Interests

**Languages**: French (Native), English (B2), German (A2).
**Interests**: Cybersecurity, Sailing, Sci-Fi Cinema, Travel, Coding.
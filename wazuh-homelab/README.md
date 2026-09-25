# Wazuh SIEM Homelab - SOC Environment

Status: In development  
Last update: September 2026  
Author: Pedro Carvalho  
LinkedIn: https://www.linkedin.com/in/pedroalvesc/

## Project Objective

Create a complete Security Operations Center environment using Wazuh open-source SIEM for monitoring, detection, and incident response. This project serves as a practical laboratory for developing Defensive Security skills and functions as a technical portfolio.

### Learning Objectives
Implement and configure enterprise-grade SIEM using Wazuh
Monitor heterogeneous systems including Windows and Linux
Develop custom rules for threat detection
Simulate real attacks and analyze detections
Create security dashboards and reports
Document processes for technical portfolio

## Environment Architecture

Internet
    |
Firewall with UFW
    |
Wazuh Server           Workstations
Ubuntu 22.04 LTS       Monitored Systems
    |                       |
Elastic Stack           Windows 10
Wazuh Manager               Sysmon
Wazuh Indexer               Wazuh Agent
Wazuh Dashboard             Test Applications
                        |
                        Ubuntu 22.04
                            Wazuh Agent
                            Common Services
                            System Logs
                        |
                        Metasploitable 3
                            Vulnerabilities
                            Wazuh Agent
                            Vulnerable Services

## Project Roadmap

### Phase 1: Planning and Installation, October 2026
Duration: 2 weeks
Tasks:
- Define objectives and scope
- Plan technical architecture
- Document hardware and software requirements
- Create installation checklist
- Configure virtualization environment

Deliverables:
- Complete planning documentation
- Architecture diagram
- Installation checklist

### Phase 2: Basic Installation and Configuration, November 2026
Duration: 3 weeks
Tasks:
- Install Wazuh Server on Ubuntu
- Configure Wazuh Manager and Indexer
- Install Wazuh Dashboard with Kibana
- Configure access and authentication
- Test basic installation

Deliverables:
- Functional Wazuh Server
- Accessible dashboard
- Installation documentation

### Phase 3: Agent Integration, December 2026
Duration: 3 weeks
Tasks:
- Install Wazuh Agent on Windows 10
- Configure Sysmon on Windows
- Install Wazuh Agent on Ubuntu
- Configure Linux system logs
- Test agent-server communication

Deliverables:
- Two or more monitored systems
- Log collection active
- Dashboard with real data

### Phase 4: Rules and Detection, January 2027
Duration: 4 weeks
Tasks:
- Configure default Wazuh rules
- Develop custom rules
- Create alerts and notifications
- Develop Kibana dashboards
- Optimize configurations

Deliverables:
- Functional custom rules
- Informative dashboards
- Configured alert system

### Phase 5: Simulation and Analysis, February 2027
Duration: 3 weeks
Tasks:
- Simulate basic attacks
- Analyze generated detections
- Create incident reports
- Adjust rules based on results
- Optimize performance

Deliverables:
- Simulation reports
- Detection analysis
- Optimized rules

### Phase 6: Final Documentation, March 2027
Duration: 2 weeks
Tasks:
- Complete all documentation
- Create step-by-step guides
- Develop specific tutorials
- Document lessons learned
- Prepare project presentation

Deliverables:
- Complete documentation
- Guides and tutorials
- Project presentation

## Technologies Used

### Operating Systems
- Wazuh Server: Ubuntu 22.04 LTS
- Windows Client: Windows 10 or 11 Pro
- Linux Client: Ubuntu 22.04 LTS
- Target: Metasploitable 3

### Security Tools
- SIEM: Wazuh 4.7 or later
- Endpoint Monitoring: Wazuh Agent, Sysmon
- Visualization: Kibana with Wazuh Dashboard
- Log Management: Elastic Stack

### Virtualization
- Proxmox VE, VirtualBox, or VMware
- Vagrant for optional automation

### Documentation
- Markdown for documentation
- PlantUML for diagrams
- Screenshots and recordings

## Repository Structure

wazuh-homelab
    README.md
    architecture
        network-diagram.puml
        system-requirements.md
        installation-checklist.md
    installation
        wazuh-server
        windows-agent
        linux-agent
        sysmon-config
    configuration
        wazuh
        rules
        alerts
        dashboards
    simulation
        attack-scenarios
        detection-analysis
        incident-reports
    documentation
        guides
        tutorials
        lessons-learned
    scripts
        setup
        monitoring
        analysis

## Getting Started

### Prerequisites
1. Hardware:
   - CPU: 4 or more cores, 8 recommended
   - RAM: 16GB or more, 32GB recommended
   - Storage: 100GB or more SSD
   - Virtualization enabled

2. Software:
   - Virtualizer such as Proxmox, VirtualBox, or VMware
   - Ubuntu 22.04 ISO
   - Windows 10 ISO
   - Metasploitable 3 OVA

3. Knowledge:
   - Basic Linux terminal, packages, services
   - Basic networking including IP, subnets, firewall
   - Basic security concepts

### Quick Installation Guide
1. Install Ubuntu Server
2. Install Wazuh using official script:
   curl -sO https://packages.wazuh.com/4.7/wazuh-install.sh
   sudo bash wazuh-install.sh --generate-config-files
3. Install agents on monitored systems
   Windows: Execute .msi installer
   Linux: curl plus apt install

## Project Metrics

| Metric | Target Value | How to Measure |
|--------|--------------|----------------|
| Monitored Systems | 3 or more | Agents connected in dashboard |
| Custom Rules | 10 or more | Active rules in Wazuh |
| Installation Time | Less than 8 hours | First commit to functional system |
| Simulated Attack Detection | 80% or more | Attacks detected versus simulated |
| Response Time | Less than 30 minutes | Detection to initial analysis |

## Implemented Use Cases

### 1. SSH Brute Force Detection
- Rules for multiple SSH login attempts
- Alerts after 5 failed attempts in 5 minutes
- Automatic blocking via firewall integration

### 2. Malicious Process Monitoring
- Detection of suspicious executables in Windows
- Process creation monitoring
- Alerts for known malicious processes

### 3. Windows Log Analysis
- Critical Event IDs monitoring
- Registry change detection
- Suspicious user activity alerts

### 4. File Integrity Monitoring
- FIM on critical directories
- Unauthorized change detection
- System integrity baseline

## Expected Results

### Technical
1. Functional SOC environment with real-time monitoring
2. Dashboard with complete environment visibility
3. Detection rules covering common attacks
4. Documented incident response process

### Professional
1. Demonstrable technical portfolio for recruiters
2. Practical experience with enterprise-grade SIEM
3. Log analysis and threat detection skills
4. Documentation demonstrating technical capability

## Contribution

This is a personal learning project, but suggestions are welcome. If you:
- Found documentation errors
- Have improvement suggestions
- Know tools or technologies that could be added

Please open an issue or contact via LinkedIn.

## Useful Resources

### Official Documentation
- Wazuh Documentation: https://documentation.wazuh.com/
- Elasticsearch Guide: https://www.elastic.co/guide/
- Kibana User Guide: https://www.elastic.co/guide/kibana/

### Tutorials and Guides
- Wazuh Installation Guide: https://documentation.wazuh.com/current/installation-guide/
- Sysmon Configuration: https://github.com/SwiftOnSecurity/sysmon-config
- MITRE ATT&CK Framework: https://attack.mitre.org/

### Communities
- Wazuh Discord: https://discord.gg/wazuh
- Reddit r/Wazuh: https://www.reddit.com/r/Wazuh/
- Stack Overflow Wazuh Tag: https://stackoverflow.com/questions/tagged/wazuh

## License

This project is for educational and portfolio purposes. All content is provided under MIT license.

## Next Steps
1. Configure virtualization environment
2. Install Wazuh Server
3. Document installation process
4. Begin agent configuration

Current Progress: Initial planning, 5% complete

Last update: September 2026 - Planning phase

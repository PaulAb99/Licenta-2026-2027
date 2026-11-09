# **Licenta-2026-2027**
## **Scalable Cyber-Physical IoT Security System with Dynamic Edge-to-Cloud Detection Policy Orchestration**

## Main Concept

  This project aims to modernise the conventional IoT monitoring system with a context-aware, dynamic, and resource-efficient approach. It consists of a scalable and distributed edge-to-cloud camera system with intent-based dynamic filtering and threat detection enabled by a dual AI architecture.
    
  The system provides an automated way of securing a variably restricted area through natural language prompts from an authorised user in real time. Through a chat interface, different rules can be enforced based on an observed person's actions, correlated with adjacent physical sensors, or location in the frame of an individual visual node. A monitored action can be considered an authorised behaviour or may trigger one of the levels of alert. A cloud-based LLM processes the prompt and generates the corresponding ruleset for the local visual model, while a Vision-Language Model (VLM) assists on-demand when fine-grained visual verification is required.        
  
  Configuration is meant to be dynamic, elastic, but secure. Additional Rpi 5 local control nodes or MCU/IP-Cam camera nodes can be set up, but they follow a secure zero-trust network architecture through secure tunnels and encryption, ensuring that only the intended information is exchanged reliably with the cloud component. Furthermore, if an edge node becomes overwhelmed by multiple concurrent streams, a cloud spillover mechanism dynamically offloads excess frame processing to the cloud. Deployed nodes will have a tamper protection mechanism through sensors and emergency short-term memory storage. 
  
  There will also be analytic reports and options to record more or less video data, based on the different alert levels, on a set time or overwrite basis. 


## System Architecture
  
  **Capture Nodes** - 1/2 Cameras paired with MCUs and sensors (e.g., laser/distance for zone correlation, accelerometer/light sensors for physical tamper detection) communicating via MQTT-TLS. 
    
  **Edge Gateway** - Raspberry Pi 5 (implemented in Rust) running a local YOLOv8n with dynamic policy enforcement and short-term memory storage, and dynamic cloud spillover under high CPU load.
        
  **Zero-Trust Network** - Secure tunnel (WireGuard) between edge and cloud with event-driven bandwidth usage and cryptographic signing of alert frames

  **Cloud Control** - Backend (implemented in Go) that manages configurations, handles compute spillover, ingests alerts and emulates virtual nodes for scalability testing, and integrates the Cloud LLM/VLM for prompt enforcement.

  **Interfaces** - Web Dashboard for system control and Telegram bot for mobile natural-language commands and instant alerts.


## Metrics to be evaluated

  **Networking** - Bandwidth savings in streaming vs event driven modes with simulated network degradation; 
  
  **Dual AI & Spillover Latency** - Comparing local execution of policy evaluation against on demand cloud VLM verification, as well as latency stability during edge-to-cloud compute spillover.
  
  **Precision** - Reduction in false positives with sensor fusion and dynamic prompt filtering.
  
  **Resource Footprint and Cloud Scalability** - RPi 5 resources, alongside Cloud backend throughput under simulated multi-node load.




